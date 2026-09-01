# AWS IAM  - Manage Access to AWS Resources

Authentication 
Authorization 
AWS Root Account  --> Enable MFA , unlimited permission 
Admin Access -- > IAM Username and password and Enable MFA , pull permission only if admin policy is attached 
      - cannot delete AWS account 
      - root user password cannot , locked account  cannot be recovered 

 Create A User and attached all Users to Group ( groups Create Cheyali )
Create A Permissions with Permissions then Permissions are attached to group     

Perform this actions using ROOT Account 
Enable MFS  --> Click UserName in AWS --> Security Credentails -->Assign MFA Device 
Create Account Alias - Which is unique globally 
<img width="402" height="62" alt="image" src="https://github.com/user-attachments/assets/c5969ab3-b6d0-4009-afca-4308edc81f10" />

Then Create the Admin User 
Set up Account Settings : 
Then Create IAM Group : Create a 3 different Groups with different permissions 
Then Create a IAM User -- > Attach group policy 
