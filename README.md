# AzureLab
Azure Lab for High Availability Web Hosting
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

<figure><img src="/Diagrams/Azure.png"><figcaption></figcaption></figure>
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the "YAML" files may be used to install only certain pieces of it, such as Filebeat.

| Name                                                                            |
------------------------------------------------------------------------------------------------|
|<a href="https://github.com/wjanness/Azure/tree/main/Ansible">- Project Related Ansible Files</a> |
|<a href="https://github.com/wjanness/Azure/blob/main/HOMEWORK.md">- Screenshots of Azure configuration</a> |
|<a href="https://github.com/wjanness/Azure/blob/main/Linux">- Linux Administration BASH scripts</a> |

This document contains the following details:
- Description of the Topology
- Access Policies
  - IP Addresses (internal and External)
- ELK Configuration
  - Beats in Use.
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
- A Load Balancer can ensure systems such as 'Web Servers' have trafic equally distributed to the most available server ensuring that whatever is being hosted has the highest probability if being available. 
- The 'Jump-Box' Server helps restrict backend accross to the network to a single point of entry on a separate external IP address. The 'Jump-Box' server uses an 'Ansible' container to run the 'playbook.yml' files to configure new and existing servers on the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system metrics.
- The Filebeat process watches System Logs for changes to the system files. 
- The Metricbeat process Logs machine metrics including uptime, CPU, Memory and Traffic Loads.

The configuration details of each machine may be found below.]

| Name       | Function      | IP Address | Operating System           |
|------------|---------------|------------|----------------------------|
| Jump-Box   | Gateway       | 10.0.0.8   | Linux - Ubuntu 18.04 LTS   |
| Elk-Server | Cloud Monitor | 10.1.0.4   | Linux - Ubuntu 18.04 LTS   |
| Web-1      | Web Server    | 10.0.0.4   | Linux - Ubuntu 18.04 LTS   |
| Web-2      | Web Server    | 10.0.0.9   | Linux - Ubuntu 18.04 LTS   |
| Web-3      | Web Server    | 10.0.0.5   | Linux - Ubuntu 18.04 LTS   |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box Provisioner can accept connections from a public address on the Internet. Access to this machine is only allowed from a defined URL / IP address(es) ## [jump.4-indigo.com]. Login to this system can only proceed with a pre-shared 'Public Key'.

Machines within the network can only be accessed by the Jump-Box Server via the Ansible container running on the Jump Box.

A summary of the access policies in place can be found in the table below.

| Name                  | Publicly Accessible | Allowed IP Addresses |
|-----------------------|---------------------|----------------------|
| Jump Box:Port 22      | Yes                 | jump.4-indigo.com    |
| Elk Server:Port 5601  | Yes                 | kibana.4-indigo.com  |
| Elk Server:Port 22    | No                  | 10.1.0.4 (jump-box)  |
| Load Balancer:Port 80 | Yes                 | www.4-indigo.com     |
| Web-1 Server:Port 80  | No                  | 10.1.0.4 (jump-box)  |
| Web-2 Server:Port 80  | No                  | 10.1.0.4 (jump-box)  |
| Web-3 Server:Port 80  | No                  | 10.1.0.4 (jump-box)  |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because using Ansible, you can very quickly rebuild the entire infrastructure. This means better quality assurance in that all servers will be setup the same way. It will also save time because changes can happen all at the same time.

The playbook implements the following tasks:
- ... Download 'Images' to be installed on target machines. 
- ... Install software such as Docker & Python 3 (PIP)
- ... Increases 'Virtual Memory' on target systems as needed.
- ... Publishes Required Ports such as: (tcp) 5044, 5601, 9200, 9300 
- ... Download and install ELK Stack Container (v761)
- ... Enable installed system to startup on reboot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
<figure><img src="/Images/Docker_PS.png"><figcaption></figcaption></figure>

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name       | Function      | IP Address | Operating System           |
|------------|---------------|------------|----------------------------|
| Web-1      | Web Server    | 10.0.0.4   | Linux - Ubuntu 18.04 LTS   |
| Web-2      | Web Server    | 10.0.0.9   | Linux - Ubuntu 18.04 LTS   |
| Web-3      | Web Server    | 10.0.0.5   | Linux - Ubuntu 18.04 LTS   |

We have installed the following Beats on these machines:
- FileBeats
- MetricBeats

These Beats allow us to collect the following information from each machine:
- File beats collects logs of file changes for each monitored system. The information is than sent to Logstash and Elastic Search. An Example would be    system.syslog that shows the boot process and 
- Collects metrics on the system such as CPU, Memory and Traffic Load and is used to generate reports. Its used to report on CPU, Memory and load metrics

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the 'filebeat_config.yml' and 'filebeat-playbook.yml' files to /etc/Ansible/files directory. 
- Make sure to update the 'host' IP address in lines 1106 and 1806 in the filebeats_config.yml file.
- Run the playbook, and navigate to the Kibana Server URL (kibana.4-indigo.com) to check that the installation worked as expected.

Run these commands to first change to the directory where the elk-server.yml file will be saved. You will run the curl command to download the elk-server
* cd /etc/ansible
* curl -i href="https://github.com/wjanness/Azure/tree/main/Ansible/elk-server.yml
* ansible-playbook /etc/ansible/elk-server.yml
