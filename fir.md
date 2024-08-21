## Private cloud/subnet communicate through internet with the help of a public cloud/subnet that helps with communication internet gateway and router table that helps for forward traffic and that Steps need to be created.##

AWS console 
1. Create a vpc 
1. Name – Tushar patil 
2. CIDR – 10.0.0.0/243
First need the create a vpc for the next process 

2. Create a public subnet (public)
1.	Select vpc 
2.	Name : - Tushar-public-subnet
3.	Subnet CIDR range  10.0.0.0/25
4.	Create subnet
Without vpc you can’t create a subnet for a create subnet to need vpc and CIDR range is randomly /25 for a 125 IP provide and other /25 125 ip provide total ip 250 and other is reserved ip 
Allocated to public
Public subnet for there is instance will be running  

3. Create private subnet (private)
1.	Select vpc
2.	Name: - Tushar-Private-subnet 
3.	Subnet CIDR range 10.0.0.128/25
4.	Create subnet
Private subnet there is not instance will be running 

4. Make public subnet as a public
1.	Select public subnet   edit subnet setting 
2.	Enable auto assign public IPV4 address
public subnet is one that's set up to allow resources within it to be accessible from the internet.



5. Create internet gateway 2 attach to vpc
1.	Provide IGW name & create
2.	Select IGW  action  attach vpc 

Create a route table name is public route table 
6. Provide internet access to public subnet
1.	Select default/public route table  (Tushar-vpc)
2.	Edit route  add rule  IGW
3.	Select your IGW
For the internet access that directly 

7. Associate public subnet is main/public R.T
1.	Go main route table
2.	Select subnet association 
3.	Edit subnet association
4.	Select public subnet
5.	Save

8. Create a 2 instance in public & private
1.	Select same key for both instance 
2.	Network setting while creating instance 
3.	Select your created vpc (Tushar-vpc)
4.	Select subnet according (public/private)
5.	Create instance

Go on CLI 
All the steps for check traffic it working or not in ec2-instance
9. Create public subnet instance 
1.	Check incoming traffic using /Cmd: - ssh -i
2.	Check outgoing traffic /cmd: - ping www.google.com
To check the internet traffic its working or not


10. Connect private instance throw public subnet instance
1.	Take instance key used while creating instance
2.	Create file in public subnet instance
3.	Cmd: - vim key.pem
4.	Give permission 400 /cmd: - chmod 400 key.pem
5.	Access private instance /cmd: -ssh -I key.pem ubuntu@privateIP
For a change permission that assign the private instance using command   

11. Check using ping command 
1.	Can private subnet instance can able to access internet or not
2.	Cmd: - ping www.google.com 
Check the traffic working or not in private instance 

Aws console 
All the steps for internet access assign to the private instance  
12. To provide internet access to private subnet
1.	Create NAT gateway (Tushar-NGW)
2.	Select public subnet 
3.	Allocate elastic ip
4.	Create NAT gateway

13. attach NAT gateway to sub route table
1.	Create sub route table 
2.	Select main route table
3.	Create sub route table

14. select sub route table 
1.	Use (6) number step (private)
2.	Select NAT gateway
3.	Use (7) number step (private) subnet

