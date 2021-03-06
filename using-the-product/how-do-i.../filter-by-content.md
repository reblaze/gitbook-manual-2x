---
description: Blocking requests that do not conform to content policies
---

# Filter by Content

There are several ways to filter requests based on their content.

[Custom Signatures](../../product-walkthrough/security/profiles/acl-policies.md#custom-signature) are a powerful method for specifying content restrictions for traffic. They are included within [ACL Policies](../../product-walkthrough/security/profiles/acl-policies.md), which are used within [Profiles](../../product-walkthrough/security/profiles/), which are assigned to various locations of your site/application at [Settings-&gt;Web Proxy-&gt;Security Profiles](../../product-walkthrough/settings/web-proxy/security-profiles.md).

A more direct method is to [create content filters directly for a location](../../product-walkthrough/settings/web-proxy/security-profiles.md#content-filtering-for-a-location). This too provides powerful filtering capabilities. Here's a comparison between this and Custom Signatures.

* Both can deny requests based on their content.
* **Location-based filtering makes it easier to** _**require**_ **certain content in incoming requests.**
* Location-based filtering is simpler when setting up different filters for different locations. 
* Custom Signatures are modular, and once defined, they can be re-used in multiple places throughout the interface. A location-based filter definition cannot do this. Instead, you have to manually define the filtering conditions for each location.

[Dynamic Rules](../../product-walkthrough/security/dynamic-rules.md) can be used to rate-limit a requestor, based on the content that is requested.

[Args Analysis](../../product-walkthrough/security/args-analysis.md) examines the characters found in arguments. Depending on its mode, it can block requests if unexpected characters are found, or pass them on to the WAF for further inspection. It can also act as an inverse content filter; those requests with arguments which contain only whitelisted characters can bypass WAF filtering. 



