

 ELB : load balancer which distributes the incoming traffic across this web server 
 ASG : which is responsible for scaling the number of EC2 instances as per different criteria 
 ELB and ASG are more related to high availability and Scalability 

 Scaling : 
          1. Vertical Scaling 
          2. Harizontal Scaling 

# Elastic Load Balancer 
<img width="1725" height="900" alt="image" src="https://github.com/user-attachments/assets/6a81ae41-8097-4a57-8ae9-ca9fbfd31094" />

<img width="1809" height="925" alt="image" src="https://github.com/user-attachments/assets/75c49709-f3ca-4683-a9bc-49016e200c23" />

### Security Group 

 <img width="1184" height="601" alt="image" src="https://github.com/user-attachments/assets/5b1ae196-d7e3-433b-b11c-5af14b006b43" />

In Soruce : Select security group of ALB 

## Types of ELB 
<img width="1214" height="597" alt="image" src="https://github.com/user-attachments/assets/26f61709-48b7-482f-8af9-d27e3bbbc903" />

### OSI Network Layers 
Layer3 -Network -IP Layer is used for routing the traffic that means it tells where to send the packet 
Layer4-Transport - TCP/UDP which are actually responsible for transmitting the packet from source to destination 
                   TCP is connection Oriented where it can also valitate whether you have received all packets or not 
                   and UDP is connectionless 
                   TCP/UDP are responsible for actually sending the packet from source to destination 
                   Then if you want to secure this communication , then you will use SSL and TLS security layer (Session,                        Presentation layers 5,6 layers )on top of this transport layer 
Application Layer 7 -HTTP/HTTPS/HTTP/2,gRPC - where you represent that data , their data is already transported but 
                      you have to present that so that the end user or application can understand that data 



  <img width="1822" height="1026" alt="image" src="https://github.com/user-attachments/assets/d1e86500-4c2c-4c5e-89c0-5f740323a632" />

                   
