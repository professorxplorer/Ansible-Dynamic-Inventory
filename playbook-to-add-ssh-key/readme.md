add 
[defaults]
host_key_checking = False and "private_key_file = /Downloads/Ansible-srv.pem" key path 
in ansible.cfg

add 
[servers]
[servers:vars]
ansible_ssh_common_args="-o StrictHostKeyChecking no"

in hosts

run this cmd in root of this project

```ansible-playbook -i ec2.py add-key.yml -u ubuntu --private-key=/home/professor/Downloads/Ansible-srv.pem -e "key=~/.ssh/id_rsa.pub"
```

Now all of your ec2 servers have you .pub key

to remove latter

```ansible-playbook -i ec2.py add-key.yml -u ubuntu --private-key=/home/professor/Downloads/Ansible-srv.pem -e "key=~/.ssh/id_rsa.pub status=absent"
```


ansible -i ec2.py  ap-south-1a --list-hosts




ansible-playbook -i ec2.py  ~/Desktop/LinuxBk/Desktop/Ansible/playbook-to-add-ssh-key/add-key.yml -u ubuntu --private-key=/home/professor/Downloads/Ansible-srv.pem -e "key=~/.ssh/id_rsa.pub"


#[servers:vars]
#ansible_ssh_common_args="-o StrictHostKeyChecking no"


ansible-playbook -i ec2.py  ~/Desktop/LinuxBk/Desktop/Ansible/playbook-to-add-ssh-key/add-key.yml -u ubuntu --private-key=/home/professor/Downloads/Ansible-srv.pem -e "key=~/.ssh/id_rsa.pub"


ansible-playbook -i ec2.py add-key.yml -u ubuntu --private-key=/home/professor/Downloads/Ansible-srv.pem -e "key=~/.ssh/id_rsa.pub"