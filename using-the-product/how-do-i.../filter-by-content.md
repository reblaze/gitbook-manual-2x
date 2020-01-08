---
description: Blocking requests that do not conform to content policies
---

# Filter by Content

There are several ways to filter requests based on their content.

[Custom Signatures](../../product-walkthrough/security/profiles/acl-policies.md#custom-signature) are a powerful method for specifying content restrictions for traffic. They are included within [ACL Policies](../../product-walkthrough/security/profiles/acl-policies.md), which are used within [Profiles](../../product-walkthrough/security/profiles/), which are assigned to various locations of your site/application at [Settings-&gt;Web Proxy-&gt;Security Profiles](../../product-walkthrough/settings/web-proxy/security-profiles.md).

A more direct method is to [create content filters directly for a location](../../product-walkthrough/settings/web-proxy/security-profiles.md#content-filtering-for-a-location). This too provides powerful filtering capabilities. However, although unlike Custom Signatures and their corresponding ACLs, a location-based filter definition cannot be built and re-used in multiple places throughout the interface. Instead, you have to manually define the filtering conditions for each location.

A third approach is to use [Args Analysis](../../product-walkthrough/security/args-analysis.md), which allows you to whitelist character values for request arguments. 



