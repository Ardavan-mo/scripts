# scripts
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
<img src="https://github.com/Ardavan-mo/scripts/blob/main/diagrams/Azure-Diagram.png"  width="1660" height="1045">

https://github.com/Ardavan-mo/scripts/blob/main/diagrams/Azure-Diagram.png

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
- _TODO: What is the main advantage of automating configuration with Ansible?
 
<h3>It allows for full automation of a specific server and reduces configuration errors.</h3>
The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.

<h3>
Install Docker: 
  
  Installs the core docker code to the remote server.
  
Install Python3_pip:
  
  Pip is an installation module that allows for additional docker modules to be installed easier

Docker Module:
  
  Tells the previous PIP module to install the necessary docker component modules.
  
Increase Memory/Use More Memory:
  
  A common issue with the ELK Docker image is to little memory. This help fix the issue to allow the server to launch.
  </h3>

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
 
![TODO: Update the path with the name of your screenshot of docker ps output]

<img src="https://github.com/Ardavan-mo/scripts/blob/main/ansible/images/docker-ps.png"  width="1460" height="245">
                                                                                                                 



### Target Machines & Beats
This ELK server is configured to monitor the following machines:
  <h3>
  
10.0.0.4
  
10.0.0.5
  
10.0.0.6
  
10.0.0.7
  
10.1.0.4
  </h3>

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed 

<h3>We have installed Filebeat and Metricbeat on the following Systems: Web-1, Web-2, Web-3, ardavan-ELK.</h3>
These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc.

<h3>Filebeats collects system type events such as logins to see who is actively logging into the system.</h3>

<h3>Metricbeats collects useful information such as cpu usage and memory, this is particularly useful when seeing if there are any aberant programs or behaviors taking system resources.

</h3>
<h3><a href="https://github.com/Ardavan-mo/scripts/blob/main/ansible/images/cpu-usage.png">Example</a> </h3>
<img src="https://github.com/Ardavan-mo/scripts/blob/main/ansible/images/cpu-usage.png"  width="1660" height="1045">









### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
<h3>
- Copy the  install-elk.yml   file to /etc/ansible/roles/filebeat-7.4.0-amd64.yml
  
<h3><a href="https://github.com/Ardavan-mo/scripts/blob/main/ansible/install-elk.yml">Example</a> 
  
- Update the  hosts  file to include the attribute, such as elk </h3>

 <h3><a href="https://github.com/Ardavan-mo/scripts/blob/main/ansible/hosts.yml">Example</a> </h3>
</h3>

<h3>Run the playbook, and navigate to  http://20.211.170.82:5601/app/kibana#/home to check that the installation worked as expected.</h3>

<h2>Note: 20.211.170.82 that is my elk VM public Ip.</h2>  
 

_TODO: Answer the following questions to fill in the blanks:_

Which file is the playbook? Where do you copy it?

<h3>Answer : For the ANSIBLE : created the dvwa_playbook.yml as the playbook.

<h3><a href="https://github.com/Ardavan-mo/scripts/blob/main/ansible/dvwa_playbook.yml">Open The File</a>

Answer : For FILEBEAT: created filebeat-playbook.yml as the playbook.

<h3><a href="https://github.com/Ardavan-mo/scripts/blob/main/ansible/filebeat-playbook.yml">Open The File</a>

Answer: For METRICBEAT: created metricbeat-playbook.yml as the playbook.

<h3><a href="https://github.com/Ardavan-mo/scripts/blob/main/ansible/metricbeat-playbook.yml">Open The File</a>
  </h3>
  
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
  <h3>

### How to Edit the Ansible Hosts file in this directory /etc/ansible/hosts
```bash
#List the IP Addresses of your webservers
#You should have at least 2 IP addresses
[webservers]
10.0.0.5 ansible_python_interpreter=/usr/bin/python3
10.0.0.6 ansible_python_interpreter=/usr/bin/python3
10.0.0.7 ansible_python_interpreter=/usr/bin/python3
#List the IP address of your ELK server
#There should only be one IP address
[elk]
10.2.0.4 ansible_python_interpreter=/usr/bin/python3
 ``` 
</h3>  
  
 ### How to Create the ELK Installation and VM Configuration in the /etc/ansible/ directory:

```bash
      - name: Config elk VM with Docker
        hosts: elk
        remote_user: sysadmin
        become: true
        tasks:
```
  ### How to Copy the raw Filebeat Module Configuration file from web

``` bash
  setup.kibana:
  host: "10.0.0.12:5601"
  .
  .
  .
hosts: ["10.0.0.12:9200"]
  username: "elastic"
  password: "changeme" 

  ```
  
  
- _Which URL do you navigate to in order to check that the ELK server is running?
  
  <h3>Test Kibana on web : _http://[your.ELK-VM.External.IP]:5601/app/kibana</h3>
  
  <h3> Test Kibana on localhost: _sysadmin@10.1.0.4: curl localhost:5601/app/kibana</h3>
  
  <img src="https://github.com/Ardavan-mo/scripts/blob/main/ansible/images/kibana.png"  width="1660" height="1045">
  

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
we should run this commend to download or update playbook file :
curl https://github.com/Ardavan-mo/scripts/tree/main/ansible/install-elk.yml
