# Secure Traffic from a Third-Party Page

Often, a web application will use external pages. For example, within digital marketing campaigns, it’s common to use landing pages that are provided by a third-party service.

Since these pages are generally hosted by the service provider, they are not directly protected by Reblaze. However, a customer can still use Reblaze to scrub traffic coming from them, and block hostile visitors from affecting the **parent site** \(i.e., the site/application that is using the third-party service\). 

For example, bots can stuff false information into landing-page forms and submit it to the parent site. Reblaze cannot prevent the bots from accessing the landing page. However, it can interdict the form submissions, and prevent them from passing through to the parent site.

Most third-party services allow code to be embedded into their pages. The following two-step process takes advantage of this.

1. Enable passive challenges for the page.
2. Enable active challenges for the page.

## Enable passive challenges for the page

With one exception \(noted below\), follow the same procedures described in [Enabling Passive Challenges](../best-practices/enabling-passive-challenges.md), and apply them to the third-party page.

**The exception:** instead of including a root-path URL \(`<script src="/c3650cdf…` \), you must include the full path \(`<script src="`[`https://www.example.com/c3650cdf…`](https://www.example.com/c3650cdf…) \).

{% hint style="info" %}
Note that this is the full path to **your** site, not the domain of the third-party service provider.
{% endhint %}

## Enable active challenges for the page

This is done by including the following code in the page \(ideally, in the page header\):

```text
<iframe src="https://www.example.com/pixel-path" width="0" height="0" style="display:none"></iframe> 
```

Explanation:

* “www.example.com” is your site. It must be the same full path \(and the same subdomain\) as used in the passive challenge procedure described above. 
* “pixel-path” is a **non-existent path**. In other words, the overall address won’t actually resolve to a page or resource within your site.

The purpose of this request is not to return a resource or page; it is merely to trigger a call into the parent site. The call will trigger an active challenge. 

* **If the visitor is a bot, the challenge will fail.** Subsequent access attempts to the parent site \(e.g., form submission attempts\) will be blocked. 
* **If the visitor is a human, the web browser will receive Reblaze’s authenticating cookies.** Subsequent ****actions by the visitor within the site will include the cookies**,** and the visitor will not be challenged anymore. 

