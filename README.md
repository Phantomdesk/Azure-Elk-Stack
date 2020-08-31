## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

~\Images\Azure-Architecture.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the *filebeat-playbook.yml* file may be used to install only certain pieces of it, such as Filebeat.

	`-filebeat-playbook.yml`
	`-metricbeat-playbook.yml`
	`-install-elk.yml`

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure, in addition to restricting external access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log data and system service metrics.

The configuration details of each machine may be found below.

| Name       | Function      | IP Address | Operating System     |
|------------|---------------|------------|----------------------|
| Jump Box   | Gateway       | 10.0.0.4   | Linux (ubuntu 18.04) |
| Web 1      | DVWA Access 1 | 10.0.0.5   | Linux (ubuntu 18.04) |
| Web 2      | DVWA Access 2 | 10.0.0.6   | Linux (ubuntu 18.04) |
| Elk Server | Server        | 10.1.0.6   | Linux (ubuntu 18.04) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: `67.149.51.17`

Machines within the network can only be accessed by SSH Connection via the *Jump Box Ansible Docker container*.

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses       |
|------------|---------------------|----------------------------|
| Jump Box   | Yes                 | 67.149.51.17:22            |
| Web 1      | No                  | 10.0.0.4 67.149.51.17:4444 |
| Web 2      | No                  | 10.0.0.4 67.149.51.17:4444 |
| Elk Server | No                  | 10.0.0.4 67.149.51.17:5601 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because you can increase efficiency with automation.

The playbook implements the following tasks:
- Install the docker and python3
- Install the docker module and increase available memory usage to allow functionality to the elk server
- Download the docker image and launch the docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

-Web-1: `10.0.0.5`

-Web-2: `10.0.0.6`

We have installed the following Beats on these machines:

-`Filebeat`

-`Metricbeat`

These Beats allow us to collect the following information from each machine:

-Filebeat:

-Collects log data and ships it to a designated destination of your choosing. This allows a clear and concise overview of what is occuring in your system and 
	 allows ease of access to that data in a centralized location.
	 
-Metricbeat:

-Measures and collects metrics from the system and the services running on the server. This allows you to monitor exactly how each service is
     running and the impact it may have on your server as a whole.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to ~/etc/ansible/roles.
- Update the ~/etc/ansible/hosts file to include the Private IP of your elk server within the [elkservers] group.
- Run the playbook, and navigate to http:[your-server-ip]:5601/app/kibana to check that the installation worked as expected.
