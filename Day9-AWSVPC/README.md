# AWS VPC 
<img width="1082" height="458" alt="image" src="https://github.com/user-attachments/assets/1652814e-4b55-41cb-b323-34e3c63b8d39" />


<img width="1284" height="566" alt="image" src="https://github.com/user-attachments/assets/ef328abd-3ca5-4f2b-a788-c2610039c7a5" />


Step1 : Create VPC with 3 public subnet and 3 private subnet with different AZ (3 AZ) and no NATGateway and no VPC Endpoint 
           Any VM in Private subnet  is not exposing the internet 
           VMs in public subnet are getting internet using IG 
<img width="1403" height="568" alt="image" src="https://github.com/user-attachments/assets/4273442a-652a-4b23-922f-bff33b473429" />

SSh Key : Public Key and Private Key , Server keeps the Public key and user keeps the private key and we can access the server using 
private key 
        SSH -i grokey.pem ubuntu@public-ip-address 

  ### Network Setting 
  VPC : select your vpc
  subnent: select public subnet
  auto-assignpublic ip: Enable 
  Firewall(SecurityGroup) : opnen ssh / http

  Create VM , Create EC2 instance with public IP 
  Connect VM : ssh -i growkey.pem ubuntu@public-ip-address 
  Connected VM : apt update \ apt apache2 -y \ cd var/www/html \ vi index.html  
  Remove existing content in index.html then copy here your content 

you did it like below diagram 
<img width="1396" height="518" alt="image" src="https://github.com/user-attachments/assets/e6f787e1-c833-4d08-9d23-10b7059f7d73" />


# Day10 AWS VPC Part 2
<img width="1205" height="697" alt="image" src="https://github.com/user-attachments/assets/c824fc39-d75b-476a-9d74-8531b3c8c8aa" />



Step1 : Create VPC with 2 AZ and 2 public subnet and 2 private subnet and  Regional-New NAT gateway (one NAT is across multiple AZ)
Step2 : Create EC2(publicVM1) with network ( vpc , public subnet1) and SG open ssh port 
Step3 : Create EC2 (privateVM1) with Network ( VPC , Private Subent1 ) and SG Open SSH Port 
Step4 : Create EC2(PrivateVM2) with Network(VPB , Private subnet2) and Open SSH port 
<img width="1400" height="414" alt="image" src="https://github.com/user-attachments/assets/99d06d11-08a9-491e-a222-a82b29ac8855" />

Connect to PublicVM1  : ssh -i growkey.pem ubuntu@public-ip-address 
How to Connect the PrivateVM1 
Copy the growkey.pem into publicVM1 
SCP -i growkey.pem growkey.pem(copy file) ubuntu@public-ip-address:/tmp/
lets verify it 
Connected to PublicVM1 : cd /tmp 
 ssh -i growkey.pem ubuntu@private-ip-address 
 to verify that VM is connect to internet or not 
  $ ping google.com 
  $curl ifconfig.me 

  One more method to copy the file ; winscp 
 Verify it ,  NAT gate is attached the Private Route table or not 
 Then Connected to PublicVM1 
 Then Connect to privateVM1 
 Then verify it , $ping google.com $ curl ifconfing.me


Then Connect to PublicVM1 and install apache2 and cd /var/www/html and vi index.html 
Then Open the Port for Http on SG 
Then Access : http://public-ip-address 


Click Network NACL : edit inbound rules and block the http 
<img width="1627" height="411" alt="image" src="https://github.com/user-attachments/assets/fa67d6a6-8667-4609-bb26-63f164cb6760" />
Then Access : http://public-ip-address  , we cannot access it 
NACL : anything block at VPC or subnet level 
SG : VMs 

# Day11 AWS VPC Peering 
<img width="1078" height="639" alt="image" src="https://github.com/user-attachments/assets/7b466757-edf2-4f83-9bd4-25d131e329af" />

 ### PVC Peering 

<img width="1347" height="637" alt="image" src="https://github.com/user-attachments/assets/a13628f8-4f97-4d69-937d-f102b96b0ec0" />

Step1 :Mumbai Region - Create VPC with 1 AZ and 1 public subnet and 1 private subnet and regional NAT gateway 
Step2 : Hyd Region - Create VPC with 1 AZ and 1 public subnet and 1 private subnet and regional NAT gateway 
Step3 : Create public VMs with Networking Setting (VPC Mumbai vpc, public subnent ) and newkeys  and enable public Ip and SG open SSH port 
and Ping enable with All ICMP port 
Step4 : Create privateVM with mumbia VPC and private subnent and select exist SG and keys 
Step5 : repeat step3 but changes - network setting ( hyd vpc , public subnent) and create new key pair 
Step6 : Repeat step4 with network setting (hyd VPC private subnet ) 
<img width="1102" height="218" alt="image" src="https://github.com/user-attachments/assets/2d02a272-a679-481c-a684-eba33a104a6e" />
<img width="971" height="214" alt="image" src="https://github.com/user-attachments/assets/cf3e7b5e-eb5b-459e-9c73-04b200e26aeb" />

Connect to publicVM : ssh -i key.pem ubuntu@public-ip-address 
$ping private-ip-address 

VPC Peering 
Go to VPC --> Peering Connection --> Create Peering connection 
<img width="1344" height="671" alt="image" src="https://github.com/user-attachments/assets/ad5fea9a-6a35-40ac-aa52-9a7093cbd494" />
Create Peering COnnection 
Now Accept my peering connection 
Go to another region --> Peering Connection 
<img width="1659" height="275" alt="image" src="https://github.com/user-attachments/assets/f57590e6-b9bd-4291-9ebd-5aba09edbae4" />


<img width="1320" height="677" alt="image" src="https://github.com/user-attachments/assets/ee2a6fff-fa10-41cf-8dd2-6bbfb1e3891a" />

Destination : Yavaritho communication cheyali 
Target : how to communicate , need medium 
Route table :  
<img width="1621" height="540" alt="image" src="https://github.com/user-attachments/assets/e2b3d58d-9856-4334-a36a-9c8591620346" />
<img width="1549" height="593" alt="image" src="https://github.com/user-attachments/assets/4a06a64b-6c0c-43e6-a309-b2c33ddd2530" />
<img width="1544" height="485" alt="image" src="https://github.com/user-attachments/assets/77d977cf-b27d-45dc-926b-1dffe6f102fe" />

This is Final Demo Diagram 
<img width="1419" height="756" alt="image" src="https://github.com/user-attachments/assets/7109df54-64fa-4d7f-ae9a-23252c386750" />
<img width="1238" height="676" alt="image" src="https://github.com/user-attachments/assets/594562d1-9c1c-4dba-90c3-fc224ea7e003" />
