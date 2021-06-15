\## Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.
**Elk Deployment**![img](https://lh5.googleusercontent.com/cf9Wur1ILbbRLIIIxNaOF1bhTwqAcuQwMHyZ3rvETajkh-Jytc3qKTUQlt0oNm8rjI8JhNBam_fTlf0cMcgC6GyvkPCpDWdhD82bR36qgGfSZDFzqaQ69qFU02iSDkdBN5ENn2hZ)
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.
  [**filebeat-playbook.yml**](https://github.com/mcfallr/CyberSecurity/blob/main/ansible/Elk-install.yml)
This document contains the following details:Description of the TopologyAccess PoliciesELK ConfigurationBeats in UseMachines Being MonitoredHow to Use the Ansible Build

**Description of the Topology**
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly avaiable, in addition to restricting access to the network.
 What aspect of security do load balancers protect? The load balancer defends organizations against DDoS attacks. It does this by shifting attack traffic from the organization's server to a public cloud provider, which limits access to the real server. 
What is the advantage of a jump box? When a jump box is used, its advantage is that any tools used for SAN are maintained on that single system. When an update to the SAN management software is available, only a single system requires the update.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the jumpbox and system network.What does Filebeat watch for? Changes to file changes on the machine What does Metricbeat record? Collect metrics from the operating system and from services running on the server.
The configuration details of each machine may be found below.

**Name****Function****IP Address****Operating System**Jump BoxGateway10.0.0.6LinuxWeb-1Webserver10.0.0.13LinuxWeb-2Webserver10.0.0.15LinuxELK-ServerMonitoring10.0.0.16Linux

**### Access Policies**
The machines on the internal network are not exposed to the public Internet. 
Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:5601 Kibana Port
Machines within the network can only be accessed by Jump Provisioner .
What was its IP address? 10.0.0.13
A summary of the access policies in place can be found in the table below.

**Name****Publicly Accessible****Allowed IP Addresses**Jump BoxYes13.92.243.250Web-1No10.0.0.13Web-2No10.0.0.15ELK-ServerNo10.2.0.5

 **Elk Configuration**Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because... What is the main advantage of automating configuration with Ansible?
Free: Ansible is an open-source tool.Very simple to set up and use: No special coding skills are necessary to use Ansible’s playbooks (more on playbooks later).Powerful: Ansible lets you model even highly complex IT workflows.Flexible: You can orchestrate the entire application environment no matter where it’s deployed. You can also customize it based on your needs.Agentless: You don’t need to install any other software or firewall ports on the client systems you want to automate. You also don’t have to set up a separate management structure.Efficient: Because you don’t need to install any extra software, there’s more room for application resources on your server.The playbook implements the following tasks: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.
Install docker.ioInstall pip3Install Docker python moduleIncrease virtual memoryDownload and launch a dockerThe following screenshot displays the result of running docker ps after successfully configuring the ELK instance.![img](https://lh3.googleusercontent.com/uOzamZS31WUkNkjjDiQVNE0n1QvZ9wDbFftI2P7i2csBOOMbKRbyNJevLVJXyVQBQ0vWI4NFg-e_lNKdy0D0vThAyTGSncGuF5XNy4LFyXkhDAgVSSZcdRYX-FQWRDVdYvsJ7Kkd)
**Target Machines & Beats**This ELK server is configured to monitor the following machines: -Private IPs of Web-1 and Web-2
**Name****IP Addresses**Web-110.0.0.13Web-210.0.0.15

We have installed the following Beats on these machines:
MicrobeatsThese Beats allow us to collect the following information from each machine:
Filebeat - collects data about the file systemMetricbeat - collects machine metrics, such as uptimeUsing the PlaybookIn order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
SSH into the control node and follow the steps below:
Copy the playbook file to Ansible Control Node. Playbooks for[ Filebeat](https://github.com/mcfallr/CyberSecurity/blob/main/ansible/filebeat-playbook.yml) and [Mtricbeat](https://github.com/mcfallr/CyberSecurity/blob/main/ansible/metric-playbook.yml) 
$ cd /etc/ansible$ mkdir files# Clone Repository + IaC Files$ git clone https://github.com/TenkiYamada/Project-1-ELK-Stack-Project.git# Move Playbooks and hosts file Into `/etc/ansible`$ cp /Project-1-ELK-Stack-Project/ReadMe/Playbooks/*
Update the hosts file to include web server and elkEdit hosts file to update and to make Ansible run the playbook on a specific machine, and specify which machine to install the ELK server on versus which to install Filebeat.Copy of the hosts file is also here: hosts
$ cd /etc/ansible$ cat > hosts <<EOF[webservers]10.0.0.710.0.0.8
[elk]10.1.0.4EOF
Run the playbook, and navigate to Kibana (http://[Host IP]/app/kibana#/home) to check that the installation worked as expected.cd /etc/ansible $ ansible-playbook install_elk.yml elk $ ansible-playbook install_filebeat.yml web servers $ ansible-playbook install_metricbeat.yml web servers
Check that the ELK server is running: http://[Host IP]/app/kibana#/home