# ASG 
  Auto Scaling groups automate the scaling of EC2 instances 
  While Creating ASG , you specify the minimum , maximum,and desired instance count 
  So ASG will maintain the desired number of the instances all the time 
  ASG do health check on EC2 to replace unhealthy instance automatically but not only do health check on EC2 
  need to do the health check inside application of ec2  , ALB will do this 
  ASG only do the health check of EC2 instance and ALB do the health check of application inside EC2 as well 
  So ALB health check is better than using the EC2 status check 
  <img width="1191" height="519" alt="image" src="https://github.com/user-attachments/assets/1a3f5337-7abc-4686-ae9b-23c18e5a8053" />

<img width="1095" height="560" alt="image" src="https://github.com/user-attachments/assets/64eecb48-6111-4f4a-9bcf-a078ebd06783" />
