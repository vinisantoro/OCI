<p align="center">
  <img src="https://assets.zabbix.com/img/logo/zabbix_logo_313x82.png">
</p>

## OCI Network Firewall - TEMPLATE 
This template is based on official Zabbix VMware templates with some changes which allows you to monitor your Oracle Cloud VMware Solution. 

### 🚀 SOME SETUP 
You will have to setup 3 macros after adding the template "VMware" in your "vCenter Host":
* {$VMWARE.URL} = https://<VCENTER_IP OR FQDN>/sdk
* {$VMWARE.USERNAME} = administrator@vsphere.local OR a Service User with Read-Only Permission
* {$VMWARE.PASSWORD} = User Password

### ☕ DISCLAIMER 
This is not an official template and it is focus on give a north of how monitor OCVS with Zabbix. If you need any special ITEM or TRIGGER you should configure by your own.
I will make a best effor to always add new ITEMS here.


### 📝 LICENSE
You are free to use, fork, change and adapt to you own environment.
