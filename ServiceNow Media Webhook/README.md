# Zabbix ServiceNow Media Webhook 

This guide describes how to upgrade existing servicenow webhook with capability such as updating event with Incident Number, URL. Also add functionality to auto-close incident if event got closed. While I am uploading it, I am using Zabbix 6.4 installation.<br>
Please note that recovery and update operations and ServiceNow's custom fields are supported only for trigger-based events.

# ServiceNow Webhook Setup

First to configure ServiceNow webhook, kindly follow [zabbix/zabbix/templates/media/servicenow](https://github.com/zabbix/zabbix/tree/release/6.4/templates/media/servicenow)<br>

## New features we are adding as custum change

1.  Adding Caller Id in Incident while logging ticket in ServiceNow.
2.  Adding CMDB CI in Incident while logging ticket in ServiceNow.
3.  Adding Contact Type in Incident while logging ticket in ServiceNow.
4.  Update ticket as comments if their is any update on event.
5.  Auto close ticket once event has been closed.

## Supported Versions
Zabbix 6.4