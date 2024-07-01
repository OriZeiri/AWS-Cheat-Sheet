# AWS Cheat Sheet
_Written by orizz for personal usage_<br>
_Using Linux Machine : Ubuntu 20.0.4_<br>
_Last update: July 01_<br>

[Course Link](https://qttechacademy.udemy.com/course/aws-certified-cloud-practitioner-new/learn/lecture/20055746?start=135#overview)<br>
[Qualitest Excel with qcraft Labs](https://ibase1-my.sharepoint.com/:x:/r/personal/sharon_baruch_qualitestgroup_com/_layouts/15/doc2.aspx?sourcedoc=%7BE439253B-36E5-4F4A-8934-2BCD3331EE11%7D&file=AWS-%20Cloud%20Practitioner.xlsx&action=default&mobileredirect=true)

## IAM:
1. list all the users from CLI
    ```
    aws iam list-users
    ```
    the output is a json object that contains the following acording to this format:
    ```
    {
    "Users": [
        {
            "Path": "/",
            "UserName": "User",
            "UserId": "AAAAAAAAAAAAAAAAAAAA",
            "Arn": "arn:aws:iam::ACOUNTID:user/Ori",
            "CreateDate": "2024-06-17T20:06:28+00:00",
            "PasswordLastUsed": "2024-06-23T20:14:13+00:00"
        },
        ...
    ]
    }
    ```

## EC2:

1. login to EC2 Instance via ssh:

    ```
    ssh -i key_file.pem ec2-user@ipadd
    ```
    to verify that we connected sucssesfully we should see the next prompt in the terminal:
    ```
       ,     #_
    ~\_  ####_        Amazon Linux 2023
    ~~  \_#####\
    ~~     \###|
    ~~       \#/___ https://aws.amazon.com/linux/amazon-linux-2023
    ~~       V~' '->
        ~~~         /
        ~~._.   _/
            _/ _/
        _/m/'
    [ec2-user@ip-172-31-31-195 ~]$
    ```
    note that we use the ec2-user instead of the local user on the machine.
    in the course the instrcator use Amazon Linux 2 AMI and Im using Amazon Linux 2023

2. to fetch users data, from the instance like the command `aws iam list-users` do not use `aws configure` command.<br>

    Add a Role for the instance. 
in your instaces page select the required instance and click on:<br>
Actions > Security > Modify IAM role

    Then add your desired role for your instance, running the command again should work now.

3. To find which avaliablity zone the EC2 Instance is on, click on the instance in the dashboard. under category **Networking** check out avaliablity zone - for example eu-west-1**b** - that matter for future 

## EC2 Instance Storage
### EBS Volume - Elastic Block Store
details:
- network drive that can be attached to EC2 Instance
- can be mounted to one instance at a time
- bound to avaliablity zone
- multipule EBS Volume can be attached to EC2 Instance - EBS Multi-Attach
- Instance can also be "free" and not connected at all, on demand attachment. 

1. when opening a new volume make sure it's in the same avaliablity zone (read EC2 - No.3 to find out how.)

### EBS Snapshot
- make a backup of an EBS Volume
- can copy across AZ(avaliablity zone)/ Region

for example:

|us-east-1a|EBS Snapshot|us-east-1b|
|----------|------------|-----------|
|EBS - 50 GB | Snapshot-> EBS -> restore | EBS - 50 GB|

#### Snapshot types:
- Standard - the default value. 
- Archive - cheaper, longer to get the data from. 24h to 72h of restoring the archive.
- Recycle Bin - setup rules for deleted snapshots, that can be recoverd after accidental deletion. save data for a period of time, after being deleted.

#### Create a snapshot 
- EC2 Instances>Actions>Create a snapshot
- EC2 Elastic Block Store> Create a snapshot

### AMI - Amzon Machine Image
AMI Are customization of an EC2 instance