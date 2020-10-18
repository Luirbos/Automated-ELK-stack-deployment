## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/Luirbos/Automated-ELK-stack-deployment/blob/main/Diagrams/ELK-Red_Team_diagram.png

These files have been tested and used to generate a live ELK deployment on Azure.
They can be used to either recreate the entire deployment pictured above.
Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

https://github.com/Luirbos/Automated-ELK-stack-deployment/blob/main/Ansible/install-ELK.yml

This document contains the following details:
  - Description of the Topologu
  - Access Policies
  - ELK Configuration
  - Beats in Use
  - Machines Being Monitored
  - How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

-Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
-Load balancers protect the Availability in the CIA triad the advantage of a Jump Box is that it creates a fan to make security easier.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system data.
-Filebeat watches for changes to the files
-Metric beat records metric data

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function  | IP Address | Operating System |
|----------|-----------|------------|------------------|
| Jump Box | Gateway   | 10.0.0.4   | Linux            |
| Web 1    |DVWA Server| 10.0.0.5   | Linux            |
| Web 2    |DVWA Server| 10.0.0.6   | Linux            |
| Web 3    |DVWA Server| 10.0.0.8   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
(my personal IP address)

Machines within the network can only be accessed by the Jumpbox.
The ELK VM can only be accessed through the Jumpbox, it's private IP address is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |     yes             |(my public IP address)|
|  Web 1   |     no              |                      |
|  Web 2   |     no              |                      |
|  Web 3   |     no              |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it saves
a lot of time

The playbook implements the following tasks:

-increases the memory used to allow room for the ELK
-installs docker.io, docker and python3 pip
-downloads and runs the sebp/elk:761 container
-publihes ports 5061 9200 and 5044

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/Luirbos/Automated-ELK-stack-deployment/blob/main/Diagrams/docker_ps_screenshot.PNG

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
10.0.0.5
10.0.0.6
10.0.0.8

We have installed the following Beats on these machines:
Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
filebeat keeps track of changes to log files and log events.
meticbeat monitors metric data and statistics.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml file to /etc/ansible/.
- Update the hosts file to include:
10.0.0.5 ansible_python_interpreter=/usr/bin/python3
10.0.0.6 ansible_python_interpreter=/usr/bin/python3
10.0.0.8 ansible_python_interpreter=/usr/bin/python3

- Run the playbook, and navigate to http://[kibana public IP]:5601 then click on system logs -> module status -> check data to check that the installation worked as expected.

-https://github.com/Luirbos/Automated-ELK-stack-deployment/blob/main/Ansible/filebeat-playbook.yml is the playbook copy it to /etc/ansible/files
-Update the hosts file to make Ansible run the playbook on a specific machine.
To specify which machine to install the ELK server on versus which to install Filebeat on, input the machine's private IP address under filebeat or ELK
- To check if the ELK server is running, navigate to http://[kibana public IP]:5601

Specific commands the user will need to run to download the playbook, update the files, etc. can be found here:

