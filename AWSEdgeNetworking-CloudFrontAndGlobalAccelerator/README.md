
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

# CloudFront Features 
<img width="1830" height="885" alt="image" src="https://github.com/user-attachments/assets/a0c0b5d4-64e4-4882-9ba1-61a7f13bf0a7" />
<img width="1798" height="881" alt="image" src="https://github.com/user-attachments/assets/8d1c0695-ef3d-4ee4-ba0f-47270bad1840" />

<img width="1816" height="938" alt="image" src="https://github.com/user-attachments/assets/c8e4be4f-4780-47b4-86dd-a379ac9b9e7d" />


<img width="1836" height="912" alt="image" src="https://github.com/user-attachments/assets/4e38ffb5-6689-46ca-a456-c56ea1257a7e" />


Cache Invalidations is charging some fess , first 1000 invalidation are free per month and after that you will pay for additional invalidation 


<img width="1841" height="943" alt="image" src="https://github.com/user-attachments/assets/bcc62063-e3ce-4e28-956a-9aff2ffc04cd" />

<img width="1800" height="930" alt="image" src="https://github.com/user-attachments/assets/d00dc27d-0a2d-404f-9c5a-46fb74fc605a" />

<img width="1830" height="936" alt="image" src="https://github.com/user-attachments/assets/9cd30d0e-86b9-4d1e-a09e-383d38a9bd7c" />


# ClodFront Security - AWS WAF and AWS Shield 
we apply the AWS WAF at cloudfront level , all request filtering happens at the edge level and that means your traffic 
never reaches to the origin , there by reducing the load on the origin if WAF identifies that as malicious request 
So Both at the Security level , it protects your origin and also it reduce the load on your origin 

Using CloudFront +WAF+ Shield together provides a multi-layered , global defense against both network layer and application layer threats 
<img width="1134" height="535" alt="image" src="https://github.com/user-attachments/assets/e6868c44-705d-4ac8-88ba-1197e329d6e2" />
<img width="1692" height="909" alt="image" src="https://github.com/user-attachments/assets/8319bbac-d371-42fc-9a46-fc137e344c5e" />
