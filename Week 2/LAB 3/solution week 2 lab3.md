aws ec2 run-instances --image-id ami-06eecef118bbf9259 --instance-type t2.micro --subnet-id subnet-0b9cba12e6bd3937d --count 1 --security-group-ids sg-0d7c33d2af33e2f53 --key-name schull-01-key
ssh -i schull-01-key.pem ec2-user@44.192.62.228
yes
sudo yum update -y
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl is-enabled httpd
sudo systemctl stop httpd
BOOSTRAPPING SCRIPT

#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd