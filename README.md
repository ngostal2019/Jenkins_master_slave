# Jenkins_master_slave
##Master installation and Configuration

sudo yum -y update
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo amazon-linux-extras install epel -y # required to install daemonize required to have jenkins on AWS
sudo yum -y upgrade
sudo yum -y install daemonize jenkins java-1.8.0-openjdk-devel
sudo systemctl daemon-reload
sudo systemctl start jenkins
sudo systemctl status jenkins

## Open Jenkins via the web browser and read this file
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

## Set up the JAVA_HOME path:
find / -name jre 2>/dev/null
vim ~/.bash_profile
JAVA_HOME= /path/to/jre

source ~/.bash_profile # load your modifications to the Environment variable

## Set up the JAVA_HOME on the Jenkins Dashboard 
Manage Jenkins > Global Tools Configuration > JDK

## Configure the Jenkins Agent (Slaves) by clicking on build executer and follow these steps from my YouTube Channel


##Clients Side Setup 

#Enable the PasswordAuthentication in /etc/ssh/sshd_config

sudo vim /etc/ssh/sshd_config
#PasswordAuthentication no 
PasswordAuthentication yes

reload the sshd daemond
sudo systemctl reload sshd

# Finally create Your users you wish Jenkins to remotely connect via ssh and a directory for the builds

# Continuity of the Master configuration after jumping on the client

## Do this after Enabling SSH connection from no to yes of the line having PasswordAuthentication in /etc/ssh/sshd_config on the slaves side
 mkdir /var/lib/jenkins/.ssh (As root user)
 ssh-keyscan -H slave_ip >> /var/lib/jenkins/.ssh/known_hosts
 or
 ssh-keyscan -H slave_hostname >> /var/lib/jenkins/.ssh/known_hosts (must have dns resolution)

## Give back the ownership of /var/lib/jenkins/.ssh/known_hosts 
chown -R jenkinks:jenkins /var/lib/jenkins/.ssh

Subscribe, Like, Share, Comment to help me improve !!!
