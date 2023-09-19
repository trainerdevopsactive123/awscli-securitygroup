# How to create AWS Security group with awscli command 

aws ec2 authorize-security-group-ingress --region ap-south-1 --group-id $(aws ec2 create-security-group --group-name myname_SG_ap-south-1  
--description "Security group description" --vpc-id vpc-03fc5b8a187b5cdc7 --output text --region ap-south-1 
--ip-permissions IpProtocol=tcp,FromPort=80,ToPort=80,IpRanges='[{CidrIp=0.0.0.0/0,Description="HTTP from anywhere"}]' 
IpProtocol=tcp,FromPort=443,ToPort=443,IpRanges='[{CidrIp=0.0.0.0/0,Description="HTTPS from anywhere"}]' 
IpProtocol=tcp,FromPort=22,ToPort=22,IpRanges='[{CidrIp=172.31.0.0/16,Description="SSH from private network"}]' 
IpProtocol=tcp,FromPort=22,ToPort=22,IpRanges='[{CidrIp=203.0.113.25/32,Description="SSH from public IP"}]'


# To delete security group 
aws ec2 delete-security-group --group-id sg-0db93639ae87aa4da

# To delete multiple security group 

#!/bin/bash

security_groups=("sg-04cef8a2f92493d8a" "sg-0b767f673337532c6")

for sg in "${security_groups[@]}"; do
    aws ec2 delete-security-group --group-id "$sg" || echo "Failed to delete security group: $sg"

done




# How to get all the secuirty group 

aws ec2 describe-security-groups

# How to get only require information 

aws ec2 describe-security-groups --query 'SecurityGroups[*].[GroupId, GroupName]' --output text


# attach with EC2 machine

aws ec2 modify-instance-attribute --instance-id i-0972b665eaf3664dc --groups sg-0098ea776ec399ba1	


# attach multiple security group with ec2 machine

aws ec2 modify-instance-attribute --instance-id i-0972b665eaf3664dc --groups sg-0098ea776ec399ba1 sg-0ef0d036201e5ad20











