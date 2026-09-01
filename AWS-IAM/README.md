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



# Custom Policies in AWS 
1. visual Policy
2.  JSON Policies

## IAM Policy Structure

An IAM policy is a JSON document that defines:

- **Who** can perform an action
- **What actions** they can perform
- **Which resources** they can access
- **Under what conditions** the actions are allowed or denied

### Example Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowEC2AndS3Access",
      "Effect": "Allow",
      "Action": [
        "ec2:StartInstances",
        "s3:ListBucket",
        "s3:GetObject"
      ],
      "Resource": "*",
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": [
            "172.16.0.0/16",
            "203.78.98.0/32"
          ]
        }
      }
    },
    {
      "Sid": "AllowS3ObjectAccess",
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "*"
    }
  ]
}

In AWS IAM policy evaluation, an explicit Deny has higher precedence than Allow.

# AWS IAM Policies – Complete Notes

## 1. What is an IAM Policy?

An **AWS IAM Policy** is a JSON document that defines what actions a user, group, or role can perform on AWS resources.

A policy mainly defines:

```text
Effect + Action + Resource
```

You can remember this as:

```text
EAR

E → Effect
A → Action
R → Resource
```

These are the most important parts of an IAM policy.

---

# 2. Ways to Create an IAM Policy

AWS provides two main ways to create a policy:

1. **Visual Editor**
2. **JSON Editor**

The Visual Editor makes it easier to select services, actions, resources, and conditions. The JSON editor allows you to directly define the policy structure.

---

# 3. Basic IAM Policy Structure

A basic IAM policy looks like this:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowSpecificActions",
      "Effect": "Allow",
      "Action": [
        "ec2:StartInstances",
        "ec2:StopInstances",
        "s3:ListBucket",
        "s3:GetObject"
      ],
      "Resource": "*"
    }
  ]
}
```

---

# 4. Version

```json
"Version": "2012-10-17"
```

This specifies the version of the IAM policy language.

`2012-10-17` is the commonly used IAM policy version.

---

# 5. Statement

```json
"Statement": []
```

The `Statement` contains the actual permission rules.

You can have:

* One statement
* Multiple statements

Example:

```text
Statement
   │
   ├── Statement 1 → EC2 permissions
   │
   ├── Statement 2 → S3 permissions
   │
   └── Statement 3 → Deny a specific action
```

Multiple statements can be used when different permissions or conditions are required.

---

# 6. Sid

```json
"Sid": "AllowSpecificActions"
```

`Sid` means **Statement ID**.

It is an optional label/identifier for a statement.

You can think of it as:

```text
Sid = Label / Name / Comment for the statement
```

For example:

```json
"Sid": "AllowEC2Management"
```

This helps administrators understand what the statement is intended to do.

---

# 7. Effect

```json
"Effect": "Allow"
```

`Effect` determines whether the permission is allowed or denied.

There are only two values:

```text
Allow
Deny
```

Example:

```json
"Effect": "Allow"
```

means the action is permitted.

Example:

```json
"Effect": "Deny"
```

means the action is explicitly denied.

---

# 8. Action

The `Action` specifies **what the user is allowed or denied to do**.

Example:

```json
"Action": [
  "ec2:StartInstances",
  "ec2:StopInstances",
  "ec2:RebootInstances"
]
```

This allows the specified EC2 actions.

For S3:

```json
"Action": [
  "s3:ListBucket",
  "s3:GetObject",
  "s3:PutObject"
]
```

Examples of actions:

```text
ec2:StartInstances
ec2:StopInstances
ec2:RebootInstances

s3:ListBucket
s3:GetObject
s3:PutObject
s3:DeleteObject
```

AWS permissions can be made very granular. For example, instead of giving full EC2 access, you can give a user only:

```text
Start instance
Stop instance
Reboot instance
Describe instances
```

## This is called **granular permissions**.

# 9. Resource

The `Resource` specifies **which AWS resource the permission applies to**.

Example:

```json
"Resource": "*"
```

`*` means all applicable resources.

However, instead of allowing access to everything, you can specify a particular resource using its **ARN**.

Example:

```text
arn:aws:ec2:region:account-id:instance/instance-id
```

Think of an ARN as a unique identifier for an AWS resource.

```text
Resource = Which resource?
Action   = What can I do?
```

The training notes emphasize that resources can be restricted to specific resources rather than giving access to everything.

---

# 10. Condition

A `Condition` adds an additional requirement that must be satisfied before the policy applies.

Example:

```json
"Condition": {
  "IpAddress": {
    "aws:SourceIp": [
      "172.16.0.0/16",
      "203.78.98.0/32"
    ]
  }
}
```

This can be used to restrict access based on the source IP address.

For example:

```text
User
  │
  ▼
AWS Request
  │
  ▼
Is request coming from allowed IP?
  │
  ├── YES → Permission can apply
  │
  └── NO  → Permission does not apply
```

The training notes give IP address restrictions as an example of using conditions, including restricting access to an office/VPN IP range.

---

# 11. MFA Condition

A condition can also be used to require MFA.

Conceptually:

```text
User
  │
  ▼
MFA configured/authenticated?
  │
  ├── YES → Access can be allowed
  │
  └── NO  → Access can be denied
```

Conditions can therefore be used to add additional security requirements to resource access.

---

# 12. Multiple Actions in One Statement

If multiple actions have the same Effect, Resource, and Condition, they can be placed in one statement.

Example:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "EC2AndS3Access",
      "Effect": "Allow",
      "Action": [
        "ec2:StartInstances",
        "ec2:StopInstances",
        "ec2:RebootInstances",
        "s3:ListBucket",
        "s3:GetObject"
      ],
      "Resource": "*"
    }
  ]
}
```

---

# 13. Multiple Statements

Multiple statements are useful when permissions have different requirements.

Example:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowEC2Actions",
      "Effect": "Allow",
      "Action": [
        "ec2:StartInstances",
        "ec2:StopInstances",
        "ec2:RebootInstances"
      ],
      "Resource": "*"
    },
    {
      "Sid": "AllowS3Read",
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket",
        "s3:GetObject"
      ],
      "Resource": "*"
    }
  ]
}
```

Each statement can have its own:

```text
Effect
Action
Resource
Condition
```

---

# 14. Explicit Deny Has Highest Precedence

This is one of the **most important IAM concepts**.

> **An explicit Deny overrides an Allow.**

Suppose a user has:

```text
Allow → s3:DeleteBucket
```

but another policy contains:

```text
Deny → s3:DeleteBucket
```

The result is:

```text
❌ DENIED
```

Even though an Allow exists.

The training notes specifically explain that AWS checks for a deny and that **Deny has the highest precedence**.

---

# 15. IAM Policy Evaluation – Simple Flow

Remember this flow:

```text
                AWS Request
                     │
                     ▼
          ┌─────────────────────┐
          │ Is there an explicit│
          │       DENY?         │
          └──────────┬──────────┘
                     │
             ┌───────┴───────┐
            YES              NO
             │                │
             ▼                ▼
        ❌ DENY        Is there an ALLOW?
                              │
                       ┌──────┴──────┐
                      YES            NO
                       │              │
                       ▼              ▼
                   ✅ ALLOW       ❌ DENY
                                  (Implicit)
```

### Remember:

```text
Explicit Deny
     ↓
Highest precedence
     ↓
❌ DENY
```

If there is no explicit Deny, there must be an applicable Allow.

If there is no applicable Allow, the request is denied.

---

# 16. Example – Allow + Deny Conflict

Suppose:

### Policy 1

```json
{
  "Effect": "Allow",
  "Action": "s3:DeleteBucket",
  "Resource": "*"
}
```

### Policy 2

```json
{
  "Effect": "Deny",
  "Action": "s3:DeleteBucket",
  "Resource": "*"
}
```

The user tries:

```text
Delete S3 Bucket
```

Both policies match:

```text
Allow → YES
Deny  → YES
```

Final result:

```text
❌ DENIED
```

Why?

```text
Explicit Deny > Allow
```

---

# 17. Implicit Deny

There is another type of denial called **implicit deny**.

Suppose the user has:

```text
Allow:
  ec2:StartInstances
```

But the user tries:

```text
ec2:TerminateInstances
```

There is no Allow for `TerminateInstances`.

Therefore:

```text
No Allow
+
No Explicit Deny
        ↓
Implicit Deny
        ↓
❌ DENIED
```

The training notes distinguish this situation from an explicit Deny.

---

# 18. Explicit Deny vs Implicit Deny

| Type          | Meaning                                                      | Result    |
| ------------- | ------------------------------------------------------------ | --------- |
| Explicit Deny | A policy specifically says `Deny`                            | ❌ Denied  |
| Implicit Deny | No applicable Allow exists                                   | ❌ Denied  |
| Allow         | An applicable Allow exists and no explicit Deny overrides it | ✅ Allowed |

Remember:

```text
Explicit Deny → strongest
No Allow      → implicit deny
Allow         → access granted if not explicitly denied
```

---

# 19. Full Access vs Granular Access

### Full access

Example:

```text
EC2
 └── *
```

This represents very broad EC2 permissions.

A user may be able to perform many EC2 operations.

### Granular access

Instead of:

```text
ec2:*
```

you can specify:

```text
ec2:StartInstances
ec2:StopInstances
ec2:RebootInstances
ec2:DescribeInstances
```

The user can then perform only the required activities.

The training demonstrates this approach by giving a user only four EC2 activities: start, stop, reboot, and describe instances.

---

# 20. Principle of Least Privilege

A good IAM policy should provide only the permissions required to perform the job.

Instead of:

```text
EC2 → Full Access
```

give:

```text
EC2
 ├── StartInstances
 ├── StopInstances
 ├── RebootInstances
 └── DescribeInstances
```

Instead of:

```text
S3 → Full Access
```

give:

```text
S3
 ├── ListBucket
 └── GetObject
```

This reduces unnecessary access and improves security.

---

# 21. S3 Example

Suppose a user needs to download objects from an S3 bucket.

Required actions could include:

```text
s3:ListBucket
s3:GetObject
```

If the user also needs to upload:

```text
s3:PutObject
```

If the user needs to delete objects:

```text
s3:DeleteObject
```

Therefore, permissions should be based on the actual requirement.

---

# 22. Example – Read-Only EC2 User

A user needs to view EC2 information but should not start, stop, or terminate instances.

Policy concept:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "EC2ReadOnly",
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeInstances"
      ],
      "Resource": "*"
    }
  ]
}
```

The user can view the required EC2 information but does not have permission to start or stop instances.

---

# 23. Example – EC2 Operations User

A user needs only:

```text
Start
Stop
Reboot
Describe
```

Example:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "EC2Operations",
      "Effect": "Allow",
      "Action": [
        "ec2:StartInstances",
        "ec2:StopInstances",
        "ec2:RebootInstances",
        "ec2:DescribeInstances"
      ],
      "Resource": "*"
    }
  ]
}
```

This is more granular than giving:

```text
ec2:*
```

---

# 24. Example – S3 Read and Write

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "S3ReadWrite",
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket",
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "*"
    }
  ]
}
```

This allows the specified S3 activities.

---

# 25. Example – Allow S3 but Deny Delete

Suppose a user should have broad S3 access but must **never delete objects**.

Conceptually:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowS3Access",
      "Effect": "Allow",
      "Action": "s3:*",
      "Resource": "*"
    },
    {
      "Sid": "DenyObjectDeletion",
      "Effect": "Deny",
      "Action": "s3:DeleteObject",
      "Resource": "*"
    }
  ]
}
```

The user has:

```text
S3 Allow → YES
DeleteObject Deny → YES
```

Therefore:

```text
❌ DeleteObject = DENIED
```

because:

```text
Explicit Deny overrides Allow
```

---

# 26. Important IAM Terms

| Term                | Meaning                                   |
| ------------------- | ----------------------------------------- |
| Policy              | Defines permissions                       |
| Statement           | Individual permission rule                |
| Sid                 | Label/identifier for a statement          |
| Effect              | Allow or Deny                             |
| Action              | Operation the user can perform            |
| Resource            | AWS resource the action applies to        |
| Condition           | Additional requirement                    |
| ARN                 | Unique identifier for an AWS resource     |
| Explicit Deny       | Policy explicitly says Deny               |
| Implicit Deny       | No applicable Allow                       |
| Granular Permission | Permission for a specific action/resource |

---

# 27. Easy IAM Policy Formula

Remember:

```text
POLICY
  │
  ├── Version
  │
  └── Statement
        │
        ├── Sid       → Label
        ├── Effect    → Allow / Deny
        ├── Action    → What?
        ├── Resource  → Which resource?
        └── Condition → Under what condition?
```

The most important part to remember:

```text
Effect + Action + Resource
```

And for policy evaluation:

```text
Explicit DENY
      ↓
Overrides ALLOW
```

---

# 28. Interview Questions

### Q1. What is an IAM policy?

An IAM policy is a JSON document that defines permissions for AWS resources.

### Q2. What are the two ways to create an IAM policy?

```text
1. Visual Editor
2. JSON Editor
```

### Q3. What are the two possible values for Effect?

```text
Allow
Deny
```

### Q4. What does Action define?

It defines the AWS operation that can be performed.

Example:

```text
ec2:StartInstances
```

### Q5. What does Resource define?

It defines which AWS resource the action applies to.

### Q6. What does Condition do?

It adds additional conditions that must be satisfied for the statement to apply.

### Q7. Which has higher precedence: Allow or Explicit Deny?

```text
Explicit Deny
```

### Q8. What happens if one policy allows an action and another explicitly denies it?

```text
❌ DENIED
```

### Q9. What is implicit deny?

If there is no applicable Allow, access is denied by default.

### Q10. Why use granular permissions?

To give users only the permissions they actually need instead of unnecessary full access.

---

# 29. Golden Rules to Remember

```text
1. IAM policies are JSON documents.

2. A policy contains one or more Statements.

3. Sid is an optional label/identifier.

4. Effect can be Allow or Deny.

5. Action defines WHAT the user can do.

6. Resource defines WHERE the action can be performed.

7. Condition defines additional requirements.

8. ARN identifies a specific AWS resource.

9. Explicit Deny overrides Allow.

10. No applicable Allow results in implicit Deny.

11. Prefer granular permissions over unnecessary full access.

12. Use Conditions when access needs additional restrictions
    such as source IP or MFA requirements.
```

## One-line memory trick

```text
Action   = WHAT can I do?
Resource = WHERE can I do it?
Condition = UNDER WHAT CONDITIONS?
Effect   = ALLOW or DENY?

And remember:

EXPLICIT DENY > ALLOW
```

