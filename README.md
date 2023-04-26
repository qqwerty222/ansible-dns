# Set up DNS, webserver and connected user using ansible

This playbook has three roles.

- webserver, install nginx and create index page with ip 
- DNS, install and configure bind9 to redirect testdomain.com ot webserver
- user, set previously configured dns as main and curl testdomain.com

## Instruction to run

To run this playbook set up next configuration:
- hosts  
You should specify ip addresses of future dns, webserver and user in hosts file, see ./hosts_reference.
Addresses in hosts file will be used by ansible to ssh into target machines. So if you want to configure AWS ec2 put public ips in hosts file. And make sure there is sec groups that allow ssh.  

- group_vars  
Also you need to specify ip addresses in ./group_vars/all file.
See ./group_vars/all_reference. This ip addresses will be used in generating templates of configuration files. So in case of using AWS ec2 you can specify private ips, because connections can be local.

- ssh-key  
Finally you need to specify ssh-key ansible will use to connect target machines. Make sure that user will be used to connect can run "sudo" without prompting a password. If you use Jenkins ansible plugin specify ssh-key from Jenkins credentials. If you run playbook locally save ssh-key in current directory as ./ssh_key. Or specify address to ssh-key in ./ansible.cfg

## Run playbook
```bash
$ ansible-playbook run playbook.yml
```