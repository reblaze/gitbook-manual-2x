---
description: A fundamental part of traffic evaluation
---

# Profile Concepts

As mentioned earlier in [Security Section Concepts](../concepts.md), Reblaze's decision-making can vary depending on the context. In a typical Reblaze deployment, much of the traffic evaluation is done using Profiles. When Reblaze receives a request for web resources, it first determines the Profile that is in effect for the resource that was requested. 

Reblaze's Profiles are hierarchical structures, so that you can set up your security framework in a modular fashion. Rules and collections of rules can be set up once, and re-used throughout your planet as needed.

The hierarchy has several levels:

* **Profile**
* **Policy**
* **Rule**
* **Condition and Operation**

A **Profile** contains one or more Policies. A **Policy** contains one or more Rules. A **Rule** is a combination of a **condition** and an **operation**. Let's illustrate these with examples, from the bottom of the hierarchy upward.

Example **conditions**: 

* Is the request coming from a specific country? Or ASN?
* Is the request coming from a specific IP address?
* Is the request coming from a proxy? Or a VPN? Or a Tor network?
* Is the request for a specific URI?
* Is the request originating from an allowed \(or a disallowed\) HTTP referer?
* Does the request contain \(or not contain\) specific arguments?
* Is the request using \(or not using\) a specific method or protocol?
* Does the request contain \(or not contain\) a query string in a specific format?
* Does the requesting client have \(or not have\) specific cookies, or a specific cookie structure?

Possible **operations**:

* Deny
* Allow
* Bypass \(similar to "Allow", but the request will not be subject to further evaluation or filtering by other rules\)

Example **Rules**:

1. If the requestor IP is within 131.253.24.0/22 \[a known range of Bing crawlers\], _Allow_.
2. If the requestor IP is within 157.55.39.0/24 \[a known range of Bing crawlers\], _Allow_.
3. If the requestor IP is within 1.10.16.0/20 \[a range within the Spamhaus DROP list\], _Deny_.
4. If the requestor IP is within 1.32.128.0/18 \[a range within the Spamhaus DROP list\], _Deny_.
5. If the requestor is a bot, _Deny_.
6. If the requestor is using a proxy anonymizer, _Deny_.
7. If the requestor's Company is \[our company\], _Bypass_.
8. If the requestor submitted an HTTP/S request, _Deny_.   

Example **Policies**:

* Allow Bing Crawlers _\[contains example Rules 1-2 above\]_
* Deny requestors on Spamhaus DROP list _\[contains example Rules 3-4\]_
* Deny bots _\[contains example Rule 5\]_
* Deny proxy users _\[contains example Rule 6\]_
* Allow users from our company _\[contains example rule 7\]_
* Deny all requests _\[contains example rule 8\]_

Example **Profiles**:

* Default: 
  * Allow Bing Crawlers
  * Deny requestors on Spamhaus DROP list
  * Deny bots
  * Deny proxy users
* Private area of our website, for internal use only:
  * Allow users from our company
  * Deny all requests\*\*

\*\* _"Allow" Policies are evaluated before "Deny" Policies. When a match is found, no further evaluation is performed. In this example, company users will be Allowed, which exempts them from the Policy which Denies all requests_.

Note that while Profiles are defined in this section of the Reblaze UI, they are assigned to specific resources in the [Web Proxy -&gt; Security Profiles](../../../product-walkthrough/settings/web-proxy/security-profiles.md#assigning-a-security-profile-to-a-location) section. 

