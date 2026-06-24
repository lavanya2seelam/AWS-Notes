AWS IAM (Identity and Access Management) - Detailed Notes with Examples
These notes are based on the AWS IAM Day-2 class and are written in an interview-friendly format.

1. Why IAM? (Bank Example)
Imagine a Bank.

The bank has:
• Customer Service Desk
• Employee Area
• Locker Room
• Cash Room

When a person enters the bank:

Step 1: Security Guard checks Identity.
Question: Who are you?
Show ID Card.
This is Authentication.

Step 2: After entering, the guard checks where you are allowed to go.

Customer -> Service Desk only
Employee -> Employee Area
Manager -> Locker Room
Cashier -> Cash Room

This is Authorization.

AWS IAM works exactly like this bank.
Authentication = Login
Authorization = Permissions

2. AWS Example
Suppose you are a DevOps Engineer.

You create one AWS Account for your company.

Without IAM:
- Everyone uses the Root Account.
- Any employee can delete EC2, S3 or RDS.
- No security.

With IAM:
- Create separate IAM Users.
- Give only required permissions.
- Root account is never shared.

3. Authentication vs Authorization
Authentication:
Verifies WHO you are.
Example:
Username + Password
IAM User Login

Authorization:
Verifies WHAT you can do.
Example:
Developer can Read S3.
Developer cannot Delete RDS.

4. IAM Components
IAM
|
|-- User
|-- Group
|-- Policy
|-- Role

User -> Person
Policy -> Permissions
Group -> Collection of Users
Role -> Temporary Access

5. Creating an IAM User (Console Steps)
1. Login as Root User.
2. Search 'IAM'.
3. Click IAM.
4. Click Users.
5. Click Create User.
6. Enter Username:
      test-user-501
7. Enable 'Provide user access to the AWS Management Console'.
8. Select 'I want to create an IAM user'.
9. Choose Auto-generated password.
10. Check 'Users must create a new password at next sign-in'.
11. Click Next.
12. Don't attach any policy.
13. Click Create User.
14. Download the CSV.
15. Share Username, Password and Sign-in URL with the user.

6. What happens without a Policy?
The user can log in successfully (Authentication).

But when opening S3 or EC2, AWS shows 'Access Denied'.

Reason:
No Authorization (No Policy attached).

7. Attaching a Policy
Login as Root/Admin.

IAM
 -> Users
 -> test-user-501
 -> Add Permissions
 -> Attach Policies Directly
 -> Search: AmazonS3FullAccess
 -> Select Policy
 -> Next
 -> Add Permissions

Now the user can:
- List Buckets
- Create Buckets
- Delete Buckets (because Full Access)

8. Creating a Group
IAM
 -> User Groups
 -> Create Group
 -> Name: Developers
 -> Attach AmazonS3FullAccess
 -> Create Group

Open Developers Group
 -> Add Users
 -> Select test-user-501
 -> Add Users

Benefit:
All users inside Developers group automatically receive the group's permissions.

9. Why Groups? (Real-time Example)
Company has 500 Developers.

Without Groups:
Create User -> Attach Policy (500 times)

With Groups:
Create Developers Group
Attach Policy Once
Add all developers to the group

Saves time and reduces mistakes.

10. IAM Roles
Roles are used for AWS Services and Applications.

Example:
EC2 needs to read files from S3.

Wrong:
Create IAM User for EC2.

Correct:
Create IAM Role.
Attach the Role to EC2.

Roles provide temporary credentials.

11. Interview Questions
Q1. What is IAM?
Q2. Difference between Authentication and Authorization?
Q3. Why should Root User not be used daily?
Q4. What happens if a User has no Policy?
Q5. Difference between User and Role?
Q6. Why use Groups?
Q7. What is Least Privilege Principle?

12. Quick Revision
IAM = Security Service
User = Authentication
Policy = Permissions
Group = Collection of Users
Role = Temporary Access
Root User = Full Access (Do not use daily)
IAM = Global Service
Policies are written in JSON.
