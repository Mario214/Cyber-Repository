
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(~/Cyber-Repository/Diagrams/HW_Diagram)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _yml__ file may be used to install only ce>
  
 - Elk-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _available_, in addition to restricting _Access_ to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
    Load Balancers protect Availability. The advantage of a jump box is that only 1 VM needs to be monitored instead of several as well as being more secure.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _logs_ and system _traffic_.
- _TODO: What does Filebeat watch for?_  lightweight shipper for forwarding and centralizing log data.
- _TODO: What does Metricbeat record?_  lightweight shipper for metrics.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.1.0.4   | Linux            |
| Web 1    | Server   | 10.1.0.7   | Linux            |
| Web 2    | Server   | 10.1.0.5   | Linux            |
| Web 3    | Server   | 10.1.0.6   | Linux            |
| Elk      | Monitor  | 10.2.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the _jumpbox_ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

   My public IP: 99.156.182.71

Machines within the network can only be accessed by _ssh_.

    The Jumpbox machine. IP: 40.84.222.145
    
   A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses      |
|----------|---------------------|-------------------------- |
| Jump Box | Yes/No              | 99.156.182.71 (My IP)     |
| Web 1    | No                  | 40.84.222.145 (Jumpbox IP)|
| Web 2    | No                  | 40.84.222.145 (Jumpbox IP)|
| Web 3    | No                  | 40.84.222.145 (Jumpbox IP)|
| Elk      | Yes                 | 199.156.182.71 40.84.222.145 (My IP and Jumpbox IP)|
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

    Everything is configured the same way in a smaller amount of time opposed to configuring everything manually and can be pushed out to several machines.

The playbook implements the following tasks:

-  The playbook installs Docker used for creating containers.
-  Installs python3-pip used for installing and managing software packages.
-  Increases the amount of virtual memory that will be used.
-  Downloads and launches an elk container.
-  lists the ports the the elk will run on.
-  Enable the docker service on boot.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(~/Cyber-Repository/Diagrams/DockerPS.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

   Web 1: 10.1.0.7.  Web 2: 10.1.0.5.  Web 3: 10.2.0.6

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
    https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
  The beat can collect log data, such as the location of where the log in was from, the device they used and more.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the _filebeat-config_ file to _the filebeat directory_.
- Update the _filebeat-config_ file to include... _the correct IP addresses_
- Run the playbook, and navigate to _the targeted vm_ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_  filebeat-playbook.yml is the play book. it must be copied into the filebeat directory to run
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
  You must update the hosts file to specify the machine you want to run the playbook on. You must update the Filebeat-config.yml to specify which machine you want to run the Filebeat-playbook on.
  The hosts file must be updated to specify the server elk will be installed on.
- _Which URL do you navigate to in order to check that the ELK server is running?_
  https://[Your-elk-vm-ip]:5601/app/kibana
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
 curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb.
 ansible-playbook filebeat-playbook.yml 
