## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Network Diagram](https://github.com/Gmartz96/Cybersecurity-project-1/blob/main/Diagrams/'Week-13-Project-1-Network.png'

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible directory may be used to install only certain pieces of it, such as Filebeat.

  - hosts.yml
  - install-ELK.yml
  - filebeat-config.yml
  - filebeat-playbook.yml
  - metricbeat-config.yml
  - metricbeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available. Traffic will be distributed evenly by the load balancer in an attempt to prevent server crashes. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the applications and system access authorization.
- Filebeat monitors traffic and sends alerts based on a predefined set of rules. Any suspicious traffic can be analyzed and appropriate action can be taken, whether it be to block traffic from the source or ignore a possible false alarm.
- Metricbeat monitors statistics on web traffic data. Traffic metrics can be filtered for parameters like country origin and operating system of the client.

The configuration details of each machine may be found below.

| Jumpbox    | Gateway                   | 10.0.0.4 | Linux |
| Web 1      | DVWA Access               | 10.0.0.5 | Linux |
| Web 2      | DVWA Access               | 10.0.0.6 | Linux |
| ELK Server | Monitoring of Web Servers | 10.1.0.4 | Linux |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the web and ELK machines can accept connections from the Internet. Access to these machines are only allowed from the following IP addresses:
- 98.31.0.88

Machines within the network can only be accessed by the jumpbox.
- The ELK server can be reached with an SSH key by the ansible container in the jumpbox and its application interface can also be accessed via HTTP from one authorized IP address, 98.31.0.88.

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jumpbox    | yes                 | 98.31.0.88
| Web 1      | no                  | 98.31.0.88  | 20.127.29.66
| Web 2      | no                  | 98.31.0.88  | 20.127.29.66
| ELK Server | yes                 | 98.31.0.88  | 20.127.29.66

- Web 1 and Web 2 are accessible via an HTTP connection through the load balancer

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Automation of the ELK playbook makes this task highly repeatable, easily deployable once the playbook syntax is correct, and errors are easier to troubleshoot with a one command deployment as opposed to a multistep manual installation.

The playbook implements the following tasks:
- Install docker, docker.io and python3
- Increase memory usage and availability so ELK can be usable
- Download and launch an ELK container
- Enable docker on boot so ELK does not have to be manually started on every boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(~/Cybersecurity-Project-1/Diagrams/Running-ELK-Container)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat: Installed on Web 1 and Web 2, monitors logging traffic data and sends it to the ELK server over port 9200
- Metricbeat: Installed on Web 1 and Web 2, monitors web traffic metrics and statistics and sends it to the ELK server over port 9200

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-ELK.yml file to your local or remote ansible container.
- Update the hosts.yml file to include the IP address of your intended ELK server and your intended web servers which will receive filebeat and metricbeat.
- Run the playbook, and navigate to http://<ELK_server_public_IP_Address>:5601/app/kibana to check that the installation worked as expected.

### Playbook Commands

- Install ELK to desired ELK server IP address specified in hosts.yml
  - ansible-playbook install-ELK.yml

- Install filebeat to web server IP addresses specified in filebeat-config.yml
  - ansible-playbook filebeat-playbook.yml

- Install metricbeat to web server IP addresses specified in metricbeat-config.yml
  - ansible-playbook metricbeat-playbook.yml
