# Create and Configure Ansible Controller
- 1 - Spin up EC2 instance.
- 2 - Create user for ansible controller --> useradd ansadmin
- 3 - Give password for ansadmin user --> passwd ansadmin
- 4 - Add ansadmin user to sudoer file --> visudo
- 5 - Copy and paste following command to suoder file --> ansadmin ALL=(ALL)      NOPASSWD:ALL
- 6 - Login as ansadmin user --> su - ansadmin
- 7 - Create ssh-key in order to exchange ssh-key and passwordless access to managed nodes --> ssh-keygen
- 8 - Logout from ansadmin user
- 9 - Give PasswordAuthentication Yes --> vim /etc/ssh/sshd_config uncomment PasswordAuthentication Yes comment out PasswordAuthentication No
- 10 - Restart sshd service in order to apply changes--> systemctl restart sshd
- 11 - Install pyhton, pip --> yum install python -y | yum install python-pip -y
- 12 - Install Ansible --> pip install ansible
- 13 - Verify ansible --> ansible --version
- 14 - Whenever we install ansible with pip it doesn't come with configuration file, we have to create configuration file.
- 15 - Create ansible directory inside /etc/ in order to create ansible.cfg file --> mkdir /etc/ansible && cd /etc/ansible
- 16 - Create ansible.cfg --> vim ansible.cfg (Search on google for 'ansible configuration file' copy and past context)

# Create and Configure RHEL Managed Node
- 1 - Spin up EC2 instance.
- 2 - Create user for ansible controller --> useradd ansadmin
- 3 - Give password for ansadmin user --> passwd ansadmin
- 4 - Add ansadmin user to sudoer file --> visudo
- 5 - Copy and paste following command to suoder file --> ansadmin ALL=(ALL)      NOPASSWD:ALL
- 6 - Give PasswordAuthentication Yes --> vim /etc/ssh/sshd_config uncomment PasswordAuthentication Yes comment out PasswordAuthentication No
- 7 - Restart sshd service --> systemctl reload sshd
- 8 - Copy private ip of Rhel-Managed-Node vm --> ifconfig 
- 9 - Login as ansadmin to Ansible-Controller vm.
- 10 - Copy Ansible-Controller ssh-key to RHEL vm in order to access RHEL vm without password --> ssh-copy-id <Private-Ip-RHEL>

# Create and Configure Ubuntu Managed Node
- 1 - Spin up EC2 instance.
- 2 - Create user for ansible controller -->  useradd -m -d /home/ansadmin ansadmin
- 3 - Give password for ansadmin user --> passwd ansadmin
- 4 - Change default note editor to vim (Ubuntu default editor is nano) --> export EDITOR=vim
- 5 - Add ansadmin user to sudoer file --> visudo
- 6 - Copy and paste following command to suoder file --> ansadmin ALL=(ALL:ALL)      NOPASSWD:ALL
- 7 - Give PasswordAuthentication Yes --> vim /etc/ssh/sshd_config change PasswordAuthentication from 'no' to 'yes'
- 8 - Restart sshd service --> systemctl reload sshd
- 9 - Copy private ip of Ubuntu-Managed-Node vm --> ip address show
- 10 - Login as ansadmin to Ansible-Controller vm.
- 11 - Copy Ansible-Controller ssh-key to Ubuntu vm in order to access Ubuntu vm without password --> ssh-copy-id <Private-Ip-UBUNTU>

# Create Inventory File for Ansible
- 1 - Connect to Ansible-Controller vm.
- 2 - Go to /etc/ansible directory because default hosts file have to be inside /etc/ansible --> cd /etc/ansible
- 3 - Create inventory (hosts) file and add Managed Nodes ip adresses --> vim hosts
- 4 - Verify connection between ansible-controller and managed-nodes --> ansible -m ping all
- 5 - Ad-hoc command --> Ad-hoc commands are great for tasks you repeat rarely
    - ansible all -m command -a 'date' --> will show date on managed hosts.
    - ansible all -m yum -a 'name=git' -b --> Install managed hosts git with ad-hoc command. -b (become root)