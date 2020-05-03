# Azure_ELK_Stack_Project
Installation and configuration ELK Stack on Azure.
The files in this repository were used to configure the network depicted below.

Images/My_azure_diagram.png - Described with a diagram to explain the project scheme.
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. 
Alternatively, select portions of the installation file may be used to install only certain pieces of it, such as Filebeat.

  - YML scripts/filebeat_playbook.yml - playbook file for installation of Filebeat to target VM. Located in YML scripts files.

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly responsive, in addition to  distributes traffic to the network.
- Load balancers helps to protect availbility and responsibility of your applications and can detect DDOS attacks. 
- Jumpbox servers provide access and manage to your servers that located in different security zones.Also,Jumpbox is using minimum resources and minimum security breaches.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the states and system logs.
- Filebeat monitors the log files which you specify and collects log events for sending it ELK servers.
- Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as ELK servers.

The configuration details of each machine may be found below.

| Name      | Function      | IP Address | Operating System |
|---------- |----------     |------------|------------------|
| Jump Box  | Gateway       | 10.0.0.4   | Linux Ubuntu     |
| DVWA-VM1  | Web Server    | 10.0.0.7   | Linux Ubuntu     |
| DVWA-VM2  | Web Server    | 10.0.0.8   | Linux Ubuntu     |
| ELK-Server| Search Engine | 10.0.0.9   | Linux Ubuntu     |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. 
Access to this machine is only allowed from the following IP addresses:
- 99.227.86.0/24

Machines within the network can only be accessed by SSH.
- Ansible machine which is located in Jumpbox server allow to access ELK VM. IP address 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 99.227.86.0/24       |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because
lets you quickly and easily deploy multiple applications to multiple servers in one command.
- The main advantage is Ansible can be run from the command line without using of any configuration files and make it fast to save time.

The playbook implements the following tasks:
- Installing Docker.io
- Installing Phyton modules
- Install ELK container
- Command for Configure increasing virtual memory on ELK VM
- Published ports(5601,9200,5044) 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

- Images/elk_docker_ps.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.7
- 10.0.0.8

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects log and event data on yours system.For example, you can use Auditbeat to collect logs and centralize audit events from the Linux Audit Framework.
- Metricbeat takes the metrics and statistics that you specify and send it ELK server such as Elasticsearch or Logstash.

Screenshot after successfully installation of Filebeat on DVWA machines.
- Images/Filebeat_Dashboard.png

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. 

SSH into the control node and follow the steps below:
- Copy the source file to destination.
- Update the file to include docker images or containers.
- Run the playbook, and navigate to target machine to check that the installation worked as expected.

The following screenshot displays the result of deploying filebeat_playbook.yml file after successfully configuring to the DVWA-VM1 instance
- Images/Ansible_playbook_deployment.png

My playbook description and function.
- Playbook file is .yml file. We copy it into ansible machine under /etc/ansible directory.
- We update the configuration file to make Ansible run the playbook on a specific machine. You can specify machines IP address in the host files on Ansible machine to install the 
ELK server on versus which to install Filebeat on.
- Copy the public IP of your ELK server and add port number which you specifed in playbook(5601) and navigate to in order to check that the ELK server is running or no.

Run command for ansible playbook:
- ansible-playbook -i vyos.example.net, -u ansible -k -e ansible_network_os=vyos first_playbook.yml
