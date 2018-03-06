Installation
------------

### The script itself

This [`chatnhook.sh` script](https://raw.githubusercontent.com/chatnhook/zabbix-alertscript/master/chatnhook.sh) needs to be placed in the `AlertScriptsPath` directory that is specified within the Zabbix servers' configuration file (`zabbix_server.conf`) and must be executable by the user running the zabbix_server binary (usually "zabbix") on the Zabbix server:

	[root@zabbix ~]# grep AlertScriptsPath /etc/zabbix/zabbix_server.conf
	### Option: AlertScriptsPath
	AlertScriptsPath=/usr/local/share/zabbix/alertscripts

	[root@zabbix ~]# ls -lh /usr/local/share/zabbix/alertscripts/chatnhook.sh
	-rwxr-xr-x 1 root root 1.4K Dec 27 13:48 /usr/local/share/zabbix/alertscripts/chatnhook.sh

If you do change `AlertScriptsPath` (or any other values) within `zabbix_server.conf`, a restart of the Zabbix server software is required.

if you have an error that the script cannot be used by zabbix, you can fix this by use the following command `sudo chmod +x chatnhook.sh` to fix the issue.

Configuration
-------------
### Within the Zabbix web interface

When logged in to the Zabbix servers web interface with super-administrator privileges, navigate to the "Administration" tab, access the "Media Types" sub-tab, and click the "Create media type" button.

You need to create a media type as follows:

* **Name**: Chat 'n' Hook
* **Type**: Script
* **Script name**: chatnhook.sh

...and ensure that it is enabled before clicking "Save":

However, on Zabbix 3.x and greater, media types are configured slightly differently and you must explicity define the parameters sent to the `chatnhook.sh` script. On Zabbix 3.x, three script parameters should be added as follows:

* `{ALERT.SUBJECT}`
* `{ALERT.MESSAGE}`

## Add script to user

When logged in to the Zabbix servers web interface with super-administrator privileges, navigate to the "Administration" tab, access the "Users" sub-tab, and make sure under "your user" sub-tab Media click on the "Add" button.

* **Type**: Chat 'n' Hook
* **Send to**: blank
* **when Active**: 1-7,00:00-24:00 (or what you preffer)
* **Use if severity**: your choice
* **Enable**: set enable

## Action

When logged in to the Zabbix servers web interface with super-administrator privileges, navigate to the "Configuration" tab, access the "Actions" sub-tab, and make sure to click on create action right upper corner.

Please configure this to your normal actions, select an action and under suv-tab "operations" click in the "Operations" section on "new" and make sure there is an action filled with send only to "all" or "ChatnHook".



