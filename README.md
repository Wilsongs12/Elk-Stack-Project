## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Project 1 - Diagram](https://github.com/Wilsongs12/Elk-Stack-Project/blob/main/Diagram/Project%201%20Diagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:

- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

- Load balancers protect application availability, by allowing client requests to be shared across a number of servers
- The advantage of a jumpbox is that minimises the attack surface by only allowing remote connections to the cloud network through
  a single VM. Also, remote connections to the jumpbox can be monitored easily.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the configuration and system files.

- Filebeat is used to monitor log files
- Metricbeat is used to collect operating system and service statistics from monitored VMs

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | DVWA     | 10.0.0.5   | Linux            |
| Web-2    | DVWA     | 10.0.0.6   | Linux            |
| Web-3    | DVWA     | 10.0.0.7   | Linux            |
| ElkSrv   | Elk      | 10.3.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- 73.216.47.168

Machines within the network can only be accessed by the Jump Box.
- The Jump Box can access the Elk VM using SSH. The Jump Box's IP is: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes(SSH)            | 73.216.47.168        |
| Web-1    | Yes(HTTP)           | 73.216.47.168        |
| Web-2    | Yes(HTTP)           | 73.216.47.168        |
| Web-3    | Yes(HTTP)           | 73.216.47.168        |
| ElkSvr   | Yes(HTTP)           | 73.216.47.168        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

- build and deployment is automatic,quick, and consistant.
- the configuration and deployment of of virtual machines ensures security measures can be scripted to minimize attack surfaces
- operating system and software updates are easier to deploy

The playbook implements the following tasks:

- The install-elk.yml is designed to set up and launch the Elk repository server in a Docker container on the Elk server. This playbook file
  implements the following:
  
  - installs Docker and Python
  - installs Docker's Python mudule
  - increases virtual memory to support the Elk stack
  - download and launch the Docker Elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- Web-1: 10.0.0.5
- Web-2: 10.0.0.6
- Web-3: 10.0.0.7

We have installed the following Beats on these machines:

- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
 
 - Filebeat collects and sends(to Elk) logs from VMs running Filebeat agent.
 - Metricbeat collects and sends system metrics from the operating system and services of VMs running the Metricbeat agent. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the playbook files to Ansible Docker Container.

- Update the Ansible hosts file (/etc/ansibel/host) to include:
  
  [webservers] 
  
  10.0.0.5 ansible_python_interpreter=/usr/bin/python3
  10.0.0.6 ansible_python_interpreter=/usr/bin/python3
  10.0.0.7 ansible_python_interpreter=/usr/bin/python3
  
  [elkservers]
  
  10.3.0.4 ansible_python_interpreter=/usr/bin/python3
 
- Update the Ansible config file /etc/ansible/ansible.cfg and set remote user parameter to the admin of the web servers.


- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
