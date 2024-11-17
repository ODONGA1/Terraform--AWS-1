Simple AWS infrastructure deployment with Terraform by ODONGA1
You can download and reuse the code as you please, 
Pull requests also allowed. 
Contact me if any support needed, thank you


                 +-----------------------+
                 |   AWS VPC (10.0.0.0/16) |
                 +-----------+-----------+
                             |
               +-------------+-------------+
               |                           |
     +---------------------+     +-------------------------+
     | Internet Gateway (GW) |     |     Public Subnet (10.0.1.0/24) |
     +---------------------+     +-------------------------+
               |                           |
               |                   +-------+---------+
     +----------------+           |   Web Server    |
     | Route Table    |           | (EC2 Instance)  |
     | (0.0.0.0/0, ::/0) |<--------|   10.0.1.50     |
     +----------------+           +-----------------+
               |                         |
    +------------------------+    +----------------------+
    | Security Group (Port 22,|    | Elastic IP (Public)  |
    | 80, 443)                |    |   Public IP          |
    +------------------------+    +----------------------+


# This Terraform configuration creates a VPC, internet gateway, route table, subnet, security group, network interface, and an EC2 instance with Apache web server installed.
#
# The VPC has a CIDR block of 10.0.0.0/16 and is tagged as "production".
#
# The internet gateway is attached to the VPC, and the custom route table is created with a route for all traffic (0.0.0.0/0) to go through the internet gateway.
#
# A public subnet is created in the VPC with a CIDR block of 10.0.1.0/24 and is associated with the custom route table.
#
# A security group is created to allow inbound traffic on ports 22 (SSH), 80 (HTTP), and 443 (HTTPS) from any IP address (0.0.0.0/0).
#
# A network interface is created in the public subnet with a private IP address of 10.0.1.50 and is associated with the security group.
#
# An Elastic IP is assigned to the network interface, and an EC2 instance is created in the public subnet. The instance has an AMI of "ami-012967cc5a8c9f891" (Ubuntu 20.04) and is of type "t2.micro".
#
# The user data script for the EC2 instance updates all installed packages, installs Apache (httpd) and mod_ssl, starts the Apache service, enables it to start on boot, and creates a simple index.html file.
#
# Finally, the configuration outputs the public IP address, private IP address, and instance ID of the created EC2 instance.


