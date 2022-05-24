## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![https://github.com/echudnow/blob/main/Diagrams/XCorp_RedTeam_Mountain_Network_Diagram.png]echudnow/Diagrams/XCorp_RedTeam_Mountain_Network_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YMAL file may be used to install only certain pieces of it, such as Filebeat.

[https://github.com/echudnow/echudnow/blob/main/ansible/Docker]echudnow/ansible/Docker)

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
- _Load balancer protect against DDoS.  The advantage of a jump box is it contanis all the tools for a SANS system.  When an updte is needed, only the jump box is updated instead of each component._

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system system metrics.
- Filebeat watches for log data
- Metricbeat collects metrics from your systems and services

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator]() to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | DVWA/ELK | 10.0.0.5   | Linux            |
| Web-2    | DVWA/ELK | 10.0.0.6   | Linux            |
| ELK VM   | Kibana   | 10.1.0.5   | Linux            |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 
- _24.255.25.239_

Machines within the network can only be accessed by 10.0.0.4.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses    |
|----------|---------------------|----------------------   |
| Jump Box | Yes                 | 24.255.25.239           |
| Web-1    | No                  | 10.0.0.4, 10.1.0.5      |
| Web-2    | No                  | 10.0.0.4, 10.1.0.5      |
| ELK VM   | Yes                 | 10.0.0.4,20.118.164.121 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it confirms the configurationwas completed without error.  The error free playbook deploys future machines with limited changes to configuration files.

The playbook implements the following tasks:

- Installs Docker and Python3-pip as the default docker modules
- Increases virtual memory to a value of "262144"
- Allows the docker service to be enabled upon boot
- Launches the elk image (sebp/elk:761) to the desired container
- Confirm the ports that ELK uses to run (5601,9200,5044)

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- filebeat
- metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects log files from specific machines such as log events like user login events.  Metricbeat collects metrics from your systems and services. This includes CPU and memory usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml and metricbeat-playbook.yml files to ~/etc/ansible/directory.
- Update the host file to include the IP address of your machine.
- Run the playbook, and navigate to VM with ELK deployed to check that the installation worked as expected. 