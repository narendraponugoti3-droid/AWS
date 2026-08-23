# ASG 
       Auto Scaling groups automate the scaling of EC2 instances 
       While Creating ASG , you specify the minimum , maximum,and desired instance count 
       So ASG will maintain the desired number of the instances all the time 
       ASG do health check on EC2 to replace unhealthy instance automatically but not only do health check on EC2 
       need to do the health check inside application of ec2  , ALB will do this 
       ASG only do the health check of EC2 instance and ALB do the health check of application inside EC2 as well 
       So ALB health check is better than using the EC2 status check 
  <img width="1191" height="519" alt="image" src="https://github.com/user-attachments/assets/1a3f5337-7abc-4686-ae9b-23c18e5a8053" />

<img width="1065" height="600" alt="image" src="https://github.com/user-attachments/assets/e1f3e254-6bb6-4d76-827f-a61194a3576a" />

ASG Enable by default EC2 health check 
Health check grace period -you can set this health check grace period based on how much time your EC2 instance take 
to fully up and running 
<img width="1136" height="473" alt="image" src="https://github.com/user-attachments/assets/9b7a0305-708e-4830-8ddc-22704fc4f233" />
<img width="1183" height="576" alt="image" src="https://github.com/user-attachments/assets/b0e9888c-cb47-4d2d-8c5b-d6d3511ddd65" />

<img width="1840" height="911" alt="image" src="https://github.com/user-attachments/assets/ceb3be9b-578d-4221-8a29-2bb6afd0115b" />

<img width="1710" height="977" alt="image" src="https://github.com/user-attachments/assets/20cad05c-059f-4165-8249-734243ff7817" />

<img width="1783" height="910" alt="image" src="https://github.com/user-attachments/assets/ef98e361-2bb2-43ed-a42f-e462210aa637" />

### ALB as target of NLB 
If you are accessing the application from your corporate network and your network team or security team wnats that , you know
there should be firewall and all IPs that your client are reaching to should be whitelisted in this firewall 
now if you are using the ALB , you cannot do that becuase ALB will be provide the DNS  
So if that is the use case , you can simply bring the NLB and put this ALB as a target of the NLB and because NLB has the static IP can be whitelisted in this firewall 
<img width="1746" height="858" alt="image" src="https://github.com/user-attachments/assets/bf8b2fa6-3282-4ba7-8346-d451b892389f" />


### Blue / Green Deployment 
<img width="1770" height="926" alt="image" src="https://github.com/user-attachments/assets/a409a0fb-5523-4951-8fc1-37a44133b60c" />


