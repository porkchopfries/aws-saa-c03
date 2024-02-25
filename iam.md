# IAM Identity Policies
* What is it?
    * Identity Policies are attached to AWS identities and either ALLOW or DENY access to AWS resources.
    * It's created using JSON. 

* High Level Overview of IAM Policies
Attach IAMPolicies-1.png

* Function of IAM Policies
    * IAM Policies consist of 1 or more statements, each statment has a unique identifier called Statment ID aka SID. 
    * SID is useful for identifying and managing individual statements within a policy. 
    * Example - "Sid" : "FullAccess" or "Sid" : "DenyCatBucket"
    * Effect is either Allow or Deny.
    * Example - "Effect" : "Allow" or "Effect" : "Deny" 
    * Action - match 1 or more actions, use wildcard * to match specific AWS resource action.
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
* Sally has group called Developers Group, which also has resource policy being attached. 
* Deny > Allow > Deny comes into place to check Sally permission access.

* IAM with inline policy
Attach screenshots of the diagram
Attach IAMPolicies-4.png

* Functions of inline policy

* IAM with managed policy
Attach screenshots of the diagram
Attach IAMPolicies-4.png
    
* Functions of managed policy
