# Automated ELK Stack Deployment


### The files in this repository were used to configure the network depicted below.

![ELK Network Full Diagram](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/1df55059afeec943886ad88013bad61ab30ab8c9/ELK%20Network%20Map.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat and Metricbeat.

  - [Filebeat-Setup.yml](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/9f7ea64a036eec7b0ab1b017842756e2bae28c67/Automated%20ELK%20Deployment/Filebeat-Playbook.yml)
  - [Metricbeat-Setup.yml](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/947c695a95dfec9401b6dad72a6c29df30d1c938/Automated%20ELK%20Deployment/Metricbeat-Setup.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient and distributed, in addition to restricting any incoming traffics to the network.
- The load balancer ensures high availability and reliability by distributing the network traffics and also protects the DWVA from any melicious attempts. The advantage of the jump box makes sure it is the only access point to the DWVA machines, and such eliminates possibilities of backdoors and lessen possible compromisations.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the services running on the servers and system metrics such as CPU or memory.
- Filebeat is a shipper for centralizing system logs collected from __Metricbeat__ and forwarding them to Logstash and Elasticsearch on Kibana.
- Metricbeat is a shipper that collects raw metrics and application data from the DVWA machines and sends them over to __Filebeat__ for indexing.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| WEB-1    | Target   | 10.0.0.5   | Linux            |
| WEB-2    | Target   | 10.0.0.6   | Linux            |
| ELK      | IDS      | 10.2.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Host IP: 72.53.80.14
- ELK IP: 20.109.127.43

Machines within the network can only be accessed by the Host Machine only.
- The ELK machine IP is whitelisted by the Jump Box and therefore accessible at 10.2.0.4 with SSH port.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses           |
|----------|---------------------|--------------------------------|
| Jump Box | Yes                 |  10.0.0.5 10.0.0.6 10.2.0.0.4  |
| WEB-1    | No                  |           20.102.77.23         |
| WEB-2    | No                  |           20.102.77.23         |
| ELK      | Yes                 | 20.102.77.23 10.0.0.5 10.0.0.6 |

### Elk Configuration

Ansible was used to automate configuration of the [ELK machine](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/39568c39d30e4927e7cda0aedcafeb6af1b2042e/Automated%20ELK%20Deployment/ELK-Setup.yml). No configuration was performed manually, which is advantageous because...
- Automating configuration with Ansible saves time for now and future deployments, it eliminates mechanical errors and can be used not only in application deployments and configuration management but also in provisioning,intra-service orchestration, and many other IT needs.

The playbook implements the following tasks:
- Install Docker to deploy containers
- Install Python for Docker module configuration
- Configure Docker module  using python
- Raw command to increase virtual memory
- Backup increase virutal memory command if raw command fails 
- Docker command to download container image
- Enable the docker service on system boot

The following screenshot displays the result of running `docker ps -a` after successfully configuring the ELK instance.

![ELK Container](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/963a0061bf02c96ebecf0b6c65ae6536f59a2d59/Automated%20ELK%20Deployment/ELK%20Container.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- WEB-1: 10.0.0.5
- WEB-2: 10.0.0.6

We have installed the following Beats on these machines:
- [Filebeat](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/963a0061bf02c96ebecf0b6c65ae6536f59a2d59/Automated%20ELK%20Deployment/Filebeat-Setup.yml)
- [Metricbeat](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/963a0061bf02c96ebecf0b6c65ae6536f59a2d59/Automated%20ELK%20Deployment/Metricbeat-Setup.yml)

These Beats allow us to collect the following information from each machine:
- Filebeat: Monitors log files and collect log events to be forwarded for indexing.
- Metricbeat: Collect metrics from the operating system and from services running on the server, ships these data to filebeat.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the [Filebeat](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/963a0061bf02c96ebecf0b6c65ae6536f59a2d59/Automated%20ELK%20Deployment/Filebeat-Setup.yml)  and [Metricbeat](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/963a0061bf02c96ebecf0b6c65ae6536f59a2d59/Automated%20ELK%20Deployment/Metricbeat-Setup.yml) and [hosts](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/39568c39d30e4927e7cda0aedcafeb6af1b2042e/Automated%20ELK%20Deployment/hosts) files to /etc/ansible/. 
- Update the [hosts](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/39568c39d30e4927e7cda0aedcafeb6af1b2042e/Automated%20ELK%20Deployment/hosts) file to include the monitor IP under ELK (include **ansible_python_interpreter=/usr/bin/python3** after the IP to run with python).
- Run the playbook, and navigate to **PLAY RECAP** to check that the installation worked as expected.

- [ELK](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/83516e5cb9faa89efb362e41b64bc6f0e99cf8ab/Automated%20ELK%20Deployment/ELK-Setup.yml), [Filebeat](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/83516e5cb9faa89efb362e41b64bc6f0e99cf8ab/Automated%20ELK%20Deployment/Filebeat-Setup.yml), [Metricbeat](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/83516e5cb9faa89efb362e41b64bc6f0e99cf8ab/Automated%20ELK%20Deployment/Metricbeat-Setup.yml) are the playbooks, once you set up ansible, you can copy them to **/etc/ansible/**.
- [hosts](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/83516e5cb9faa89efb362e41b64bc6f0e99cf8ab/Automated%20ELK%20Deployment/hosts) file can be updated to choose the destination IP address of where you want to run the previously mentioned playbooks on, within [hosts](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/83516e5cb9faa89efb362e41b64bc6f0e99cf8ab/Automated%20ELK%20Deployment/hosts) you can make your own category of hosts by adding **[yourChoiceOfName]** and your choices of IPs under that name, or you can directly mentioned the IP address in the playbooks on 3rd line after [**hosts:**](https://github.com/SimonZhang0122/CyberSecurity-Projects/blob/83516e5cb9faa89efb362e41b64bc6f0e99cf8ab/Automated%20ELK%20Deployment/ELK-Setup.yml#L3)  
- Once Everything has been setted up, you can navigate to **yourMachinesPublicIP:5601/app/kibana** to make sure its working (_for exmaple, if my ELK machine's IP is 20.109.127.43, then the URL will be 20.109.127.43:5601/app/kibana_) 
