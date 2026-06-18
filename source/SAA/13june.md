
# ExamPrepper 13/06/2026


1. A company has two VPCs named Management and Production. The Management VPC uses VPNs through a customer gateway to connect to a single device in the data center. The Production VPC uses a virtual private gateway with two attached AWS Direct Connect connections. The Management and Production VPCs both use a single VPC peering connection to allow communication between the applications. 

What should a solutions architect do to mitigate any single point of failure in this architecture? 

    A. Add a second set of VPNs to the management VPC from a second customer gateway device
    B. Add a set of VPNs between the Management and Production VPCs
    C. Add a second VPC peering connection between the Management VPC and the production VPC. 
    D. Add a second virtual private gateway and attach it to the Management VPC. 

Answer is A, why?

A is the correct option to mitigate the single point of failure. 
The management VPC currently has a single VPN connection through one customer gateway device. This is a single point of failure. 
Adding a second set of VPN Connections from the Management VPC to a second customer gateway device provides redudancy and eliminates this single point of failure. 

(production) VPN 1 ------> cgw 1 
(Management) VPN 2 ------> cgw 2 

## Glosarium 
   1. what meaning about customer gateway? 
      
   based on documentation https://docs.aws.amazon.com/vpn/latest/s2svpn/your-cgw.html A customer gateway device is a physical or software appliance that you own or manage in your on-premises network (on your side of a Site-to-site VPN Connection)

   2. what meaning virtual private gateway? 
   3. what meaning AWS Direct connect? 
   4. what meaning single VPC peering connection? 


2. A company uses NFS to store large video files in on-premises network attached storage. Each video file ranges in size from 1 MB to 500 GB. The total storage is 70 TB and is no longer growing. The company decides to migrate the video files to Amazon S3. The company must migrate the video files as soon as possible while using the least possible network bandwidth. 

which solution will meet these requirement?

    A. Deploy an S3 File Gateway on premises. Create a public service endpoint to connect to the S3 File Gateway. Create an S3 bucket. Create new NFS file share on the S3 File Gateway. Point the new file share to the S3 bucket. Transfer the data from the existing NFS file share to the S3 File Gateway. 
    B. Create an AWS Snowball Edge job. Receive a Snowball Edge device on premises. Use the Snowball Edge client to transfer data to the device. Return the device so that AWS can import the data into Amazon S3. 
    C. Create an S3 bucket. Create an IAM role that has permissions to write to the S3 bucket. Use the AWS CLI to copy all files locally to the S3 bucket
    D. Set up an AWS Direct Connect connection between the on-premises network and AWS. Deploy an S3 File Gateway on premises. Create a public virtual interface (VIF) to connect to the S3 File Gateway. Create an S3 bucket. Create a new NFS file share on the S3 File Gateway. Point the new file share to the S3 bucket. Transfer the data from the existing NFS file share to the S3 File Gateway. 

Answer is B, why? 
let's analyze this. on a Snowball Edge device you can copy files with a speed of up to 100Gbps. 70TB will take around 5600 seconds, so very quickly, less than 2 hours. The downside is that it'll take between 4-6 working days to receive the device and then another 2-3 working days to send it back and for AWS to move the data onto S3 once it reaches them. Total time: 6-9 working days. Bandwith used:0 

simple analyze 
The key is 
- the total storage is 70 TB and is no longer growing 
- using the least possible network bandwidth
No longer growing mean 1 time migrate, no need file gw 
least possible nw bandwith -->> snowball edge. 


3. A company uses AWS to host its public ecommerce website. The website uses an AWS Global Accelerator accelerator for traffic from the internet. The Global Accelerator accelerator forwards the traffic to an Application Load Balancer (ALB) that is the entry point for an Auto Scalling Group 

The company recently identified a DDoS attack on the website. The Company needs a solution to mitigate future attacks. 

Which Solution will meet these requirement with the LEAST implement effort? 

    A. Configure an AWS Lambda function to read the ALB metrics to block attacks by updating a VPC Netwok ACL 
    B. Configure an Amazon Cloudfront distribution in front of the Gloval Accelerator accelerator 
    C. Configure an AWS WAF web ACL for Global Accelerator accelerator to block traffic by using rate-based rules
    D. Configure an AWS WAF web ACL on the ALB to block traffic by using rate-based rules

Anwer is D, why? 
WAF can be applied on ALB, API gateway or cloud front 
AWS Global Accelerator itself doesn't support AWS WAF   