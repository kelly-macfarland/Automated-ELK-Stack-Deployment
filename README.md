# Automated-ELK-Stack-Deployment
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/kelly-macfarland/Automated-ELK-Stack-Deployment/blob/main/network_diagram.jpg

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

  - root@773c98c89be6:etc/ansible/roles/filebeat-playbook2.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
-Load balancers serve as protection against distributed denial-of-service (DDoS) attacks. The Load balancer also serves as a distributer of traffic between clients across multiple servers. The advantage of a jump box is that it increases security and it is network and host-restricted.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic
- _TODO: What does Filebeat watch for?_
Filebeat watches for log files/locations and collects log events.
- _TODO: What does Metricbeat record?_
Metricbeat takes the metrics and statistics that collects and ships them to0 the output you specify. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator] (http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------   |----------|------------|------------------|
| Jump Box   | Gateway              | 10.1.0.4   | Linux        |
| Web-1 VM | Virtual Machine | 10.1.0.5   | Linux        |
| Web-2 VM | Virtual Machine | 10.1.0.6   | Linux        |
| ELK VM       | Virtual Machine | 10.2.0.4   | Linux        |
| DVWA-VM3| Virtual Machine| 10.3.0.5   | Linux        |             
|DVWA-VM4 |Virtual Machine | 10.3.0.4   | Linux        |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_
98.206.141.27
10.1.0.4

Machines within the network can only be accessed by SSH.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
The only machine able to connect to the ELK VM is the jumpbox.  The private IP for the jumpbox is 10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|------------------------|
| Jump Box      | Yes/No    | 10.0.0.1 10.0.0.2 |
| Web-1           |  No           |  10.1.0.4                |
| Web-2           |  No           |  10.1.0.4                |
| DVWA-VM3  | No           | 10.1.0.4                 |  
| DVWA-VM4  | No           | 10.1.0.4                 |   
|ELK VM           | No           | 10.1.0.4  & Personal IP      |            

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
The primary advantages of automating configuration using Ansible is its quick learning curve and its ease of use. I utilized playbooks to configure my machines as it allowed a single command to set up multiple machines after the initial configuration.

To set up the playbook, complete the following tasks:
- Create the VM: establish a simple name “Elk-VM”, note the private and public IPs as you’ll need them to SSH into the VM and access the Kibana Portal respectfully.
-Once you access the Kibana Portal, you download filebeat and navigate to log data > system logs > DEB to see the instructions for the playbook
-Download and configure /etc/hosts file to include your new server. You add your new group and private IP to the file.

The playbook implements the following tasks:
1.  Download Docker.
2.  Double-click the DMG file and drag-and-drop Docker into your Applications folder.
3.  You need to authorize the installation with your system password.
4.  Double-click Docker.app to start Docker.
5.  The whale in your status bar indicates Docker is running and accessible.
6.  Docker presents some information on completing common tasks and links to the documentation.
7.  You can access settings and other options from the whale in the status bar. a. Select About Docker to make sure you have the latest version.
The playbook downloads, installs and configures the Elk VM and starts the container.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
Image 1- Images folder

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
ELK VM: Public IP 52.250.124.74, Private IP Address 10.2.0.4
WEB1 VM: Public IP Adress 13.68.186.179, Private IP Address 10.1.0.5
WEB2 VM: Public IP Address 13.68.186.179, Private IP Address 10.1.0.6

We have installed the following Beats on these machines:
FileBeat and MetricBeat

These Beats allow us to collect the following information from each machine:
FileBeat collects Data and Data logs
MetricBeat to periodically collect metrics from the operating system and from servers running in the server.
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
•	Copy the YAML file to '/etc/ansible' directory.
•	Update the /etc/ansible/hosts' file to include 'hosts' group, private IP address, the following line 'ansible_python_interpreter=/usr/bin/python3'
•	Run the playbook, and navigate to 'curl localhost/setup.php' to check that the installation worked as expected.
•	The playbooks are listed as 'install-elk.yml' // 'filebeat-playbook.yml' // 'metricbeat-playbook.yml' // 'ansible_config.yml' and are meant to be copied in the '/etc/ansible' directory.
•	Update the '/etc/ansible/hosts' directory with the hosts group name with the correlating IP addresses underneath to specify on which machines to run the playbooks.
•	To check if the ELK server is running, navigate to 'http://[your.VM.IP]:5601/app/kibana'
•	install-elk.yml: This will install the ELK stack on the VM in your <hosts> group.
•	install-filebeat.yml: This will install Filebeat on your <hosts> group.
•	install-metricbeat.yml: This will install Metricbeat on your <hosts> group.

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
Ansible-playbook filebeat-playbook.yml
