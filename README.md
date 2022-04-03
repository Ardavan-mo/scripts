# scripts
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: https://github.com/Ardavan-mo/scripts/tree/main/diagrams/Azure-Diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: 
<h3>Elk Install <a href="https://github.com/Ardavan-mo/scripts/blob/main/ansible/install-elk.yml">Open The File</a> </h3>
<h3>DVWA  <a href="https://github.com/Ardavan-mo/scripts/blob/main/ansible/dvwa_playbook.yml">Open The File</a> </h3>

<h3>FileBeat  <a href="https://github.com/Ardavan-mo/scripts/blob/main/ansible/filebeat-playbook.yml">Open The File</a> </h3>
<h3>MetricBeat  <a href="https://github.com/Ardavan-mo/scripts/blob/main/ansible/metricbeat-playbook.yml">Open The File</a> </h3>

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build



### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting  access to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?
- 
<h3>A jump box or bastion server serves as a gatway to gain entry into a remote network. Many times the primary mode of access is SSH and without the key access is forbidden.

A load balancer is meant to serve as a specific point of access for a service that is served by multiple machines. This allows high availability models to function properly.</h3>

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resources.
- _TODO: What does Filebeat watch for?

<h3>Filebeat is meant primarily to watch for system logs and forward any changes to the Elasticsearch Host.</h3>

- _TODO: What does Metricbeat record?

<h3>Metricbeat is used only for gathering metrics and system resources usage for display in Elasticsearch.</h3>





The configuration details of each machine may be found below.
<h3>

| Name       | Function            | IP Address | Operating System |
|------------|---------------------|------------|------------------|
| Jump Box   | Gateway             | 10.0.0.4   | Ubuntu           |
| Web-1      | Web Server          | 10.0.0.5   | Ubuntu           |
| Web-2      | Web Server          | 10.0.0.6   | Ubuntu           |
| Web-3      | Web Server          | 10.0.0.7   | Ubuntu           |
| Ardavan-ELK| ElasticSearch Stack | 10.1.0.4   | Ubuntu           |

</h3>




### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the   jump box   machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

<h3>Public IP:  40.122.232.89</h3>

Machines within the network can only be accessed by jump box   
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?

<h3>Public IP:  13.67.227.184</h3>
<h3>Private IP: 10.0.0.4</h3>



A summary of the access policies in place can be found in the table below.
<h3>

| Name     | Publicly Accessible   | Allowed IP Addresses      |
|----------|-----------------------|---------------------------|
| Jump Box | SSH - 22 - Yes        | 13.67.227.184             |
| Web-1,2,3| No                    | Web LB - 40.122.232.89    |
| LB       | HTTP - 80 - Yes       | *                         |
| ELK      | Kibana - 5601 - Yes   | *                         |
| ELK      | HTTP API - 9200 - Yes | 10.0.0.0/16               |

</h3>


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
It allows for full automation of a specific server and reduces configuration errors
The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
nstall Docker: Installs the core docker code to the remote server
Install Python3_pip: Pip is an installation module that allows for additional docker modules to be installed easier
Docker Module: Tells the previous PIP module to install the necessary docker component modules
Increase Memory/Use More Memory: A common issue with the ELK Docker image is to little memory. This help fix the issue to allow the server to launch

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
 
![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
https://github.com/Ardavan-mo/scripts/tree/main/ansible/images/docker-ps.png


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
10.0.0.4
10.0.0.5
10.0.0.6
10.0.0.7
10.1.0.4

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
We have installed Filebeat and Metricbeat on the following Systems: Web1, Web2, Web3, ELK.
These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeats collects system type events such as logins to see who is actively logging into the system.
See here for Filebeats Example
Metricbeats collects useful information such as cpu usage and memory, this is particularly useful when seeing if there are any aberant programs or behaviors taking system resources
See here for MetricBeats Example








### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the  elk_install.yml   file to /etc/ansible/roles/ filebeat-7.4.0-amd64.yml
Example: https://github.com/Ardavan-mo/scripts/tree/main/ansible/ install-elk.yml
- Update the  hosts  file to include the attribute, such as elk
Example : https://github.com/Ardavan-mo/scripts/tree/main/ansible/hosts.yml


- Run the playbook, and navigate to  http://20.211.170.82:5601/app/kibana#/home to check that the installation worked as expected.
Note: 20.211.170.82 that is my elk VM public Ip.  
 

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
we should run this commend to download or update playbook file :
curl https://github.com/Ardavan-mo/scripts/tree/main/ansible/ install-elk.yml
