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

# Concept


AWS IAM (Identity and Access Management) policies are JSON-based permission documents that define what actions a user, group, or role can perform on which AWS resources, under what conditions. [Citation]
A custom policy gives fine-grained (granular) control beyond predefined AWS managed policies — allowing organizations to restrict or permit specific actions on specific resources. [Citation]
Every IAM policy is built around three core mandatory elements: Effect, Action, and Resource (commonly abbreviated as EAR). [Citation]
Policy precedence rule: An explicit Deny always overrides any Allow — if any policy attached to a user contains a Deny for an action, that action is denied regardless of other Allow policies. [Citation]
Implicit Deny: If no policy explicitly allows an action, access is denied by default — AWS does not grant access unless explicitly permitted. [Citation]
Condition is an optional but powerful element that restricts when a policy applies — for example, limiting access to a specific IP address range or requiring MFA. [Citation]
SID (Statement ID) is an optional label/comment field within a policy statement used to describe the intent of that statement. [Citation]
---
What I understood
JSON Policy Structure
A valid IAM policy JSON document begins with opening braces {} and contains a Version field, always set to "2012-10-17" — this value never changes. [Citation]
Inside the policy, a Statements array holds one or more individual permission blocks, each enclosed in {} within square brackets []. [Citation]
Each statement contains the three mandatory fields: [Citation]
    Effect: Either "Allow" or "Deny" — only two valid values exist.
    Action: Specifies which AWS API actions are permitted or denied (e.g., ec2:StartInstances, s3:ListObjects, s3:GetObject, s3:DeleteObjects).
    Resource: Specifies the ARN (Amazon Resource Name) of the resource(s) the policy applies to — can be a wildcard * for all resources or a specific ARN.
ARN (Amazon Resource Name) is a unique identifier for every AWS resource — analogous to a barcode or unique ID number — used to precisely target specific resources in a policy. [Citation]
Example of a multi-action policy statement covering both EC2 and S3: [Citation]
    Actions: ec2:StartInstances, ec2:StopInstances, s3:ListObjects, s3:GetObject, s3:DeleteObjects
    Multiple actions are listed inside a square bracket array []
    Resource: specific ARN (e.g., arn:aws:ec2:ap-south-1:123456:instance/...) or * for all
EAR — The Core Policy Elements
Effect — Determines whether the policy allows or denies the action; must be either Allow or Deny. [Citation]
Action — Defines what API operation is being controlled; uses the format service:ActionName (e.g., ec2:StartInstances, s3:GetObject, ec2:* for all EC2 actions). [Citation]
Resource — Defines the specific AWS resource(s) the policy applies to; using * grants access to all resources of that type, while a specific ARN restricts to a single resource. [Citation]
Wildcard (*) Usage
Using ec2:* as the action grants full access to all EC2 operations — start, stop, reboot, terminate, create, delete, etc. [Citation]
Using * as the resource grants permissions across all resources of the specified service.
While convenient, using wildcards (especially ec2:* or *) is not recommended in production — granular permissions are the best practice. [Citation]
Multiple Statements in One Policy
A single policy document can contain multiple statements, each with its own Effect, Action, and Resource. [Citation]
Example: One statement grants full EC2 permissions; a second statement grants S3 GetObject (read-only) permissions — both coexist in the same policy. [Citation]
Statements are separated by commas inside the Statements array.
Deny Policy and Conflict Resolution
When a Deny and an Allow exist in the same policy or across attached policies for the same action, Deny always wins — no exceptions. [Citation]
Example scenario: A user has a policy allowing full S3 permissions AND a separate statement denying s3:DeleteBucket. [Citation]
    If the user tries to delete a bucket → AWS checks for any Deny first → Deny found → Access Denied, no questions asked.
    If the user tries to create a bucket → AWS checks for Deny → No Deny found → AWS checks for Allow → Allow found → Access Granted.
    If the user tries to create a VPC → No policy covers VPC at all → No explicit Allow exists → Implicit Deny → Access Denied. [Citation]
The policy evaluation flow: [Citation]
    Check for explicit Deny → if found, deny immediately.
    Check for explicit Allow → if found, allow.
    If neither → implicit deny (default behavior).
SID — Statement Identifier
SID is an optional field that acts like a comment or label for a policy statement. [Citation]
Example SID value: "This policy will allow users to perform any action on EC2 instances and read S3 objects"
Helps administrators understand the intent of each statement without reading the full JSON logic.
Condition Element
Condition is an optional fourth element that adds constraints on when a policy applies. [Citation]
Two common use cases demonstrated: [Citation]
    IP Address restriction: Policy only applies if the request originates from a specific IP range (e.g., office network 0.0.0.0/16 or VPN IP 203.x.x.x/32). If the user is not on the office network or VPN, access is denied even if the policy would otherwise allow it. [Citation]
    MFA (Multi-Factor Authentication) requirement: Policy only applies if the user has MFA configured and active. Without MFA, the user cannot access the resource even if the Allow policy is attached. [Citation]
Conditions make policies context-aware — the same user can have different effective permissions depending on their network location or authentication state.
Visual Policy Editor
AWS provides two methods to create custom policies: [Citation]
    JSON editor: Write raw JSON directly — requires knowledge of JSON structure and AWS action names.
    Visual editor: A GUI-driven interface that has matured significantly — allows creation of granular permissions without writing JSON manually.
In the Visual editor, selecting a service (e.g., EC2) dynamically loads all available action categories: [Citation]
    List actions (e.g., DescribeInstances, DescribeVolumes)
    Read actions (e.g., GetConsoleOutput, GetPasswordData)
    Write actions (e.g., CreateKeyPair, CreateLaunchTemplate, CopyImage, CopySnapshot)
    Tagging actions (e.g., CreateTags, DeleteTags)
    Permission management actions
Selecting specific actions (e.g., only DescribeInstances under List) creates a granular permission — the user can only describe instances, not start, stop, or terminate them. [Citation]
After selecting actions, you specify Resources: either all (*) or a specific ARN. [Citation]
Visual editor and JSON editor are synchronized — changes in one are reflected in the other automatically. [Citation]
Live Demo — Custom Policy Creation and Testing
A custom policy named "full access to EC2 instances" was created: [Citation]
    Action: ec2:* (all EC2 actions)
    Resource: * (all resources)
This policy was attached to a test user (S3 Admin / DevOps Engineer user) with console access and a custom password. [Citation]
Testing in incognito window: [Citation]
    Attempted to create an S3 bucket → Denied — policy does not grant S3 permissions.
    Attempted to launch an EC2 instance → Denied — even with EC2 full access policy, the AMI (Amazon Machine Image) used was from another account/region, causing an authorization error. [Citation]
    Successfully launched an EC2 instance using the correct AMI → Confirmed full EC2 access works. [Citation]
Granular Custom Policy — 4 Actions Only
The policy was then edited to restrict the user to only 4 specific EC2 actions: [Citation]
    ec2:RebootInstances
    ec2:StartInstances
    ec2:StopInstances
    ec2:DescribeInstances
After saving, the user could no longer launch new instances — only start, stop, reboot, and describe existing ones. [Citation]
In the EC2 console, the user could see instances but volume descriptions failed because DescribeVolumes was not included — demonstrating true granularity. [Citation]
Only the 4 permitted actions appeared as enabled options in the instance action menu; all others were grayed out or returned "not authorized." [Citation]
S3 Custom Policy Demo
A separate S3 policy was constructed targeting a specific S3 bucket (Terraform demo bucket): [Citation]
    Actions: s3:GetObject (download), s3:PutObject (upload)
    Resource: Specific bucket ARN copied from the bucket properties [Citation]
In the Visual editor, S3 object-level actions were found under the Object category: [Citation]
    GetObject — grants permission to retrieve/download objects from S3
    PutObject — grants permission to upload/add objects to a bucket
    RestoreObject — also available but not selected
---
What I didn't fully get
Why ARN Matters for Resource Specification
ARN uniquely identifies every AWS resource — without specifying the correct ARN, a policy either applies too broadly (using *) or fails to target the right resource. [Citation]
ARN format for EC2: arn:aws:ec2:<region>:<account-id>:instance/<instance-id>
When you copy an ARN from the AWS console (e.g., from an S3 bucket's Properties tab), you can paste it directly into the Resource field of a policy to ensure the policy applies only to that specific resource. [Citation]
Using * as the resource is called "overly promiscuous" — it grants access to all resources of that type, which is a security risk in production environments. [Citation]
Conflicting Statements — How AWS Resolves Them
When a user has multiple policies attached (directly or via groups), AWS evaluates all of them together. [Citation]
The resolution logic is strict:
    Any explicit Deny in any attached policy = immediate denial, regardless of any Allow anywhere.
    An explicit Allow with no conflicting Deny = access granted.
    No matching policy at all = implicit deny (access denied by default).
This means you can safely write broad Allow policies and then layer specific Deny statements on top to carve out exceptions — the Deny will always take precedence. [Citation]
Condition Operators
Conditions use operators to compare request attributes against expected values. [Citation]
For IP address conditions, the operator checks whether the request's source IP falls within a specified CIDR range.
For MFA conditions, the operator checks whether the authenticated session has MFA active.
Multiple conditions can be combined — e.g., require BOTH a specific IP range AND MFA to be present for access to be granted. [Citation]
Visual Editor vs. JSON — When to Use Which
JSON is preferred when you need to write complex, multi-statement policies quickly or when copying policy templates. [Citation]
Visual editor is better for beginners or when you need to discover available actions for a service without memorizing action names. [Citation]
Both produce identical output — the visual editor generates valid JSON behind the scenes, and any JSON written manually is reflected in the visual editor. [Citation]
Azure IAM vs. AWS IAM
In Azure, IAM is more streamlined — it integrates with Active Directory, where users and groups are managed centrally, and IT admins handle most configurations. [Citation]
In AWS, IAM is more explicit — you must manually create users, groups, and policies, and attach them deliberately.
AWS IAM gives more granular control but requires more intentional configuration compared to Azure's AD-integrated approach.
---
Might show up on the exam
JSON policy version is always "2012-10-17" — never changes, never use a different value. [Citation]
EAR = Effect + Action + Resource — the three mandatory fields in every IAM policy statement; SID and Condition are optional. [Citation]
Effect values: Only two valid options — "Allow" or "Deny" — no other values are accepted. [Citation]
Deny always wins: Explicit Deny overrides any Allow — this is the most tested IAM concept. No exceptions. [Citation]
Implicit Deny: If no policy grants access, access is denied by default — AWS does not allow anything unless explicitly permitted. [Citation]
Policy evaluation order: (1) Check for explicit Deny → (2) Check for explicit Allow → (3) Implicit Deny if neither found. [Citation]
Wildcard * in Action: ec2:* = all EC2 actions; s3:* = all S3 actions; * alone = all actions on all services (extremely broad, not recommended). [Citation]
Wildcard * in Resource: Grants permissions on all resources of the specified service — use specific ARNs for least-privilege access. [Citation]
ARN uniqueness: Every AWS resource has a unique ARN — used to precisely target resources in policies. [Citation]
SID is optional: Acts as a label/comment — does not affect policy logic or enforcement. [Citation]
Condition use cases to know: IP address restriction (CIDR range), MFA requirement — both are common exam scenarios. [Citation]
Two policy editor types: Visual editor and JSON editor — both produce the same output; visual editor auto-updates JSON. [Citation]
Custom vs. Managed policies: AWS-managed policies are predefined; custom policies are user-created for specific organizational requirements. [Citation]
Multiple statements: A single policy document supports multiple statements — each can have different Effect, Action, Resource combinations. [Citation]
Conflicting Allow + Deny on same action: Deny wins — user cannot perform the action regardless of the Allow. [Citation]
No matching policy = implicit deny: If a user tries an action not covered by any policy, it is denied automatically — not an error, just a default deny. [Citation]
