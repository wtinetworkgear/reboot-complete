# WTI RESTful - Reboot Complete.

This Ansible Playbook piggybacks off the reboot Ansible plugin and adds another level of reboot reliability.

This playbook will see if the Linux **hosts** you are trying to reboot are reachable. 
If not reachable, then the playbook will contact the WTI Power Device and reboot the plug that the failed Linux **hosts** are connected to. 

If the Linux **hosts** are reachable, then the Ansible builtin reboot plugin is run, this plugin, after the reboot, will wait for the Linux **hosts** to become reachable. If the Linux **hosts** does not become reachable, then the playbook will contact the WTI Power Device and reboot the plug that the failed **hosts** are connected.

# To Configure Playbook Script:
First you must have a WTI Power device (with a CPM or VMR series)
Second, you must have installed the WTI Ansible collection
https://galaxy.ansible.com/wti/remote

In your Ansible hosts file, these parameters need be defined to talk to a WTI PDU

**These parameters are mandatory:**
wti_device, wti_username, wti_password, wti_plug

**These parameters are optional:**
wti_use_https, wti_validate_certs:

**Examples are as follows:**
wti_device: test.wti.com
wti_username: super
wti_password: super
wti_plug: "5"
wti_use_https: true 
wti_validate_certs: true 

If any of the mandatory parameters are not defined, then the WTI PDU reboot portion is skipped.

# To Run:
`sudo ansible-playbook ./cpm_reboot-complete.yml`

This script will see if the Linux **hosts** are online, if they are online, then a system **reboot** command will be attempted. If the Linux **hosts** are rebooted sucessfully, the script will end. If any of the detection or reboot operations fail, the **cpm_plugcontrol** module from the WTI collection will run and reboot the Linux **hosts** that failed.

# Ansible Galaxy Collection / RESTful API Documentation:

The Ansible Galaxy Collection for WTI devices can be found here:
https://galaxy.ansible.com/wti/remote

The HTML, RAML OR OpenAPI/Swagger file relating to the RESTful API calls can be found here:

https://www.wti.com/t-wti-restful-api-download.aspx

# Contact US
If you have any questions, comments or suggestions you can email us at kenp@wti.com

# About Us
WTI - Western Telematic, Inc.
5 Sterling, Irvine, California 92618

Western Telematic Inc. was founded in 1964 and is an industry leader in designing and manufacturing power management and remote console management solutions for data centers and global network locations.
Our extensive product line includes Intelligent PDUs for remote power distribution, metering, reporting and control, Serial Console Servers, RJ45 A/B Fallback Switches and Automatic Power Transfer Switches.
