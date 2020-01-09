# Secure Traffic from a Third-Party Page

Often, a web application will use external pages. For example, within digital marketing campaigns, it’s common to use landing pages that are provided by a third-party service.

Since these pages are generally hosted by the service provider, they are not directly protected by Reblaze. However, a customer can still use Reblaze to scrub traffic coming from them, and block hostile visitors from affecting the **parent site** \(i.e., the site/application that is using the third-party service\). 

For example, bots can stuff false information into landing-page forms and submit it to the parent site. Reblaze cannot prevent the bots from accessing the third-party landing page. However, it can interdict the form submissions, and prevent them from passing through to the parent site.

Most third-party services allow code to be embedded into their pages. The following process takes advantage of this.

Add the following code to the page \(ideally and if possible, in the page header\):

```text
<iframe src="https://www.example.com/pixel-path" width="0" height="0" style="display:none"></iframe> 
```

Explanation:

* “www.example.com” is your site.  
* “pixel-path” is a **non-existent path**. In other words, the overall address won’t actually resolve to a page or resource within your site.

The purpose of this request is not to return a resource or page; it is merely to trigger a call into the parent site. The call will trigger an active challenge. 

* **If the visitor is a bot, the challenge will fail.** Subsequent access attempts to the parent site \(e.g., form submission attempts by a bot\) will be blocked. 
* **If the visitor is a human, the web browser will receive Reblaze’s authenticating cookies.** Subsequent ****actions by the visitor will include the cookies**,** and will be accepted by Reblaze. 

{% hint style="warning" %}
Note that Reblaze needs to be configured so that active challenges occur on the `pixel-path` URL given above.
{% endhint %}

