# CyberSecurity-Projects
========================
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![ELK Network Full Diagram](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/1df55059afeec943886ad88013bad61ab30ab8c9/ELK%20Network%20Map.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat and Metricbeat.

  - [Filebeat-Setup.yml](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/9f7ea64a036eec7b0ab1b017842756e2bae28c67/Automated%20ELK%20Deployment/Filebeat-Playbook.yml)
  - [Metricbeat-Setup.yml] TODO

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient and distributed, in addition to restricting any incoming traffics to the network.
- _The load balancer ensures high availability and reliability by distributing the network traffics and also protects the DWVA from any melicious attempts. The advantage of the jump box makes sure it is the only access point to the DWVA machines, and such eliminates possibilities of backdoors and lessen possible compromisations._

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the services running on the servers and system metrics such as CPU or memory.
- _Filebeat is a shipper for centralizing system logs collected from __Metricbeat__ and forwarding them to Logstash and Elasticsearch on Kibana._
- _Metricbeat is a shipper that collects raw metrics and application data from the DVWA machines and sends them over to __Filebeat__ for indexing._

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| WEB-1    | Target   | 10.0.0.5   | Linux            |
| WEB-2    | Target   | 10.0.0.6   | Linux            |
| ELK      | IDS      | 10.2.0.40  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Host IP: 72.53.80.14
- ELK IP: 20.109.127.43

Machines within the network can only be accessed by the Host Machine only.
- _The ELK machine IP is whitelisted by the Jump Box and therefore accessible at 10.2.0.4 with SSH port._

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses           |
|----------|---------------------|--------------------------------|
| Jump Box | Yes                 |  10.0.0.5 10.0.0.6 10.2.0.0.4  |
| WEB-1    | No                  |           20.102.77.23         |
| WEB-2    | No                  |           20.102.77.23         |
| ELK      | Yes                 | 20.102.77.23 10.0.0.5 10.0.0.6 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

<<<<<<< HEAD
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
=======
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
>>>>>>> 3aa1c7a24ff6179615059363334df0a6376d990f
