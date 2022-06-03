launch an instance
aws ec2 run-instances --image-id ami-06eecef118bbf9259  --instance-type t2.micro --subnet-id subnet-05b06117682a6fcef --count 1 --key-name schull-01-key
connect to the instance
ssh -i schull-01-key.pem ec2-user@3.238.26.247
exit the instance
exit
describe AMI
aws ec2 describe-images --region us-east-1 --image-ids ami-06eecef118bbf9259
to describe the status of an instance
aws ec2 describe-instance-status --instance-id i-0bd218c8b11c3faa5
to stop an instance
aws ec2 stop-instances --instance-ids i-0bd218c8b11c3faa5
to start an instance
aws ec2 start-instances --instance-ids i-0bd218c8b11c3faa5
To delete a key pair 
aws ec2 delete-key-pair --key-name raphael_key
To delete a security group
aws ec2 delete-security-group --group-id sg-903004f8