# AWS_ApplicationLoadBalancer_Setup_For_MicroServices_Application

# Phase 1 : Create Web Servers Pool

1) Create Two EC2 Instances For Frontend Microservice development 
put below script in the user data area in the Advance tab (update server number accordingly)
Use same security group and for Server 02 which got created while creating Front end Server 01
#!/bin/bash
sudo su
yum update -y
yum install httpd -y
cd /var/www/html
echo "Welcome To Microservice App Setup Demo - Server_01" >index.html (echo "<html><h1>Server-01</h1></html>">index.html)
service httpd start
chkconfig httpd on

2) Create Two EC2 Instances For Train Microservice development
put below script in the user data area in the Advance tab (update server number accordingly)
use same security group which got created while creating Front end Server 01
#!/bin/bash
sudo su
yum update -y
yum install httpd -y
cd /var/www/html
echo "<html><h1>Train_Server_01</h1></html>">index.html
service httpd start
chkconfig httpd on

3) Create Two EC2 Instances For Flight Microservice development 
put below script in the user data area in the Advance tab (update server number accordingly)
use same security group which got created while creating Front end Server 01
#!/bin/bash
sudo su
yum update -y
yum install httpd -y
cd /var/www/html
echo "<html><h1>Flight_Server_01</h1></html>">index.html
service httpd start
chkconfig httpd on

4) Add Inbound Rule in the security group for the port 80

Note: You can verify web service is working fine or not by accessing server with its public IP


# Phase 2: Create Load Balancer

Step 1
1) Goto EC2 Dashboard > Load Balancer > Create Load Balancer
2) Select Application Load Balancer > provide LB name "mymsalb01"
3) Select same security group which got created while creating Front end Server 01
4) Select all Availibility Zones
5) Click next

Step 2
6) In the Taeget Group section click on create Target Group
7) create New Target Group
8) Provide Target Group Name "TrainTG" 
9) select Two EC2 Instances created for Train web server pool
10)
11) 
12) Follow 7 - 11 to create "FlightTG"

Step 3
13) Goto Load Balancer Tab > refresh Taeget Group section > select "TrainTG" > Create Load Balancer
Step 4
14) Goto Load Balancer Tab > "mymsalb01" > Listeners > HTTP:80 > rules > Manage Rules > + > Insert Rules
15) Provide these information in the Condition section: key = vehicle value=train
16) Provide these information in the Action section : Go to Target Group=TrainTG
17) Save Rule
18) Click on Insert Rules
19) Provide these information in the Condition section: key = vehicle value=Flight
20) Provide these information in the Action section : Go to Target Group=FlightTG
21) Save Rule


# Test

Goto Load Balancer "mymsalb01", from general tab copy dns name of the LB
Brouse URL for Front End Web page: <dns name of the LB>\
Brouse URL for Train Web Page: <dns name of the LB>\?vehicle=train
Brouse URL for Flight web page: <dns name of the LB>\?vehicle=flight



