# Installation of Nagios and Puppet Python Packages

### About This Guide
This guide will help you to install client-side version of Nagios and Puppet Python packages on Windows Operating System. It'll help you to access these services from Python interface.

### Prerequisites
- Operating System: `Windows 7 SP1 x64 Architecture`
- Python Version: `3.7.11 x64 bits`
- Installation mode: `pip`

### **Nagios**

Nagios is an essential part for monitoring in DevOps lifecycle. It is an software monitoring tool that helps to monitor, alert and resolve problems of infrastructural devices and application before they can affect customers and businesses. 

### Installation:

To install `nagiosplugin`,

`C:\> python -m pip install nagiosplugin==1.3.2`

### **Puppet**
Puppet is an essential part for automation in DevOps lifecycle. It is an infrastructural automation tool which helps to manage complex workflows and configuration of servers.

### Installation:
To install `check_puppet_agent`,

`C:\> python -m pip install check_puppet_agent`

where `-m` targets to install package for specific executable python file.

With these steps, we have completed installation of Nagios and Puppet packages.

