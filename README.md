# VPC Endpoints

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-endpoints)

**Author:** Albert  
**Email:** tapcyberx@gmail.com

---

## VPC Endpoints

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-networks-endpoints_09bcaa8a)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a private cloud network that you create inside AWS and it is useful because it gives you control over your cloud resources , including which devices you connect, IP addresses, and how traffic flows.

### How I used Amazon VPC in this project

In this project, I used Amazon VPC to connect an S3 bucket and an EC2 instance via a VPC endpoint without public Internet access.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was the way that we can set up endpoints in the best security practice, including policies that also can be attached to IAM roles.

### This project took me...

This project took me around 2.30h trying to understand taking notes and learning the concept of policies.



---

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I will set up a VPC, launch an EC2 instance, and configure an S3 bucket, as these are the core resources for this project’s architecture.

### Step 2 - Connect to EC2 instance

In this step, I will connect to my EC2 instance and test access to S3 to determine whether I have public internet access.



### Step 3 - Set up access keys

In this step, I will create access keys because I need to connect my EC2 Instance with my S3 bucket.

### Step 4 - Interact with S3 bucket

In this step, I will interact with my S3 bucket now that I have created my access key, so I can configure the connection between S3 and the EC2 instance.

---

## Architecture set up

I started my project by launching a VPC and EC2 Instance.

I also set up an Amazon S3 bucket. After creating it, I'll access it from the EC2 instance to manage and inspect its objects.



![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-networks-endpoints_4334d777)

---

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I configured an AWS Access Key ID, AWS Secret Access Key, Default region name and default output format. This four things there I just configure give me the interaction in this case with my S3 bucket.

Access keys are credentials for your applications and other servers to log into AWS and interact with your AWS services/resources.

Secret access keys are a password that pairs with your access key ID. You need both to access AWS services. Secret is a keyword; if anyone who has it can access your AWS account, so we need to secure it in a safe environment.

### Best practice

Although I'm using access keys in this project, a best practice alternative is to use IAM access keys in AWS is to leverage temporary credentials, primarily through the use of IAM Roles. This approach significantly enhances security by eliminating the need to store and manage static, long-lived credentials.

---

## Connecting to my S3 bucket

The command I ran was aws s3 ls. This command is used to list all of the aws resources that can interact with my s3. 

Format your response as 'The terminal responded with nextwork-vpc-project-albert1. This indicated that the access keys I set up confirm that I have access to my S3 bucket.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-networks-endpoints_4334d778)

---

## Connecting to my S3 bucket

I also tested the command aws s3 ls s3://nextwork-vpc-project-  which returned with the objects that I uploaded before in my S3 bucket.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-networks-endpoints_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command sudo touch /tmp/nextwork.txt This command creates blank .txt file inside my EC2 Instances.

The second command I ran was aws s3 cp /tmp/nextwork.txt s3://nextwork-vpc-project-albert1. This command will copy the file nextwork.txt that I just created in my EC2 Instance should be copied in my S3 bucket.

The third command I ran was aws s3 ls s3://nextwork-vpc-project-albert1 which validated that the file nextwork.txt was copy in my S3 bucket.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-networks-endpoints_3e1e79a2)

---

## In the second part of my project...

### Step 5 - Set up a Gateway

In this step, I will set up a VPC endpoint because, with the previous configuration, the S3 bucket was connected to my EC2 instance via the public internet, which is not the most secure practice due to potential interception by external threats.

### Step 6 - Bucket policies

In your own words, start this step by explaining what you're about to do. I'm going to block all traffic that is not related to my VPC endpoint by setting up and S3 bucket policy.

### Step 7 - Update route tables

In this step, I will is my EC2 Instance have access to my S3 bucket because if it can means that I set up endpoint connection perfectly.

### Step 8 - Validate endpoint conection

In this step, I will test if the VPC endpoint its set up correctly because to validate our work, I need to see if the EC2 Instance interact with my S3 bucket.

---

## Setting up a Gateway

I set up an S3 Gateway, which is is a type of endpoint used specifically for Amazon S3 and DynamoDB (DynamoDB is an AWS database service).

### What are endpoints?

An endpoint is a service that allows connection between your VPC and other AWS services without needing the traffic to go over the internet.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-networks-endpoints_09bcaa8a)

---

## Bucket policies

A bucket policy is type of IAM policy designed for setting access permissions to an S3 bucket. Using bucket policies, you get to decide who can access the bucket and what actions they can perform with it.

My bucket policy will denies all actions on your S3 bucket and its objects to everyone, unless is coming from the VPC ID defined in aws:sourceVpce.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-networks-endpoints_7316a13d)

---

## Bucket policies

Right after saving my bucket policy, my S3 bucket page showed 'denied access' warnings. This was because the policy denies all actions unless they come from your VPC endpoint. 

I also had to update my route table because traffic from your EC2 instance is actually trying to get to your S3 bucket through the public internet instead.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-networks-endpoints_4ec7821f)

---

## Route table updates

To update my Route Table, I click on endpoint and select route tables + manage route table, I select public route table and then modify route tables. After that I head back to subnet/ refresh button next to the action and then check the Route Tables again.

After updating my public subnet's route table, my terminal could return with the 2 object that I just created a few minutes ago.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-networks-endpoints_d116818e)

---

## Endpoint policies

An endpoint policy is quickly block off access if you suspect attackers are using your endpoint to access your resources.

I updated my endpoint's policy by switch the effect to Deny I could see the effect of this right away, because my gateway is closed.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-networks-endpoints_3e1e79a3)

---

---
