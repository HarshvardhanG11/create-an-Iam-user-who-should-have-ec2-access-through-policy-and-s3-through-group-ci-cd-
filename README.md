AWS IAM User Setup – EC2 Access (Policy) & S3 Access (Group: ci-cd)
📘 Project Overview

This project demonstrates how to create an IAM User in AWS who has:

EC2 access through a directly attached policy

S3 access through membership in a group (ci-cd)

It is designed for AWS beginners to understand role-based access control (RBAC) using IAM, policies, and groups.

☁️ Prerequisites

Before starting, ensure you have:

An active AWS account

Access to the AWS Management Console

Basic knowledge of IAM concepts (Users, Groups, Policies)

🧩 Step 1: Create an IAM Group (ci-cd)

Go to IAM Dashboard → User groups → Create group

Enter Group name: ci-cd

Click Next to attach policies

Search for and attach:

AmazonS3FullAccess (or choose a custom limited S3 policy if needed)

Click Create group

✅ Now the ci-cd group has S3 permissions.

🧩 Step 2: Create a Custom EC2 Policy

Go to IAM Dashboard → Policies → Create policy

Choose JSON and paste the following:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:Describe*",
        "ec2:StartInstances",
        "ec2:StopInstances"
      ],
      "Resource": "*"
    }
  ]
}


Click Next → Next → Create policy

Name it: EC2AccessPolicy

✅ You’ve created a custom EC2 policy that allows viewing, starting, and stopping EC2 instances.

🧩 Step 3: Create an IAM User

Go to IAM Dashboard → Users → Create user

Enter User name: DevUser (or your preferred name)

Click Next

Check “Provide user access to the AWS Management Console” (optional for UI access)

Click Next → Set permissions

🧩 Step 4: Attach Permissions to the User

You’ll now give the user access through both:

A Group (ci-cd) → for S3 access

A Policy (EC2AccessPolicy) → for EC2 access

➤ Add to Group

Under “Add user to groups,” select ci-cd

➤ Attach EC2 Policy

Under “Attach policies directly,” select EC2AccessPolicy

Click Next → Create user

✅ User created successfully!

🔑 Step 5: Access Keys (Optional for CLI Access)

If the user needs to use the AWS CLI:

Click on the user → Security credentials tab

Under Access keys, click Create access key

Save the Access key ID and Secret access key

🧠 Verification
Check S3 Access:

Run:

aws s3 ls


Should list all S3 buckets (because of group ci-cd).

Check EC2 Access:

Run:

aws ec2 describe-instances


Should show EC2 instances (because of EC2AccessPolicy).

🧾 Summary
Access Type	Method	Policy / Group	Description
EC2	Direct Policy	EC2AccessPolicy	Allows describe/start/stop instances
S3	Group Membership	ci-cd	Provides full access to S3
🧰 Tools Used

AWS IAM

AWS Management Console

AWS CLI (optional)

📜 License

This project is open-source and free to use for educational purposes.
