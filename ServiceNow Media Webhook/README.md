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

## Benefits

Writing benefits as it gives me when i deploy in any project.

1.  For better reporting as it will help me to add custom details to Incident.
2.  Assign Incident to perticular Assignment Group as per team/template/server/item.
3.  You don't have to worry about incident closure in ServiceNow once issue has been resolved because it will be resolved by Zabbix as soon as recovery received on event hence engineer will focus more on tech side instead of process. 
4.  Also TTD & TTR will be accurate which is too hard to calculate in any project.

## Changes need to be done

Below are the steps to do so:

1.  Add some more parameters as per our requirement:<br>
    a.  "caller_id" and pass value with sys_id of User you want to populate in "Caller" field.<br>
    b.  "cmdb_ci" and pass value as "{EVENT.TAGS.cmdb_sysid}". Will configure this tag on hosts to update "Configuration item" field so that we can fetch later how many tickets were logged for this perticular host.<br>
    c.  "contact_type" and pass value with "monitoring" to populate in "Channel" field and it will help us to bifurcate how an incident is coming in ServiceNow.<br>
    d.  "zabbix_auth" and pass value as "{$ZABBIX_AUTHCODE}". Will configure this Global Macro to provide update on event if required. <br>
    e.  "zabbix_zurl" and pass value as "{$ZABBIX_ZURL}". Will configure this Global Macro to provide update on event if required.<br>

![New Parameters](https://github.com/vsbopi/zabbix/blob/fef4f14eb34467bb6660b059cf70482bca027dfe/ServiceNow%20Media%20Webhook/images/image1.png?raw=true)

2.  Configure a API Token in zabbix that will be add as "zabbix_auth".

3.  Go to Global Macros and configure below macros.
![Global Macros](https://github.com/vsbopi/zabbix/blob/003fb9cd62ab1cc88405332490d1abe1e2f28e9e/ServiceNow%20Media%20Webhook/images/image2.png?raw=true)

4.  Now time to configure "cmdb_sysid" tag on hosts so that when an incident logged "Configuration Item" will be updated.
![Host Config](https://github.com/vsbopi/zabbix/blob/b560dadd16a8b7090ace562e95e3aa0f476921eb/ServiceNow%20Media%20Webhook/images/image3.png?raw=true)

Note:- Similarily you can configure Assignment Group as well. Parameter will be and you can pass one more tag that can be tagged on template/host/host group/items etc.

5.  Last and final steps is to replace script with ![Script.js](https://github.com/vsbopi/zabbix/blob/b560dadd16a8b7090ace562e95e3aa0f476921eb/ServiceNow%20Media%20Webhook/Script.js) i have uploaded.
## Supported Versions
Zabbix 6.4