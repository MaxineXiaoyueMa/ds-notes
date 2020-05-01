# Cheatsheet - aws cli

## EC2 Instances
- start:
`aws ec2 start-instances --instance-ids i-xxxxxxxxxxxxxxxxx`

- stop:
`aws ec2 stop-instances --instance-ids i-xxxxxxxxxxxxxxxxx`

- resize:
`aws opsworks --region us-east-1 update-instance --instance-id dfe18b02-5327-493d-91a4-c5c0c448927f --instance-type c3.xlarge`

## EBS Volumes
- change size:
`aws ec2 modify-volume --size xx(desired size) --volume-id vol-xxxxxxxxxxxxxxxxx`
- change type, size, IOPS
`aws ec2 modify-volume \
    --volume-type io1 \
    --iops 10000 \
    --size 350 \
    --volume-id vol-1234567890abcdef0`
