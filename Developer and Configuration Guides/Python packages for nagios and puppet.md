# Python Packages Required to install Nagios and Puppet

This guide will help you to install Nagios plugin both for Python 2.7.x and 3.5.x.

Assuming you've already downloaded, Puppet VM and followed setup instructions
Puppet VM password

root

amo.paton

Installation of nagiosplugin 1.2.4:
- Operating System: `Windows 7 SP1 64 bits`
- Python Version: `2.7.x 32 bits` and `3.5.x 64 bits`
- Installation mode: `pip`

Make sure following 
For python 2.7, C:\Python27\python.exe
For python 3.5, C:\Python35\python3.exe

For nagiosplugin installation, Python 2.7

`C:\> python -m pip install nagiosplugin`

For nagiosplugin installation, Python 3.5

C:\>pip install nagiosplugin


To install check_puppet_agent (mind with the underscores)

Install wheel with pip, for Python 2.7:

C:>pip install check_puppet_agent-1.0.0-py2.py3-none-any.whl

Install wheel with easy_install(provided you have setuptools already installed), For Python 3.5:


This procedure auto detects the Python 3.5 (if set in Environmental Variables)

C:>easy_install -z check_puppet_agent-1.0.0-py3.5.egg
