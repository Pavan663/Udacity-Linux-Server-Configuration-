# Udacity-Linux-Server-Configuration
## About Project:
#### This project is about configuring the linus server
## Process to create grader user:
#### sudo adduser grader
#### It adds new user
 sudo nano/etc/sudoers
####  In the above file we include the following:
 grader  ALL=(ALL:ALL) ALL
#### The above sentence gives permission to grader
##  To Create ssh key pair for grader:
#### On your local machine in terminal in ubuntu for example/command prompt for example windows
 ssh-keygen
#### The above command creates keys in .ssh folder
  su - grader
#### create .ssh directory and new file authorized_keys
  mkdir .ssh
  sudo nano .ssh/authorized_keys
#### Now place the public key with .pub extension to authorized_keys and save the file
  chmod 700 .ssh
  chmod 644 .ssh/authorized_keys
  service ssh restart
#### Logging in to grader with private key generated
  ssh -i .ssh/id_rsa grader@ipaddress 
#### Change the port 22 to 2200 
sudo nano /etc/ssh/sshd_config
#### Restart the ssh server
  service ssh restart
#### Private key generated :
  ssh -i .ssh/id_rsa grader@ipaddress
