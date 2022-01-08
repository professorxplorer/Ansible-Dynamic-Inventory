# Ansible Dynamic Inventory for AWS EC2
### Pre-requisites:
1. Ansible Server - Get [Click here](https://docs.ansible.com/ansible/latest/user_guide/intro_dynamic_inventory.html#inventory-script-example-aws-ec2) to install on RHEL 8 and [click here](https://aws.amazon.com/blogs/apn/getting-started-with-ansible-and-dynamic-amazon-ec2-inventory-management/) to install on Amazon Linux
### Setup
# Optional Step to add ssh to all ec2 instances in on go ! or to setup ssh in ansible hosts [Click here](https://github.com/professorxplorer/Ansible-Dynamic-Inventory/tree/master/playbook-to-add-ssh-key)
To get help on dynamic inventory please follow [Ansible Official Document](https://docs.ansible.com/ansible/latest/user_guide/intro_dynamic_inventory.html#inventory-script-example-aws-ec2)
To get help on dynamic inventory please follow [AWS Official Document](https://aws.amazon.com/blogs/apn/getting-started-with-ansible-and-dynamic-amazon-ec2-inventory-management/)
1. Download [ec2.py](https://github.com/professorxplorer/Ansible-Dynamic-Inventory/blob/master/Ansible-dynamic-inventory/ec2.py) and [ec2.ini](https://github.com/professorxplorer/Ansible-Dynamic-Inventory/blob/master/Ansible-dynamic-inventory/ec2.ini) files
2. Create IAM Programmatic access user with EC2 full access on AWS console if you are using ec2 instance as your ansible server
`IAM` → `users` → `Add user`
`EC2` → `Select-your-server` → `Actions` →`Security` → `Modify IAM role` → `Add or Update IAM role`
2. Export IAM user credentials on the Ansible server. if you are using your own machine as a server
Get an IAM role and get secret keys from AWS account.
2. Install AWS CLI on your machine.
```sudo apt-get update```
``` sudo apt-get install awscli ```
2. Configure aws cli
``` aws configure ```
Enter your aws Access and secret Access keys
``` AWS Access Key ID [****************DQ7G]: ```
``` AWS Secret Access Key [****************W9mW]: ```
``` Default region name [us-east-1]: ```
```bash
export AWS_ACCESS_KEY_ID='1bc123'
export AWS_SECRET_ACCESS_KEY='abc123'
```
3. install python-pip and boto3
## Install Python
``` sudo apt-get install python ```
## Install pip
``` sudo apt install python3-pip ```
## Install Python Boto3 using PIP
``` pip install boto3 ```
``` pip3 - version ```
4. To export keys permanently make sure that you have installed pip and boto and add credentials ~/.boto file
5. add executing permissions to ec2.py script
```sh
chmod 755 ec2.py
```
6. test the script
```
./ec2.py - list
```
6. List out servers that are running on ap-south-1a AZ
```
ansible -i ec2.py ap-south-1a - list-hosts
```
6. How to Run playbook with tags
### Option 1
1. We can run ansible-playbook for our sever with some specific tag by giving hosts name as a tag in our playbook
``` - -
- name: Aerospike Dynamic Inventory
hosts: tag_dev_view
gather_facts: no
# vars_files:
```
2. then we can run our playbook as
``` ansible-playbook -i ec2.py main.yml ```
in this as we are giving tags in playbook tag is the combination of ```tag_dev_view``` tag → tag dev → key view →value
### Option 2
1. In this we can give multiple tags to our ansible server to identify environment and name Because we could have the same name in multiple environments.
2. For this we can get our hosts to all AWS we don't have any hosts as it's dynamic inventory.
3. Now we will be providing tags in command while running the ansible-playbook
## To ping server with tag
``` ansible -i ec2.py - limit "tag_App_backend:&tag_Environment_staging:&tag_Usage_clock_worker" -m ping all ```
## To run the playbook
``` ansible-playbook -i ec2.py - limit "tag_App_backend:&tag_Environment_staging:&tag_Usage_clock_worker" main.yml ```
## Authors
The module is maintained by  [Professor Xplorer](https://professorexplorer.github.io/)
## License
Licensed. See [LICENSE]() for full details.