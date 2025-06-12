
## In office Hands on

![Screenshot 2025-06-11 121439](https://github.com/user-attachments/assets/838f110a-3c77-40cb-908a-6b4d9df206ee)
-- > Go to the EC2 Dashboard and create a new key pair named day-one-Yashwanth-kp.
Select RSA as the key type and choose the .pem file format so we can use it for SSH access later.
After the key pair is created, download the .pem file and make sure to store it safely Locally on your computer
  
![Screenshot 2025-06-11 122425](https://github.com/user-attachments/assets/a9d565de-f166-4127-80a2-ba2df6d1984a)

--> Next, go to the VPC Dashboard and create a new VPC by selecting the "VPC only".
Giving the name like day-one-yashwanth-VPC and set the IPv4 CIDR block to 10.0.0.0/16. This gives us around 65,000 IP addresses.
If we don’t need that many, we can also use something like 10.0.0.0/24, which gives 256 IP addresses we can choose the range based on our needs. Once done, we can go ahead and create the VPC
After creating the VPC, create a subnet inside it.
we Name it day-one-yashwanth-subnet and use the CIDR block 10.0.1.0/24, which gives around 256 IP addresses.
Then we just hit create for finish setting up the subnet.
![Screenshot 2025-06-11 122425](https://github.com/user-attachments/assets/051857cd-b1c9-45fa-8269-1211041380f0)
-->Now,we create an Internet Gateway which allows our resources inside the VPC to connect to the internet.
we name it day-one-yashwanth-igw and once it's created attach it to our VPC (day-one-yashwanth-VPC).
-->Next we create a Route Table and name it day-one-yashwanth-RT.
A route table which helps direct traffic within our VPC and between subnets.
While we setting it up edit the routes and adding a destination (0.0.0.0/0) which means traffic to anywhere on the internet.
For the target we select the Internet Gateway we just created (day-one-yashwanth-igw).
To make a subnet public we need to associate the subnet with this route table.
Once connected then the subnet will be able to communicate with the internet which meaning it’s now a public subnet.
![Screenshot 2025-06-11 122711](https://github.com/user-attachments/assets/237e3e92-56da-4a50-a63b-a7b4776f0041)
--> Next we go to the Security Groups section to create a new one.
wen name it day-one-yashwanth-SG and make sure to attach it to the VPC we created earlier (day-one-yashwanth-VPC).
A security group which it acts like a virtual firewall it controls what kind of traffic can reach our instance.
Now, we’ll add inbound rules, which define what incoming traffic should be allowed
SSH (port 22) This allows us to connect to our EC2 instance from our computer using the .pem key. Set the source to "My IP" if we want to restrict access to our system or 0.0.0.0/0 if you want access from anywhere.
HTTP (port 80) This allows web traffic which people can access it from the internet.
And set the source to 0.0.0.0/0 which means it will accept traffic from any IPv4 address.
Once these rules are added create the security group.
![Screenshot 2025-06-11 123331](https://github.com/user-attachments/assets/96085f54-a3b1-4c28-8d7b-3332a23616e9)

-->Now to launch our EC2 instance. we start by creating a new instance and giving it a name like day-one-yashwanth-ec2.
For the AMI (Amazon Machine Image),we select Amazon Linux AMI.Instance type is t2.micro AMI ID :"ami-0b09627181c8d5778"
Under the Key pair, we select the one we created earlier day-one-yashwanth-kp. This will be used for secure SSH access.
By default, the instance might be attached to the default VPC. Make sure to change the network setting and select the VPC we created earlier day-one-yashwanth-VPC.
Then we choose the subnet we created (day-one-yashwanth-subnet) and make sure auto-assign public IP is enabled so the instance gets internet access.
under security group settings choose the security group we created earlier day-one-yashwanth-SG.

![image](https://github.com/user-attachments/assets/387f949b-8cab-492f-bedf-d32b6f9b7096)
in the Advanced setting we give our basic Script #!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
and by clicking the launch intance the instance will be launched after launching the instance we get an public IP with that public IP we can open our site .
![Screenshot 2025-06-11 133238](https://github.com/user-attachments/assets/104de878-1d5b-41e4-bb41-e3c26f109e3a)





