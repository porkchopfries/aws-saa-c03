# IAM 
## 1.1 IAM Overview

* AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. With IAM, you can centrally manage     permissions that control which AWS resources users can access. You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources

## 1.1.1 Overview of IAM

* Attach IAMOverview-1.png
* IAM Principals must be **authenticated** to send requests (with a few exceptions)
* A principal is a person or application that can make a request for an **action** or **operation** on an AWS resource 
* AWS determines whether to **authorise** the request (allow/deny)
* **Actions** are **authorised** on AWS **resources** 

## 1.2 IAM Users
* Identity used for anything requiring **long-term** AWS access
    * Humans
    * Applications
    * Service Accounts
* When a **principal** wants to **request** to perform an action, it will **authenticate** against an identity within IAM. An IAM user is an identity which can be used in this way.
* There are two ways to authenticate:
    * Username and Password
    * Access Keys (CLI)
* Once the **Principal** has authenticated, it becomes an **authenticated identity**

## 1.2.1 Amazon Resource Name (ARN)
* Attach IAMUsers-2.png
* Uniquely identify resources within any AWS accounts.
* This allows you to refer to a single or group of resources. This prevents individual resources from the same account but in different regions from being confused.
* partition: almost always **aws** unless it is china **aws-cn**
* region: can be a double colon (::) if that doesn't matter
* account-id: the account that owns the resource
    * EC2 needs this
    * S3 does not need account-id because its globally unique
* resource-type/id: changes based on the resource
* An example that leads to confusion:
* arn:aws:s3:::catgifs
    * This references an actual bucket
* arn:aws:s3:::catgifs/*
    * This refers to objects in that bucket, but not the bucket itself
* **These two ARNs do not overlap**

## 1.2.2 FAQ
* 5,000 IAM users per account
* IAM user can be a member of 10 groups

## 1.3 IAM Groups 
* Attach IAM-Groups-1.png
* Containers for users. **You cannot login to IAM groups** 
* They have no credentials of their own, used solely for management of IAM users
* Benefits of Groups
    1. Effective administrative style management of users based on the team
    2. Groups can have Inline and Managed policies attached
* AWS merges all of the policies into a set of permissions 
* Limitations of Groups
    1. 5000 iam user limit applies to Groups
    2. There is no all iam users in Group, you can create a group and add all users into that group, but it needs to be created and managed on your own
    3. No nesting
    4. 300 Groups limit per account, this can be fixed with support ticket 
* **GROUPS ARE NOT A TRUE IDENTITY THEY CAN'T BE REFERENCED AS A PRINCIPAL IN A POLICY**

## 1.3 Identity Policies
* Identity Policies are attached to AWS identities and either ALLOW or DENY access to AWS resources
* It's created using JSON

* High Level Overview of IAM Policies
Attach IAMPolicies-1.png

* Function of IAM Policies
    * IAM Policies consist of 1 or more statements, each statment has a unique identifier called Statment ID aka SID 
    * SID is useful for identifying and managing individual statements within a policy
    * Example - "Sid" : "FullAccess" or "Sid" : "DenyCatBucket"
    * Effect is either Allow or Deny
    * Example - "Effect" : "Allow" or "Effect" : "Deny" 
    * Action - match 1 or more actions, use wildcard * to match specific AWS resource action
    * Example - "Action" : ["s3:GetObject"] or "Action" : ["s3:*"]
    * Resource specify individual AWS resources or specify list of AWS resources
    * Example - "Resource" : ["*"] or "Resource" : ["arn:aws:s3:::catgifts", "arn:aws:s3:::catgifts/*"]

* IAM Policies with overlap statment
Attach IAMPolicies-2.png

* Explicit Deny > Explicit Allow > Default Deny
    * If there is deny in IAM Policies, the user will not have access and you can't overwrite the policy.
    * Deny > Allow > Deny

* IAM with resource policy
Attach IAMPolicies-3.png

* Functions of resource policy

* Sally has multiple policies, Policy 1 & Policy 2.
* Sally has group called Developers Group, which also has resource policy being attached
* Deny > Allow > Deny comes into place to check Sally permission access

* IAM with inline policy
Attach screenshots of the diagram
Attach IAMPolicies-4.png

* Functions of inline policy

* IAM with managed policy
Attach screenshots of the diagram
Attach IAMPolicies-4.png
    
* Functions of managed policy

