## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
![elkstack drawio](https://user-images.githubusercontent.com/95665069/154867965-31d30efe-37bd-4c86-bdc8-ff5afb7aa2cf.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YML file may be used to install only certain pieces of it, such as Filebeat.

- Elk Stack -
- Filebeat - 
- Metricbeat -

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
Load balancers help ensure environment availability through distribution of incoming data to web servers. Jump boxes allow for more easy 
administration of multiple systems and provide an additional layer between the outside and internal assets.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the event logs and system metrics.
What does Filebeat watch for?
Filbeats watch for log directories or specific log files.
What does Metricbeat record?
Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server.




The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| WEB 1    |  Server  | 10.0.0.5   | Linux            |
| WEB 2    |  Server  | 10.0.0.6   | Linux            |
|Elk Server|Log server| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-Workstation MY Public IP

Machines within the network can only be accessed by Workstation and Jump-Box-Provisioner through SSH Jump-Box.
Which machine did you allow to access your ELK VM?
- 10.1.0.4 via SSH port 22

What was its IP address?
- Workstation MY Public IP via port TCP 5601

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | Workstation/personal |
| Load Bal.| Yes                 | Open                 |
| Web 1    | No                  | 10.0.0.5             |
| Web 2    | No                  | 10.0.0.6             |
|Elk Server| No                  |Public IP W/ TCP 5601 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because services running can be limited so system installations with updates turn processes to be more replicable.
 
 What is the main advantage of automating configuration with Ansible?
 Ansible can quickly and easily deploy multitier applications through a YAML playbook
 Custom codes are not necessary to automate your systems
 Ansible can figure out how to get your systems to the state you want them to be in

The playbook implements the following tasks:
- Installing docker.io, pip3, and the docker module -

![image](https://user-images.githubusercontent.com/95665069/154869831-f80ecfc4-adf9-4280-a215-1f2fbc401fa7.png)

- Increase the virtual Memory -

![image](https://user-images.githubusercontent.com/95665069/154869964-0f2c8c9f-971d-4ebc-9e02-7f8e4ebca978.png)

- System control (sysctl) Module -

![image](https://user-images.githubusercontent.com/95665069/154870010-15115fa3-17e9-4cb1-aebd-06c055c1363a.png)

- downloads and launches the docker container for elk server -

![image](https://user-images.githubusercontent.com/95665069/154870092-fde7e899-dfd3-4635-8ab0-e463e8b3e910.png)

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/95665069/154870123-24757e76-2329-4cf8-ad64-123b5cca0ff9.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-Web 1 (10.0.0.5)
-Web 2 (10.0.0.6)

We have installed the following Beats on these machines:
-FileBeat
Login to Kibana > Logs : Add log data > System logs > DEB > Getting started
Copy: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deb
-Metric Beat
Login to Kibana > Add Metric Data > Docker Metrics > DEB > Getting Started
Copy: curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.6.1-amd64.deb

These Beats allow us to collect the following information from each machine:

-Filebeat is a log data shipper for local files. Installed as an agent on the servers, Filebeat monitors the log directories or specific log files and forwards them either to Elasticsearch or Logstash for indexing. 

-Metricbeat collects metrics and statistics on the system. An example is a cpu usage, which can be used to monitor the system health.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Config file to the Web Virtual machines.
- Update the /etc/ansible/hosts file to include the IP address of the Elk Server VM and webservers.
- Run the playbook, and navigate to http://[Elk_VM_Public_IP]:5601/app/kiban to check that the installation worked as expected.

Answer the following questions to fill in the blanks:

- Which file is the playbook?
The Filebeat-configuration

- Where do you copy it?
/etc/ansible/files/filebeat-config.yml to /etc/filebeat/filebeat.yml

- Which file do you update to make Ansible run the playbook on a specific machine?
 filebeat-config.yml

- How do I specify which machine to install the ELK server on versus which to install Filebeat on? 
You specify which machine to install by updating the host files with IP addresses of web and elk servers and from there you select which group to run on in ansible 

- Which URL do you navigate to in order to check that the ELK server is running?
http://[your.ELK-VM.External.IP]:5601/app/kibana 


