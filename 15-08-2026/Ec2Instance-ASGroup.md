
# AWS EC2 Instance AS roup 

Step1 : Create a EC2 instance with Test
<img width="885" height="277" alt="image" src="https://github.com/user-attachments/assets/60f545e8-404b-40fd-944d-43077bbef30c" />


3/3 checks passed 
 System status Check : verify te health of underlying AWS infra (power , HW and NW) 
 Instance Status :  OS is healthy or not --high CPU usage, kernel  panic, boot failure 
 EBS Status : 
 
 need to restart the VM to resolve this issue ,if not fix 

# Placement Group : we can place the VMs closer ( single hardware , singe rack 
            I have a single App , I should put all VM into single place ( one physical server , one rock , one server ) to communicate 
            easily all applications 
   1.Cluster  
              all VM should put one place and configure , this is called cluster configure 
             Advantages : 
                      -  Low netwrok latency 
                      -  Highest through put 
                      -  best performance 
                            1. rack failure 
                            2. hardware failure 
SIngle Application , Single cluster lo place cheste incase rack failure or hardware failure , your entire application will go down 
This is singlepoint of failure 

<img width="521" height="272" alt="image" src="https://github.com/user-attachments/assets/5fa71c52-913d-46db-8bde-9136f37075af" />

VMs should be part of ifferent racks and different hardwares 
2. Spread Placement group 


3. Partition Placement Group
    I have 3 rack and place my all VMs regarding Frontend and backend and DB place into single rack with single hardware 
<img width="954" height="281" alt="image" src="https://github.com/user-attachments/assets/c846369a-4805-49b7-964a-0cb7e60e26cb" />

| Placement Group | Same AZ? | Multiple AZs?                 |
| --------------- | -------- | ----------------------------- |
| **Cluster**     | ✅ Yes    | ❌ No                          |
| **Spread**      | ✅ Yes    | ✅ Yes, within the same Region |
| **Partition**   | ✅ Yes    | ✅ Yes, within the same Region |

The key point to remember

Cluster = one AZ only
Spread = can span multiple AZs
Partition = can span multiple AZs

<img width="1282" height="844" alt="image" src="https://github.com/user-attachments/assets/72da4c5f-4afb-4940-a262-eb373149e9da" />

<img width="786" height="527" alt="image" src="https://github.com/user-attachments/assets/b8609cbf-12e4-4f2b-96b7-aed94201349e" />

AWS Console --> EC2 --> Placement group --> Create Placement group 
<img width="1448" height="499" alt="image" src="https://github.com/user-attachments/assets/4c64812f-e420-437e-91c5-2fc67b66ec8a" />

First Created the Placement Group , Then Create the EC2 instance 
while create the EC2 instance , it showing the advance setting  
Placement Group : Select the placement group 
Target Partition: 
then launch EC2 instance and then create the one more ec2 instance with same placement group and target partition 
Then Create 2 More VM with placement group with different partitions 


# AWS AutoScaling Groups 
<img width="1051" height="372" alt="image" src="https://github.com/user-attachments/assets/7ea8ca8e-1fbc-441d-a37f-0168cc62b925" />


Launch Instance --GrwoApplication  ( Connect to VM via CMD ,install apache2 , cd var/www/html , vi index.html , remove the existing 
content then paste new html website here then save it ) 
Create an AMI ( Select VM and Clicks Action --> Image and templates --Create image 
Create Launch template  ( Auto Scaling  --> Launch Configuration )
Create an auto scaling group  (
attach Load Balancer 
Auto scaling 

<img width="1565" height="601" alt="image" src="https://github.com/user-attachments/assets/c9ff0740-3cb3-4037-9ee8-7e3001c30878" />




Create the Auto Scale and then review it 

connect to main VM --- then Connec to another VM with private IP 
top command to see the utilization 
now incease the load 
$ yes > /dev/null &    // spike the cpu 
$ top 
