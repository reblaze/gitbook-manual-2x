---
description: Restricting consumption of resources and rate of requests
---

# Set Rate Limits

Different types of rate limits are defined in different parts of the Reblaze interface.

**Global:** The [Static Rules -&gt; Speed & Rate](../../product-walkthrough/security/static-rules.md#speed-and-rate) settings apply to your entire planet.

**By location:** Rate limits for specific locations/URLs can be created by defining the locations within [Web Proxy -&gt; Security Profiles](../../product-walkthrough/settings/web-proxy/security-profiles.md#managing-locations), and selecting "More" at the end of each location's entry in the list. See full explanation here: [Setting Rate Limits for a Location](../../product-walkthrough/settings/web-proxy/security-profiles.md#setting-rate-limits-for-a-location). 

**By traffic source:** Requestors who are submitting excessive requests can be banned for configured lengths of time. This can be done via [Dynamic Rules](../../product-walkthrough/security/dynamic-rules.md). 

## Creating Rate Limiting Exemptions

Creating exemptions from rate limits is done differently, depending on the scope of the rate limits being addressed.

**Global:** Create an [ACL Policy with an OC suffix](../../product-walkthrough/security/profiles/acl-policies.md#special-acls).

**By location:** Create an [ACL Policy](../../product-walkthrough/security/profiles/acl-policies.md) with the name "**Rate Limit Whitelist**". This can exempt any combination of IP, Country, and ASN. The Policy should then be included in a [Profile](../../product-walkthrough/security/profiles/), and the Profile should be [assigned](../../product-walkthrough/settings/web-proxy/security-profiles.md#assigning-a-security-profile-to-a-location) to the appropriate location\(s\)  or portions of your site/application. Example:

![An ACL with this name will exempt the traffic sources from rate limiting for the specific location](../../.gitbook/assets/rate-limit-whitelist%20%281%29.png)

**By traffic source:** A traffic source can be exempted from Dynamic Rule filtering either by [adding an Ignore parameter to the Rule itself](../../product-walkthrough/security/dynamic-rules.md#dynamic-rule-settings), or by adding the traffic source to the [Whitelist within the Quarantine section](../../product-walkthrough/security/quarantined.md#whitelist).





