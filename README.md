# Project_1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![project1_diagram drawio](https://user-images.githubusercontent.com/93159337/154403307-dd55f154-d524-4df5-bcfc-38927f87db00.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML files may be used to install only certain pieces of it, such as Filebeat.

- [Ansible Playbook](https://github.com/NikeoseaRichardson/Project_1/blob/e1a17f0d3eb82066c53c0e0fe4eb7c460ce045be/ansible/DVWA/my-playbook.yml)

- [Ansible Configuration](https://github.com/NikeoseaRichardson/Project_1/blob/e1a17f0d3eb82066c53c0e0fe4eb7c460ce045be/ansible/DVWA/ansible.cfg)

- [Ansible Hosts](https://github.com/NikeoseaRichardson/Project_1/blob/e1a17f0d3eb82066c53c0e0fe4eb7c460ce045be/ansible/DVWA/hosts)

- [Ansible ELK Installation and VM coonfiguration](https://github.com/NikeoseaRichardson/Project_1/blob/e1a17f0d3eb82066c53c0e0fe4eb7c460ce045be/ansible/DVWA/install-elk.yml)

- [Ansible Filebeat Playbook](https://github.com/NikeoseaRichardson/Project_1/blob/e1a17f0d3eb82066c53c0e0fe4eb7c460ce045be/ansible/Filebeat/filebeat-playbook.yml)

- [Ansible Filebeat Config File](https://github.com/NikeoseaRichardson/Project_1/blob/e1a17f0d3eb82066c53c0e0fe4eb7c460ce045be/ansible/Filebeat/filebeat-config.yml)

- [Ansible Metricbeat Playbook](https://github.com/NikeoseaRichardson/Project_1/blob/e1a17f0d3eb82066c53c0e0fe4eb7c460ce045be/ansible/Metricbeat/metricbeat-playbook.yml)

- [Ansible Metricbeat Config File](https://github.com/NikeoseaRichardson/Project_1/blob/e1a17f0d3eb82066c53c0e0fe4eb7c460ce045be/ansible/Metricbeat/metricbeat-config.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
- The load balancers protect many security aspects such as Availability, Web Traffic, and Web Security. The load balancer serves as the middle man between the clients and the servers by distributing traffic across the servers, which enhances the user experience because of the extra security factor.

- There are many advantages of the Jump Box such as such as Security, Network Segmentation, Automation, and Access Control. The jump box allows admin to be the first to conntect and all have one point of access, adding another layer of security. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- The filebeat will monitor the log files and the locations that you choose specifically, collects log events, and transfers them to Elasticsearch or Logstash for indexing.
- The metricbeat will use the metrics and statistics that it collects and send them to the output that you choose, that being Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name               |   Function  |       IP Address      | Operating System |
|--------------------|-------------|-----------------------|------------------|
| Jump Box           |Gateway      | 10.0.0.7/20.120.19.169| Linux            |
| Web1               |WebServer    | 10.0.0.8              | Linux            |
| Web2               |WebServer    | 10.0.0.9              | Linux            |
| Elk                |ELK Server   | 10.1.0.5/40.112.160.39| Linux            |
| Load Balancer      |LoadBalancer | Static External IP    | Linux            |
| Workstation        |AccessControl| ExternalIP or PublicIP| Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Elk Server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-Workstation Public IP through TCP 5601

Machines within the network can only be accessed by Workstation and Jump-Box.
- Only Jump-Box and my Work Station were allowed access to the ELK VM through SSH connect. The IP addresses were as followed, Jump-Box IP (10.0.0.7 via SSH port 22) Workstation Public IP (via port TCP 5601)

A summary of the access policies in place can be found in the table below.

| Name         | Publicly Accessible |                   Allowed IP Addresses                   |
|--------------|---------------------|----------------------------------------------------------|
| Jump Box     | No                  | Workstation Public IP on SSH 22                          |
| Web1         | No                  | 10.0.0.7 on SSH 22                                       |
| Web2         | No                  | 10.0.0.7 on SSH 22                                       |
| ElkServer    | No                  | Workstation Public IP using TCP 5601                     |
| LoadBalancer | No                  | Workstation Public IP on HTTP 80                         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because the Ansible allows you to efficiently delpoy multiplier apps. Eliminating the need to write custom code to automate your systems. The tasks that you require to do be done would be listed within a playbook, from there the ansible will determine how to get your system to the state you want them to be in.

The playbook implements the following tasks:
- Increase System Memory
- Launching and Exposing the container with ports 5601:5601, 9200:9200, 5044:5044
- Installs docker.io to the ELK machine (VM)
- Installs pip3 (python3) to the ELK machine
- Installs the Docker python module
- Download and launch the Docker ELK container, configuring/publishing the ports for elasticsearch, logstash, and kibana

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img width="772" alt="Screen Shot 2022-02-16 at 10 52 17 PM" src="https://user-images.githubusercontent.com/93159337/154402954-bf91dc40-d9e4-4f65-8aa1-0a7ded1e05ef.png">

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1: 10.0.0.8
- Web2: 10.0.0.9
- Elk: 10.1.0.5

We have installed the following Beats on these machines:
- FileBeat and MetricBeat

These Beats allow us to collect the following information from each machine:
- The Filebeat will monitor and log events, collects all of the data and sends it to the ELK server.
<img width="959" alt="Screen Shot 2022-02-19 at 10 43 19 AM" src="https://user-images.githubusercontent.com/93159337/155444364-eeab8f23-8667-4b19-8328-a22219ce74ce.png">

- Metricbeat will periodically collect metric data from the target servers. It is used to monitor their performance by collecting data such as system CPU, memory, and load. 
<img width="873" alt="Screen Shot 2022-02-23 at 10 16 19 PM" src="https://user-images.githubusercontent.com/93159337/155451779-adc3307a-44f7-4bbc-9f40-c7794ce61a78.png">

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file filebeat-playbook.yml or install-elk.yml to file to '/etc/ansible/roles' folder.
- Update the configuration file so tahat your IP address of the ELK machine is included. Within the file, the hosts file need to have the IP addresses of the webservers and the elk machine.
- Run the playbook with the command ansible-playbook filebeat-playbook.yml and navigate to Kibana http://[your.VM.IP]:5601/app/kibana> Logs : Add log data > System logs > 5:Module Status > Check data to check that the installation worked as expected.
