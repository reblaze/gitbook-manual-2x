---
description: Administer the lists of which requestors are banned and/or permitted access
---

# Quarantined

## Overview

The quarantined section will show requestors that have been banned for violation of the [Dynamic Rules](dynamic-rules.md), requestors that have been blacklisted, and requestors that have been whitelisted. You can add and remove requestors, and transfer them among the various lists. 

## Main Display

There are four lists of requestors in this section:

1. **Banlist**
2. **Simulation Banlist**
3. **Blacklist**
4. **Whitelist**

Each is described in more detail below.

For each entry, it's possible to see the following: IP address, origin country, AS number, the violation that was triggered, "CNT/Limit" \(the number of violations compared to the allowable limit\), when the ban began, and when the ban will expire. 

![Quarantined requestors](../../.gitbook/assets/image%20%2821%29.png)

### **Banlist** 

**All requests from these requestors are currently being rejected.** These requestors violated a Dynamic Rule that was set to “Ban” mode. 

### **Simulation Banlist**

**These requestors are NOT having all their requests rejected.** These requestors violated a rule that was set to “Simulated Ban” mode. Simulated Bans are used mainly for testing new rules and seeing how they function, before converting those rules to Ban mode.

### Blacklist

**All requests from these requestors are currently being rejected.** These requestors were placed here by a Reblaze admin.

### Whitelist

**These requestors are exempted from the Dynamic Rules.** For example, even if they violate a rate limit, they will not be banned. 

## Managing Requestors on the Lists

On the right part of the screen is the section menu, invoked via the button with three vertical dots:![](../../.gitbook/assets/screenshot-2020-01-02-16.36.22.png). Depending on context, the section menu will offer the management abilities described below.

## Adding an Entry

#### Banlist and Simulation Banlist

Requestors are added to the Banlist and Simulation Banlist automatically when they violate a Dynamic Rule. 

#### Blacklist and Whitelist

You can add a requestor manually to the Whitelist or Blacklist using the "Add New Entry" option in the section menu. This is demonstrated in the following video:

{% embed url="https://youtu.be/gpxMH3cJAYI" caption="Adding new entry - Example" %}

The fields are:

| Field Name | **Description**  |
| :--- | :--- |
| **Type** | Cookie, Country, ASN, IP, Request Body, Request Header. |
| **Name** | Will appear for specific types: Cookie \(Name\), Headers, etc. |
| **Value** | The value which will activate the blacklisting. For example, when Type is "IP", the blacklistable IP address would be entered here. |
| **Reason** | User description of the reason for adding this entry. |
| **Expiration** | The expiration of the entry, in Hours or Minutes \(only relevant for blacklists\).  |

## Transferring an Entry

Requestors can be transferred among the various lists with this procedure:

1. Select the requestor\(s\) by checking the box at the left of each entry.
2. Open the section menu.
3. Choose the desired "Move to" command \(e.g., "Move to Whitelist"\).

{% hint style="info" %}
Moving an item to the Banlist can only be done from the Simulation Banlist. 
{% endhint %}

## Removing an Entry 

### Automatic Removal

Requestors on the Banlist, Simulation Banlist, or Blacklist will be automatically removed when their expiration time is reached. \(The Whitelist has no expiration time.\)

### Manual Removal 

Requestors can be manually removed from the list they are currently on:

1. Select the requestor\(s\) by checking the box at the left of each entry.
2. Open the section menu by clicking on its button \(![](../../.gitbook/assets/screenshot-2020-01-02-16.36.22.png)\).
3. Choose "Delete".





