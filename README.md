# AzureLab
Azure Lab for High Availability Web Hosting
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

<figure><img src="/Diagrams/Azure.jpg"><figcaption></figcaption></figure>
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the "YAML" files may be used to install only certain pieces of it, such as Filebeat.

  - /Ansible/

This document contains the following details:
- Description of the Topologu
- Access Policies
  - IP Addresses (internal and External)
- ELK Configuration
  - Beats in Use.
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly avaiable, in addition to restricting traffic to the network.
- _TODO: What aspect of security do load balancers protect? Weserver uptime
What is the advantage of a jump box?_ restricts accrss to the network to a single point on entry to config the network securly.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system metriks.
- _TODO: What does Filebeat watch for? Logs Changes to the system files
- _TODO: What does Metricbeat record?_ Logs machine metricks including uptime, CPU, MEmory and traffic.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Function      | IP Address | Operating System           |
|------------|---------------|------------|----------------------------|
| Jump-Box   | Gateway       | 10.0.0.8   | Linux - Ubuntu 18.04 LTS   |
| Elk-Server | Cloud Monitor | 10.1.0.4   | Linux - Ubuntu 18.04 LTS   |
| Web-1      | Web Server    | 10.0.0.4   | Linux - Ubuntu 18.04 LTS   |
| Web-2      | Web Server    | 10.0.0.9   | Linux - Ubuntu 18.04 LTS   |
| Web-3      | Web Server    | 10.0.0.5   | Linux - Ubuntu 18.04 LTS   |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: My Office Address with the correct Public Key

Machines within the network can only be accessed by the Jump-Box Server via the Ansible container running on the Jump Box.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_Ansible Container (public ELK IP on differant private IP 10.1.0.4)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 10.0.0.1 10.0.0.2    |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_ Quick to rebuild. Better Quality Assurance. All servers setup the same way. Changed can happen all at the sae time.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...Docker, Python 3 (PIOP)
- ...Increases memory on the VM
- ... Publishes Ports 5601, 
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

| Name       | Function      | IP Address | Operating System           |
|------------|---------------|------------|----------------------------|
| Web-1      | Web Server    | 10.0.0.4   | Linux - Ubuntu 18.04 LTS   |
| Web-2      | Web Server    | 10.0.0.9   | Linux - Ubuntu 18.04 LTS   |
| Web-3      | Web Server    | 10.0.0.5   | Linux - Ubuntu 18.04 LTS   |

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_ Metric and file beats

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
File beats collects logs of file changes for each minitored system. The information is than sent to Logstash and Elastic Search. An Example would be system.syslog that shows the boot process and 
Colleccts metwroics on the operating system. Its ued to report on CPU, Memory and load metrics

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the 'playbook.yml' file to /etc/Ansible/files directory.
- Update the 'hosts' file in the /etc/Ansible directory to include any internal IP addresses for new servers
- Run the playbook, and navigate to the Kibana Server URL to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running? http://Loadbalancer_IP/setup.php

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._ 
curl -i weblocation_of_the_YML file
ansible-playbook /path/playbook_name.yml
