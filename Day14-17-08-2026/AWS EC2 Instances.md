
# AWS Virtual Machines 
EC2 Instance : Elastic Compute cloud , Servers in the cloud 
<img width="987" height="290" alt="image" src="https://github.com/user-attachments/assets/eb96127b-1d55-4bbd-93c6-beb674575532" />
<img width="1059" height="364" alt="image" src="https://github.com/user-attachments/assets/5f594099-9bbc-434e-acbc-b7910a2cdc11" />
<img width="1039" height="261" alt="image" src="https://github.com/user-attachments/assets/011ace33-85d4-4240-998d-db9342acb909" />

### Savings Plan 
its modern approach for reserved instances 
<img width="1082" height="218" alt="image" src="https://github.com/user-attachments/assets/a98903e2-681e-4a2b-9bb9-e72f2f54d12b" />


<img width="988" height="131" alt="image" src="https://github.com/user-attachments/assets/7f6e3541-2a37-4458-8840-d824a6c46fc8" />

### Do this in AWS 
<img width="1030" height="557" alt="image" src="https://github.com/user-attachments/assets/4dd85e73-d2c3-4975-8504-4d1a0f4cd39f" />


Login in AWS Console --> Region Hyd ---> VPC 
Create a VPC with More 
Auto-generated : Grwo
Ipv4CIDR Block: 10.0.0.0/16 
Tenancy: Default 
Number of AZ : 2 
   first availability zone: 2a , 2b 
   number of public subnets: 2 
   customize subnets CIDR blocks :

NAT gateway :None 
VPC endPoint: None 

Create VPC 

Then Go to EC2 Instance -- Click Reserved Instance -- it is showing the purchase reserved instance 
<img width="1307" height="583" alt="image" src="https://github.com/user-attachments/assets/7ba9f0de-afd0-4c6b-b2d5-d5d27aed609b" />


Then Create an Instances:Grow2a with VPC along with subnets and open the port ssh and http for security group and enable public IP Address 
Then Create an Instances :Grow2b with VPC along with subnets and open the port ssh and http for security group 

Then Connect to VM:Grow2a and then install apache2 then update the index.html file (cd /var/wwww/html)
Then Repeat same steps of grow2a on grow2b VM 

Then Create the Load balancer 
Create Load Balancer --Application Load balancer (ALB --HTTP/HTTPS) 
Basic Configuration: 
       Load Balancer Name: GrowLB 
       Scheme: internent-facing 
       Load balancer IP Address type: Ipv4 (Dualstack ,dualstack without public Ipv4)
Network mapping : 
        VPC: 
        AZandSubnet: select both subent 
        Security Group : 
Listeners and routing : 
    Listener HTTP:80 
         Protocol: HTTP       Port :80 
    Default action: 
       routing action: 
          forward to target group       Redirect to URL          Return fixed response 
          Create target group 

<img width="1541" height="261" alt="image" src="https://github.com/user-attachments/assets/ccfa10be-f38c-40ea-b06c-04e4b2c63678" />

Click Create target group 
Create target Group :
           Settings:
              target type: Instances 
  Click Next 
   Register targets -- Add targets 
   Create a target group 
Then Create A Load Balancer Then we will get a DNS name and check it 

| Feature         | Savings Plan                       | Reserved Instance          |
| --------------- | ---------------------------------- | -------------------------- |
| Commitment      | $/hour of compute usage            | Specific EC2 configuration |
| Term            | 1 or 3 years                       | 1 or 3 years               |
| Discount        | Up to 72%, depending on plan       | Up to 72%, depending on RI |
| Flexibility     | **Higher**                         | Lower                      |
| Instance family | Depends on plan                    | Generally specific         |
| Region          | Compute SP can move across Regions | Generally tied to Region   |
| Instance size   | Flexible                           | More restrictive           |
| EC2             | ✅                                  | ✅                          |
| Fargate/Lambda  | Compute SP can apply               | ❌                          |
| Best for        | Changing workloads                 | Very stable workloads      |

Interview question

Q: Which would you choose for a production application whose EC2 instance type may change in the future?

Answer: Usually Savings Plan, especially a Compute Savings Plan, because it provides greater flexibility than an EC2 Reserved Instance. AWS itself currently recommends Savings Plans over Reserved Instances for most EC2 workloads



EC2 Instance scope is global or regional : regional service 
