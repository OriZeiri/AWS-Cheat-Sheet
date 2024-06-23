# AWS Cheat Sheet
_written by orizz for personal usage_<br>
_Using Linux Machine : Ubuntu 20.0.4_

[Course Link](https://qttechacademy.udemy.com/course/aws-certified-cloud-practitioner-new/learn/lecture/20055746?start=135#overview)
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
            "UserId": "AIDAS7JBZ3JKZ7C5SNGXB",
            "Arn": "arn:aws:iam::204618717781:user/Ori",
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