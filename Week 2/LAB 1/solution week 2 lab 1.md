launch an instance
aws ec2 run-instances --image-id ami-06eecef118bbf9259  --instance-type t2.micro --subnet-id subnet-05b06117682a6fcef --count 1 --key-name schull-01-key
Allow connection to port 80
aws ec2 authorize-security-group-ingress --group-id sg-037cca46a16517bb6 --protocol tcp --port 80 --cidr 10.0.0.0/0
Allow connection to port 22
aws ec2 authorize-security-group-ingress --group-id sg-037cca46a16517bb6 --protocol tcp --port 22 --cidr 10.0.0.0/0  
To connect to my instance 
Open powershell
In the directory where my key pair is saved i type
ssh -i schull-01-key.pem ec2-user@3.235.40.18
To update my instance
sudo yum update -y
To install Apache server
sudo yum install httpd -y
To start Apache 
sudo systemctl start httpd
To enable Apache
sudo systemctl enable httpd
To view my server in action 
Type 3.235.40.188 in a web browser