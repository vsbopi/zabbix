# Zabbix ServiceNow Webhook Upgrade Guide

## Overview

This guide provides instructions for enhancing your existing ServiceNow webhook with additional features, such as updating events with Incident Number and URL, and auto-closing incidents upon event resolution. These enhancements are tailored for Zabbix 6.4 installations.

## ServiceNow Webhook Configuration

To configure the ServiceNow webhook, follow the instructions provided in [zabbix/zabbix/templates/media/servicenow](https://github.com/zabbix/zabbix/tree/release/6.4/templates/media/servicenow).

## New Custom Changes

We're introducing the following enhancements:

1. **Caller ID Addition:** Incorporate the Caller ID when logging tickets in ServiceNow.
2. **CMDB CI Inclusion:** Add CMDB CI details to incidents for better tracking.
3. **Contact Type Specification:** Include the Contact Type in incidents for classification.
4. **Ticket Updates:** Update tickets with event changes via comments.
5. **Auto-Closure:** Automatically close tickets when events are resolved.

## Benefits

Deploying these enhancements offers several advantages:

1. **Enhanced Reporting:** Custom details improve incident documentation.
2. **Targeted Assignments:** Assign incidents to specific groups based on criteria.
3. **Streamlined Process:** Automating incident closure frees up engineers for technical tasks.
4. **Accurate Metrics:** Time to Detect (TTD) and Time to Resolve (TTR) metrics become more reliable.

## Required Changes

Follow these steps to implement the upgrades:

1. **Additional Parameters:** Introduce new parameters as needed:
   - **caller_id:** Provide the sys_id of the user for the Caller field.
   - **cmdb_ci:** Utilize {EVENT.TAGS.sysid} to populate the Configuration Item field.
   - **contact_type:** Set as "monitoring" for Channel field classification.
   - **zabbix_auth:** Use {$ZABBIX_AUTHCODE} to authenticate event updates.
   - **zabbix_zurl:** Incorporate {$ZABBIX_ZURL} for event update URLs.

![New Parameters](https://github.com/vsbopi/zabbix/blob/fef4f14eb34467bb6660b059cf70482bca027dfe/ServiceNow%20Media%20Webhook/images/image1.png?raw=true)

2. **API Token Configuration:** Set up an API Token in Zabbix for zabbix_auth.

3. **Global Macros Configuration:** Configure the following macros in Global Macros.

![Global Macros](https://github.com/vsbopi/zabbix/blob/003fb9cd62ab1cc88405332490d1abe1e2f28e9e/ServiceNow%20Media%20Webhook/images/image2.png?raw=true)

4. **Host Configuration:** Add the "sysid" tag to hosts for updating the Configuration Item when an incident is logged.

![Host Config](https://github.com/vsbopi/zabbix/blob/7e58910af5048474aa6362d4322a1360bfde1e2f/ServiceNow%20Media%20Webhook/images/image3.png?raw=true)

5. **Script Replacement:** Replace the existing script with the one provided in [Script.js](https://github.com/vsbopi/zabbix/blob/b560dadd16a8b7090ace562e95e3aa0f476921eb/ServiceNow%20Media%20Webhook/Script.js).

## Supported Versions

These upgrades are compatible with Zabbix version 6.4.
