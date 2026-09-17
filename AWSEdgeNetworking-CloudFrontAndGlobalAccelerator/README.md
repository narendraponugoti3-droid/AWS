
# AWSEdgeNetworking-CloudFrontAndGlobalAccelerator

AWS Edge Networking : Access applicaions with lowest latency across the globe 
AWS edge network solves by routing the traffic through AWS edge network 
if you use aws edge network , then this traffic may go through something like this means 
which means most of the traffic flow over through AWS backbone network 
<img width="1218" height="640" alt="image" src="https://github.com/user-attachments/assets/78791352-700d-41da-ac93-3f05523f97aa" />


``` text
AWS Edge Networking : Access application with lowest latency across the globe

if you use AWS edge Network then this traffic may go something like which means most of the traffic flow over through AWS backbone network

with out AWS Edge network , there will be a lot of network hops and that's where latency is not really predictable or consistent 
But if you go AWS edge network then only the traffic from end user to the nearest
 AWS edge location will go over the intrnent and rest of the traffic will be routed through AWS backbone network

So which means AWS edge location provide the consistent and low latency 
```
# AWS CloudFront 
CF can delivery this content over the low latency network and also it can cache the content in the nearest edge location of the user 
and thats where CF improves the end user exprerince 

Advantage of CF is that it reduces the load on your origin servers 

<img width="1802" height="871" alt="image" src="https://github.com/user-attachments/assets/d42b482f-3692-4590-827e-4e1d90514ae1" />
<img width="1720" height="849" alt="image" src="https://github.com/user-attachments/assets/b59d6822-76d3-491d-a27c-939a72916a87" />

<img width="1870" height="897" alt="image" src="https://github.com/user-attachments/assets/42b23e69-5f32-4fe3-978a-8a28fe3cf74c" />
ClodFront , the most importent component is the cloudfront distribute and in the distribution ,
you will then define the origin which means where exactly your application is hosted 

Now end user will make the request to the cloudFront DNS , which will basically takes that request to the nearest 
Edge Location and form there , as you have configured the origin as the application load balancer
this traffic will go from the cloud front edge location to this load balancer over the AWS backbone network 

and the Origin 
Distribution is all about configuring which origins are there , how to route the traffic , wheather to enable specific security features 
Origin server means where exactly your application is hosted 


<img width="1850" height="934" alt="image" src="https://github.com/user-attachments/assets/3f01ce91-e6a9-4bee-b913-8e5ed5515898" />

<img width="1823" height="726" alt="image" src="https://github.com/user-attachments/assets/cf615ed0-375d-4009-9335-08b2b68e7562" />



# CloudFront Origin 
if we use cloudFront in front of S3 bucket and delivery that content through the CloudFront 
The Data Transfer out cost could be as low as 1cent per GB And on top of that ,there is 1 terabytes of free data
transfer out per month 

<img width="1743" height="938" alt="image" src="https://github.com/user-attachments/assets/b309077b-d0e4-4e9c-ae7a-8d4d9f384693" />

<img width="1870" height="880" alt="image" src="https://github.com/user-attachments/assets/8cd8c3d0-a6f4-4be4-a4fa-e2fa248e55bf" />


<img width="1792" height="839" alt="image" src="https://github.com/user-attachments/assets/f89e3f8f-33df-4296-a6cd-41231b8b4d7c" />


``` text

in AWS --> CloudFront --> Distribution --> Create a Distribution 
Select Free Pricing plan 
Distribution Options :
    Distribution Name: narendra 
	Distribution type: single website or app 

Click NEXT 
Origin Type : Amazon S3 
Origin : 
  S3 Origin : choose S3 bucket 
  
Settings: 
 Allow private S3 bucket access to cloudfront 
 Origin setting : 

Clikc Next 
Click NEXT 
Create a Distribution
```
CloudFront Allow the HTTP and HTTPS Connection 
in AWS --> CLick Project of CloudFront Distribution
Click Behaviors --EDIT --> viewer protocol policy 
<img width="464" height="120" alt="image" src="https://github.com/user-attachments/assets/5f2d6490-a4d4-4c45-827c-afbff017c0eb" />


you can also control how CloudFront connect to Origin 
<img width="1846" height="924" alt="image" src="https://github.com/user-attachments/assets/ea1fe7ef-a33a-4c3a-9e4d-298c072dfc4f" />


# Mutual TLS (mTLS) 
CloudFront support mutual TLS menas CloudFront validate the client certificates ,weather legimate users and having the legitimate certificate 
<img width="1895" height="904" alt="image" src="https://github.com/user-attachments/assets/8821af2f-7762-4a0b-a346-a75e9bbdfa2a" />


<img width="1862" height="877" alt="image" src="https://github.com/user-attachments/assets/cc953cf7-ff13-4958-beba-48780ba7da93" />

<img width="1765" height="907" alt="image" src="https://github.com/user-attachments/assets/6a979aef-1452-4ff1-8006-711094aca96e" />

<img width="1685" height="804" alt="image" src="https://github.com/user-attachments/assets/010daa7c-7fea-4eed-9021-ccd2972d21c9" />
