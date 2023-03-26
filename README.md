# AWS_ApplicationLoadBalancer_Setup_For_MicroServices_Application

#Phase 1 : Create Web Server Pools (Front End, Train, Flight)

1) Create Two EC2 Instance FESVR01 For Frontend Microservice development server 01
Download file FrontEndServer01 and put that bash script into the user data area in the Advance tab

2) Create EC2 Instance FESVR02 For Frontend Microservice development server 02
Use same security group which got created while creating Front End Server 01
Download file FrontEndServer02 and put that bash script in the user data area in the Advance tab

3) Create EC2 Instance TrainSVR01 For Train Microservice development server 01
Use same security group which got created while creating Front End Server 01
Download file TrainServer01 and put that bash script in the user data area in the Advance tab

4) Create EC2 Instance TrainSVR01 For Train Microservice development server 02
Use same security group which got created while creating Front End Server 01
Download file TrainServer02 and put that bash script in the user data area in the Advance tab

5) Create EC2 Instances FlightSVR01 For Flight Microservice development server 01
Use same security group which got created while creating Front End Server 01
Download file FlightServer01 and put that bash script in the user data area in the Advance tab

6) Create EC2 Instances FlightSVR02 For Flight Microservice development server 02
Use same security group which got created while creating Front End Server 01
Download file FlightServer02 and put that bash script in the user data area in the Advance tab

7) Add Inbound Rule in the security group to allow port 80 traffic

Note: You can verify web service is working fine or not by accessing server with its public IP


#Phase 2: Create Load Balancer

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

#Test

Goto Load Balancer "mymsalb01", from general tab copy dns name of the LB
Brouse URL for Front End Web page: <dns name of the LB>\
Brouse URL for Train Web Page: <dns name of the LB>\?vehicle=train
Brouse URL for Flight web page: <dns name of the LB>\?vehicle=flight
