# How to set up new AWS EC2 instance

## instance 
0. Create account

1. Log into AWS account (as Administrator):

2. Pick and launch an EC2 instance:
    1. "EC2" -> "Instances" -> "Launch" -> "Choose AMI: Ubuntu" ->
    "Choose an Instance Type: t2.micro" -> "Review and launch" ->
    "Select an existing key pair" -> "Launch" -> "View instances"
    2. ssh into the remote instance:
    check keypair is private:
        - `chmod 400 ~/path/to/xx.pem` (permission: owner can read, that's it)
        - `ssh [-i identity_file] [-J [user@]host[:port]] [-L address]`
        - `ssh -i "xx.pem" ec2-user@ec2-34-212-232-179.us-west-2.compute.amazonaws.com`
        - `ssh -i ~/path/to/xx.pem ubuntu@ec2-00-00-00-000.us-west-2.compute.amazonaws.com`
    3. set up environment:
         - `pip install packages`
    4. set up virtual environment:
         1. `python3 -m venv .venv`
         1. `source .venv/bin/activate`
         - `pip freeze > requirements.txt`
    5. to recreate the environment:
         - `pip install -r requirements.txt`

EBS volume monitoring
1. check available space (after ssh into remote):
    - `df --output=source, pcent /dev/nvme0n1p1`
    - `df -hT /dev/nvme0n1p1`
2. where it is mounted: / (indicating the root)

## start working flow:
1. start instances:
  `aws ec2 start-instances --instance-ids i-0000000000000000`

2. Get instance public DNS:
  `aws ec2 describe-instances | grep DNS --output table`

3. ssh into instance:
  `ssh -i ~/path/to/xx.pem ubuntu@ec2-00-00-00-000.us-west-2.compute.amazonaws.com`

4. activate virtual environment:
  `source .venv/bin/activate`
5. check volume usage: `df -hT /dev/nvme0n1p1`

4. start jupyter with no browser:
  `jupyter notebook --no-browser`

5. forward port where jupyter is served to local port:
  `ssh -N -f -L localhost:8889:localhost:8888 ubuntu@ec2-00-00-00-000.us-west-2.compute.amazonaws.com`

6. stop instance:
  `aws ec2 stop-instances --instance-ids i-04ba31a1d78978d34`

## tips
After running jobs:
    1. scp file back to local server
    2. copy multple files: `scp user@remote.com:'path/path1/file1 /path2/file2 /path3/file3' /localPath'`

scp ubuntu@ec2-18-236-70-44.us-west-2.compute.amazonaws.com:dev/num_cols_miss_imputing_dict.pkl ~/Documents/ds-local/ds-portfolio/ds-port-proj-classification-loanDefault-webScrape-realData-AWS-2020Feb/dev

keep jupyter running:
tmux new -s jup
jupyter notebook --no-browser

## reference
0. https://medium.com/@junseopark/from-zero-to-aws-ec2-for-data-science-62e7a22d4579
1. https://www.cyberciti.biz/faq/linux-check-disk-space-command/
2. https://www.howtoforge.com/linux-lsblk-command/]
