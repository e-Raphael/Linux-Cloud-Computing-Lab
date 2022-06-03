first let's create a key pair
aws ec2 create-key-pair --key-name schull-key --query "KeyMaterial" --output text > MyKeyPair.pem
creating security group 
aws ec2 create-security-group --group-name schullSG --description "Security group for schull " --vpc-id vpc-0b3db92cf45e4a946
allowing port 80
aws ec2 authorize-security-group-ingress --group-id sg-0589a8c4b8c1357e8 --protocol tcp --port 80 --cidr 0.0.0.0/0
allowing port 22
aws ec2 authorize-security-group-ingress --group-id sg-0589a8c4b8c1357e8 --protocol tcp --port 22 --cidr 0.0.0.0/0

run the instance
aws ec2 run-instances --image-id ami-08191defa0d4a23af --count 1 --instance-type t2.micro --key-name schull-key --security-group-ids sg-0589a8c4b8c1357e8 --subnet-id subnet-05b06117682a6fcef
Adding a tag to my instance 
aws ec2 create-tags --resources i-0c419ead498dc0922 --tags Key=Name,Value=ProdCafeServer
Modifying the behaviour of my subnet
aws ec2 modify-subnet-attribute --subnet-id subnet-05b06117682a6fcef --map-public-ip-on-launch
