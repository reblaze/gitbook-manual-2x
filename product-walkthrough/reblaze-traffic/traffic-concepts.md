---
description: How Reblaze reports on the requests it receives
---

# Traffic Concepts

The Reblaze [Dashboard](dashboard.md) and [View Log](view-log.md) provide intuitive yet very powerful ways of viewing your traffic.

Within those sections, your traffic data is reported in terms of several statistics: 

| Statistic | Comment |
| :--- | :--- |
| **Hits** | Total incoming requests |
| **Humans** | Requests originating from humans. |
| **Bots** | Requests originating from traffic sources not \(yet\) verified to be human. Most of the requestors will be bots, but some will not be. More on this below. |
| **Passed** | Requests accepted by Reblaze and passed upstream to the **origin** \(i.e., the web server, API endpoint, etc.\). |
| **Blocks** | Requests deemed to be hostile, and blocked. |
| **Challenges** | Requests that were challenged. The [challenge process](traffic-concepts.md#the-challenge-process) is an important part of Reblaze's traffic processing, as seen below. |

The Dashboard provides a variety of ways to view your traffic. Most of them do not include all of the above metrics in the same view \(as in the first screenshot below\), but some do \(as in the second screenshot below\).

![This graph shows Hits, Challenges, and Blocked](../../.gitbook/assets/screenshot-2020-01-02-10.55.19.png)

![The Top Sessions view shows all the metrics](../../.gitbook/assets/screenshot-2020-01-02-10.59.10.png)

Reblaze processes "web" requests \(http/s traffic for a web site or application\) differently than API requests from a mobile/native application. Mobile applications have different methods of client authentication, as discussed here: [Mobile SDK](../../using-the-product/reblaze-api-1/mobile-sdk.md). 

The discussion below is for sites and web applications.

## The Challenge Process

Most of the Reblaze interface focuses on configuration for:

* The detection and mitigation of hostile requests.
* The detection and mitigation of hostile behavior of requestors.

The challenge process is different. It is built into Reblaze, and provides a third approach to security. It mitigates threats based on the requestor's identity and environment.

When Reblaze receives the first request from a previously unknown traffic source \(below described as the "user"\), this is the typical process that is followed.

1. **Reblaze challenges the user's browsing environment.** Reblaze uses a variety of proprietary, multi-faceted techniques to verify that this requestor is a human using a browser, instead of a bot using a headless browser or emulator. \(This topic is discussed in some depth in this white paper: [2019 State of Bot Protection](https://www.reblaze.com/resources/white-papers/2019-state-bot-protection/).\)
2. **If the challenge is not passed, the request is suspected to be a bot, and another challenge is issued.** This process continues until a challenge is passed, or a threshold is reached \(e.g., via a Dynamic Rule\) to ban the requestor. 
3. **If the challenge is passed, the browser's session is authenticated**, and the browser receives cookies from Reblaze.
4. **The browser then automatically resubmits the original request**, but this time, the cookies are included. The user is granted access to the requested URL, resources, etc.
5. **Subsequent requests will also include the cookies,** and thus, they are not challenged.

This process happens quickly \(in a few milliseconds\), and is **invisible** to the user.  

{% hint style="info" %}
As noted above, this is the "typical" process that occurs in normal use. There are a variety of situations in which it might not be followed.  For example, sometimes Reblaze is configured to whitelist certain IP addresses, and not to challenge them. 

The discussion below will be based on the typical process described above.
{% endhint %}

## How Requests Are Reflected in Reblaze's Statistics

The process described above will result in the following statistics being incremented.

For each challenge that was not passed:

* **Hits**
* **Challenge**
* **Bots**

If the challenge was passed:

* **Hits** 
* **Challenge**
* **Bots** \(see explanation below\)
* **Hits** \(incremented a second time for the post-challenge resubmission of the request\)
* **Passed**
* **Humans**

## Counting Bots

{% hint style="info" %}
**Within Reblaze, a request that does not have authenticating cookies is counted as a bot.**
{% endhint %}

As a result, the Bot count can sometimes be incremented even when the visitors are humans. Examples:

* When a human user visits a Reblaze-protected site for the first time, **the first request does not yet have the authenticating cookies**. 
* Static files \(images, etc.\) are often exempted from challenges for performance reasons. Direct requests for those URLs from a new visitor will not have cookies.
* Sometimes, trusted IPs are whitelisted and exempted from challenges. They never receive authenticating cookies.

Therefore, although _most_ of the Bot count represents non-human requests to your web application, the Bot metric is not an _exact_ count of this. 

## Relationships of Traffic Metrics

When working with Reblaze's traffic statistics, the following relationships can be helpful.

### **Hits = Passed + Blocked + Challenges**

### **Hits = Humans + Bots**

## Active Challenges versus Passive Challenges

The process described on this page is the **active** challenge process. Out of the box, this is the challenge process that Reblaze uses.

{% hint style="info" %}
**We recommend that whenever possible, customers also enable** _**passive**_ **challenges.** 
{% endhint %}

Passive challenges have three primary benefits:

* **They enable Biometric Bot Detection**: a much more powerful means of identifying automated traffic, and an important part of Reblaze's behavioral analysis.
* **In some situations, active challenges can interfere with certain metrics** such as those provided by Google Analytics. \(The initial referrer information is lost.\) If this is a problem, active challenges can be disabled. In this situation, passive challenges can provide effective bot protection instead. 
* **When caching is being done by a CDN**, active challenges will not occur for pages being served from the cache. Passive challenges are necessary for Reblaze to perform bot detection in this situation.

{% hint style="info" %}
**If possible, we recommend that customers use both active and passive challenges.**
{% endhint %}

To learn more about passive challenges, go here: [Enabling passive challenges. ](../../using-the-product/best-practices/enabling-passive-challenges.md)



