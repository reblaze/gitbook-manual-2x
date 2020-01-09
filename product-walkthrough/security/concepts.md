---
description: How Reblaze scrubs incoming traffic
---

# Security Section Concepts

When Reblaze receives an incoming request, it decides whether to pass the request through to the upstream server, or block it.

This decision-making is done in several stages. 

![](../../.gitbook/assets/reblaze-stages%20%282%29.png)

| Stage | Comments |
| :--- | :--- |
| **Quarantines and Dynamic Rules** | Traffic from requestors that are currently on the [Banlist](quarantined.md#banlist) or [Blacklist](quarantined.md#blacklist) is blocked. Other requestors are evaluated for potential additional to the Banlist using [Dynamic Rules](dynamic-rules.md). |
| **Static Rules and Rate Limits** | Requests that do not conform to specified size, time, and rate limits are blocked. More information: [Static Rules](static-rules.md) |
| **ACLs** | Filtering based on [Access Control Lists](profiles/acl-policies.md), including [Custom Signatures](profiles/acl-policies.md#custom-signature). |
| **Rate Limits** | Enforces rate limits defined for specific locations/resources within the planet. More information: [Setting Rate Limits for a Location](../settings/web-proxy/security-profiles.md#setting-rate-limits-for-a-location). |
| **Challenges** | Verifies that requests are coming from humans. More information: [The Challenge Process](../reblaze-traffic/traffic-concepts.md#the-challenge-process). |
| **Content Filtering**  | Blocks requests that do not conform to specified rulesets for required or disallowed content. This is the location-based filtering described in [Filtering on Content](../../using-the-product/how-do-i.../filter-by-content.md).  |
| **Argument Analysis** | Examination of characters in arguments. Possible results are to exempt a request from WAF filtering, to send the request to the WAF for inspection, or to block the request. More info: [Args Analysis](args-analysis.md). |
| **WAF/IPS Policies** | Blocks requests that do not conform to the [WAF/IPS Policy](profiles/waf-ips-policies.md) settings. |

Some of the criteria for the decisions are global. In other words, they apply throughout your entire planet. For example, the settings in the [Static Rules](static-rules.md) section are globally applicable, and do not change depending on the context of the request. They will be applied to all traffic for all resources within your planet.

Conversely, some criteria are non-global, and they do depend on the context. For example, you can assign different security rulesets for different resources or locations within your planet. In other words, you can assign different rules to specific domains, subdomains, folders, filetypes, etc. 

These non-global criteria are primarily defined within the [Profiles](profiles/) section. They have their own structure, explained in more detail in that section of this Manual \(see especially the [Profile Concepts](profiles/profile-concepts.md) page\). 

Once Profiles are defined, they are available to be assigned to specific resources/locations within your planet. Those assignments are done in the [Settings-&gt;Web Proxy-&gt;Security Profiles](../settings/web-proxy/) section.

