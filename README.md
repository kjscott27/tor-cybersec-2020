## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Diagram](Diagrams/groupdiagramelk.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - [Filebeat Playbook](Ansible/filebeat-playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _____, in addition to restricting _____ to the network.
- LoadBalancers assist in protecting against things like DDOS attacks or redundancy issues where one server becomes sluggish or otherwise suddenly crashes. The JumpBox is a useful VM for engineers that may need to get access to other VM's running on the network and need a way to connect as a "service entrance". This is generally useful for managing sysadministrator access sectionally in a resource group.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to any data on the system and system logging.
- Filebeat watches for log changes and filters them as necessary in the configuration, then forwarding them on to Elastisearch/Kibana for further logging and moderation.
- Metricbeat will record any requeted metrics and send them on to Elastisearch/Kibana for further logging and moderation.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Function        | IP Address | Operating System |   |
|------------|-----------------|------------|------------------|---|
| JumpBox    | Gateway         | 10.0.0.1   | Linux            |   |
| Web1       | Web Application | 10.0.0.5   | Linux            |   |
| Web2       | Web Application | 10.0.0.6   | Linux            |   |
| ELK Server | Logging         | 10.1.0.4   | Linux            |   |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 70.27.175.231/32

Machines within the network can only be accessed by SSH.
- 70.27.175.231

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses                    |
|------------|---------------------|-----------------------------------------|
| JumpBox    | Yes                 | 10.0.0.1, 10.0.0.4/32, 70.27.175.231/32 |
| Web1       | No                  | 10.0.0.5                                |
| Web2       | No                  | 10.0.0.6                                |
| ELK Server | Yes                 | 70.27.175.231                           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Automation saves time and can prevent human error.

The playbook implements the following tasks:
- apt-get install docker
- apt-get install python3-pip
- pip install docker
- container memory Configuration
- install and run a docker container of ELK with options

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5, 10.0.0.6

We have installed the following Beats on these machines:
- MetricBeat, FileBeat

These Beats allow us to collect the following information from each machine:
- Filebeat watches for log changes and filters them as necessary in the configuration, then forwarding them on to Elastisearch/Kibana for further logging and moderation. 
- Metricbeat will record any requeted metrics and send them on to Elastisearch/Kibana for further logging and moderation.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible/roles.
- Update the playbook file to include the hosts you're looking to run on, i.e. webservers
- Run the playbook, and navigate to $ELK_PUBLIC_IP:5601 to check that the installation worked as expected.