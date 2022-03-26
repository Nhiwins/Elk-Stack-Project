## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Elk Network Diagram](https://github.com/Nhiwins/Elk-Stack-Project/blob/main/Images/Elk%20Stack%20Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible playbook files may be used to install only certain pieces of it, such as `Filebeat`.

  - [Ansible Playbooks](https://github.com/Nhiwins/Elk-Stack-Project/tree/main/Ansible)

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
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.

The configuration details of each machine may be found below.

| Name                | Function           | Public IP Address | Private IP Address | Operating System   |
|---------------------|--------------------|-------------------|--------------------|--------------------|
| Jumpbox Provisioner | Gateway            | 20.25.62.17       | 10.1.0.4           | Ubuntu Linux 18.04 |
| Web1                | Application Server | N/A               | 10.1.0.5           | Ubuntu Linux 18.04 |
| Web2                | Application Server | N/A               | 10.1.0.6           | Ubuntu Linux 18.04 |
| ELK Server          | Elk Stack          | 40.118.131.54     | 10.2.0.4           | Ubuntu Linux 18.04 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My Personal IP Address

Machines within the network can only be accessed by the Jumpbox Provisioner and my personal workstation.
- IP Address: 10.1.0.4
- My Personal IP Address

A summary of the access policies in place can be found in the table below.

| Name                | Publicly Accessible | Allowed IP Addresses |
|---------------------|---------------------|----------------------|
| Jumpbox Provisioner | Yes                 | Personal IP Address  |
| Web1                | No                  | 10.1.0.4             |
| Web2                | No                  | 10.1.0.4             |
| ELK Server          | Yes                 | Personal IP Address  |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because multiple machines can be setup quickly without inconsistency. Updates and software can also be installed across systems faster.

The playbook implements the following tasks:
- Install `docker.io` and `python3-pip`
- Install the docker python module
- Configure syslogs to use more memory
- Enable Docker through `systemd`
- Run the Elk Stack Docker container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Elk Container Running](https://github.com/Nhiwins/Elk-Stack-Project/blob/main/Images/Elk%20Container%20Running.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1 (10.1.0.5)
- Web2 (10.1.0.6)

We have installed the following Beats on these machines:
- `Filebeat`
- `Metricbeat`

These Beats allow us to collect the following information from each machine:
- Filebeat probes and forwards log files from the Web VMs to the Elk Stack VM in user friendly format. For example, the log files contain logon information to the DVWA.
- Metricbeat collects system reports from the Web VMs to the Elk Stack VM. These metrics can be uesd to find general information such as location and helps monitor system health. Metrics can be accessed through Kibana.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the `install-elk.yml` playbook to the `/etc/ansible/roles` directory
- Update the hosts file to include the IP addresses of the Web1, Web2, and Elk Server VMs. This also includes enabling the use of python with `ansible_python_interpreter=/usr/bin/python3`
- Run the playbook, and navigate to the ELK server to check that the installation worked as expected.

- The playbook files are [filebeat-playbook.yml](https://github.com/Nhiwins/Elk-Stack-Project/blob/main/Ansible/filebeat-playbook.yml) and [metricbeat-playbook.yml](https://github.com/Nhiwins/Elk-Stack-Project/blob/main/Ansible/metricbeat-playbook.yml). These files are copied to the `/etc/ansible/rules` directory.

- The files used to update are the [filebeat-config.yml](https://github.com/Nhiwins/Elk-Stack-Project/blob/main/Ansible/Config%20Files/filebeat-config.yml) and the [metricbeat-config.yml](https://github.com/Nhiwins/Elk-Stack-Project/blob/main/Ansible/Config%20Files/metricbeat-config.yml). The host must be specified in order to configure the files for the right machine.

- To check that the ELK Server is running correctly, you must visit http://[Host IP]/app/kibana#/home within a browser
