To create a VPC with the following: Name: LabVPC, CIDR block 10.0.0.0/
aws ec2 create-vpc --cidr-block 10.0.0.0/16 --tag-specification "ResourceType=vpc,Tags=[{Key=Name,Value=MyVpc}]"
Creation of the first subnet
aws ec2 create-subnet --vpc-id vpc-0b3db92cf45e4a946 --cidr-block 10.0.1.0/24
Creation of the second subnet 
aws ec2 create-subnet --vpc-id vpc-0b3db92cf45e4a946 --cidr-block 10.0.0.0/24
creation of an internet gateway
aws ec2 create-internet-gateway --query InternetGateway.InternetGatewayId --output text
Attaching the created gateway to my created VPC
aws ec2 attach-internet-gateway --vpc-id vpc-0b3db92cf45e4a946 --internet-gateway-id igw-0a956dd0b8e861ebe
Creating a custom route table for my VPC
aws ec2 create-route-table --vpc-id vpc-0b3db92cf45e4a946 --query RouteTable.RouteTableId --output text
Create a route in the route table that points all traffic (0.0.0.0/0) to the internet gateway
aws ec2 create-route --route-table-id rtb-00a040eeb6766c0e5 --destination-cidr-block 0.0.0.0/0 --gateway-id igw-0a956dd0b8e861ebe
to confirm 
aws ec2 describe-route-tables --route-table-id rtb-00a040eeb6766c0e5
getting the subnet IDs of my VPC
aws ec2 describe-subnets --filters "Name=vpc-id,Values=vpc-0b3db92cf45e4a946" --query "Subnets[*].{ID:SubnetId,CIDR:CidrBlock}"
making one of the subnet a public subnet 
aws ec2 associate-route-table  --subnet-id subnet-05b06117682a6fcef --route-table-id rtb-00a040eeb6766c0e5
modifying the behaviour of my public subnet 
aws ec2 modify-subnet-attribute --subnet-id subnet-05b06117682a6fcef --map-public-ip-on-launch