---
description: Easy-to-use checklists for starting and testing Reblaze
---

# Reblaze Setup Checklists

### Overview <a id="overview"></a>

Please go through these checklists, and verify that their actions have been completed, **both before and after** your traffic is routed through Reblaze. 

There are three checklists below: two for setup, and one for testing.

### Prerequisite

Before going through the checklists below, you should already have performed the actions listed in [Getting Started](quick-start-guide.md).

### **Configuring your environment** 

<table>
  <thead>
    <tr>
      <th style="text-align:left">Item</th>
      <th style="text-align:left">Action</th>
      <th style="text-align:left">More Information</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>Web Server Firewall</p>
        <p>&amp; Hosting Firewall</p>
      </td>
      <td style="text-align:left">Verify that Reblaze IPs are whitelisted in the firewall.</td>
      <td style="text-align:left">Also, please ensure that only Reblaze IPs are able to access your web
        server, i.e. block access for all non-Reblaze IPs. This can be done via
        a set of rules for your firewall, or via .htaccess files.</td>
    </tr>
    <tr>
      <td style="text-align:left">Rate Limits</td>
      <td style="text-align:left">Verify that you&apos;re not using any Rate Limit/QOS rules that apply
        to Reblaze IPs.</td>
      <td style="text-align:left">This avoids potential blacklisting of Reblaze, and other availability
        issues. (If Rate Limits are applied, Reblaze can be misidentified as a
        DDoS source.)</td>
    </tr>
    <tr>
      <td style="text-align:left">Website Cache Settings</td>
      <td style="text-align:left">Ensure that each site/application returns the correct caching instructions.</td>
      <td
      style="text-align:left">You can also <a href="using-the-product/how-do-i.../cache-modes.md">control caching behavior through Reblaze</a>,
        as mentioned below.</td>
    </tr>
  </tbody>
</table>### **Setting up Reblaze** 

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Item </b>
      </th>
      <th style="text-align:left">Action</th>
      <th style="text-align:left">More Information</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Upstream Server</td>
      <td style="text-align:left">Verify that the Web Proxy settings for each domain/site are correct. (These
        settings define where and how Reblaze forwards incoming traffic.)</td>
      <td
      style="text-align:left">Defined via <a href="product-walkthrough/settings/web-proxy/web-proxy-general-settings.md#upstream-servers">Upstream Servers</a> and
        also <a href="product-walkthrough/settings/web-proxy/web-proxy-general-settings.md#proxy-settings">Proxy Settings</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left">SSL</td>
      <td style="text-align:left">Verify that your SSL setup (which should have been performed already,
        as described in <a href="quick-start-guide.md#setting-up-ssl-certificates">Getting Started</a>)
        is complete before routing traffic to Reblaze. (Note that if you want Reblaze
        to generate Let&apos;s Encrypt certificates for you, the traffic must be
        routed to Reblaze before the certificate can be generated.)</td>
      <td style="text-align:left">You can use pre-existing certificates, or generate new ones via Reblaze.
        <a
        href="product-walkthrough/settings/ssl-management.md">More info</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Non- Browser Applications</td>
      <td style="text-align:left">If your application serves bots or other non-browser clients (e.g., monitoring
        services, mobile/native applications using an API, etc.), you will need
        to exempt them from Reblaze&apos;s browser challenges.</td>
      <td style="text-align:left">
        <p>Mobile/native applications are exempted by using the <a href="using-the-product/reblaze-api-1/mobile-sdk.md">Mobile SDK</a>.</p>
        <p></p>
        <p>For other non-browser clients, you should <a href="using-the-product/best-practices/enabling-passive-challenges.md#disabling-active-challenges-optional">disable Active Challenges</a>. <b>It is highly recommended that you </b>
          <a
          href="using-the-product/best-practices/enabling-passive-challenges.md"><b>enable Passive Challenges</b>
            </a><b> </b>to replace them. More info on the overall challenge process is
            <a
            href="product-walkthrough/reblaze-traffic/traffic-concepts.md#the-challenge-process">here</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">HTTPS</td>
      <td style="text-align:left">Enable traffic via HTTPS.</td>
      <td style="text-align:left">Make sure that the <a href="product-walkthrough/settings/web-proxy/web-proxy-general-settings.md#upstream-servers">Proxy Settings</a> are
        configured properly.</td>
    </tr>
    <tr>
      <td style="text-align:left">Block Known Sources</td>
      <td style="text-align:left">Define ACL Policies to reject traffic from sources known to be hostile
        (e.g., IPs, countries, etc.)</td>
      <td style="text-align:left">This is done with <a href="product-walkthrough/security/profiles/">Security Profiles</a> that
        include <a href="product-walkthrough/security/profiles/acl-policies.md">ACL Policies</a> with
        an operation of &quot;Deny&quot;.</td>
    </tr>
    <tr>
      <td style="text-align:left">Whitelist Known Sources</td>
      <td style="text-align:left">Exempt specific traffic sources from inspection and filtering.</td>
      <td
      style="text-align:left">This is done with <a href="product-walkthrough/security/profiles/">Security Profiles</a> that
        include <a href="product-walkthrough/security/profiles/acl-policies.md">ACL Policies</a> with
        an operation of &quot;Allow&quot; or &quot;Bypass&quot;.</td>
    </tr>
    <tr>
      <td style="text-align:left">Web Application Firewall (WAF)</td>
      <td style="text-align:left">Review the default <a href="product-walkthrough/security/profiles/acl-policies.md">ACL Policies</a> and
        <a
        href="product-walkthrough/security/profiles/waf-ips-policies.md">WAF/IPS Policy</a>, to ensure they meet your needs. Define new ones if
          necessary.</td>
      <td style="text-align:left">The Policies are included in one or more <a href="product-walkthrough/security/profiles/">Security Profiles</a>,
        which are then assigned to appropriate locations within your site <a href="product-walkthrough/settings/web-proxy/security-profiles.md">as explained here</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left">DDoS Settings (Rate Limits)</td>
      <td style="text-align:left">Review the <a href="product-walkthrough/security/static-rules.md">global rate limits</a> to
        ensure they match your site&apos;s capacity. For most use cases, the default
        settings should work well.</td>
      <td style="text-align:left">In addition to the general rate limits, it&apos;s also possible to define
        limits for specific site locations and/or traffic sources. <a href="using-the-product/how-do-i.../set-rate-limits.md">More info about this</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Cache Settings</td>
      <td style="text-align:left">Review the applications&apos; cache settings in their <a href="product-walkthrough/settings/web-proxy/application-profiles.md">Application Profiles</a>.</td>
      <td
      style="text-align:left">Reblaze has a variety of caching options. Its settings are explained
        <a
        href="using-the-product/how-do-i.../cache-modes.md">here</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Alerts</td>
      <td style="text-align:left">Review and customize alerts and notifications according to your needs.</td>
      <td
      style="text-align:left"><a href="https://app.gitbook.com/@reblaze-2/s/product-manual/~/drafts/-LyOyZcCv0r35mSbCJs1/product-walkthrough/settings/planet-overview#notification-and-alert-settings">More info about this</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Account</td>
      <td style="text-align:left">Review your <a href="product-walkthrough/settings/account.md">account settings</a> to
        ensure they are correct.</td>
      <td style="text-align:left">Sometimes new customers enter placeholder values at first. Ideally, correct
        values would be in place by the time Reblaze is active.</td>
    </tr>
  </tbody>
</table>### **Testing your setup** 

When the following checklist has been completed, you'll be ready to go. 

{% hint style="info" %}
Note: by default, **Reblaze is deployed in** [**Report mode**](product-walkthrough/settings/web-proxy/security-profiles.md#enabling-report-only-mode) for all applications. In this mode, it will not block traffic; it merely reports on the traffic it would have blocked, if that application had been set to Active mode. 
{% endhint %}

<table>
  <thead>
    <tr>
      <th style="text-align:left">Item</th>
      <th style="text-align:left">What to verify</th>
      <th style="text-align:left">More Information</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Check DNS</td>
      <td style="text-align:left">
        <p>Run a DNS query for the website, and validate that the DNS records of
          the HTTP/S services are pointing to Reblaze CNAME /IPs only.</p>
        <p></p>
      </td>
      <td style="text-align:left">You can use tools such as <a href="https://dnschecker.org/">https://dnschecker.org/</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Test Traffic</td>
      <td style="text-align:left">Generate traffic to your site, and verify that it is being displayed in
        the <a href="product-walkthrough/reblaze-traffic/dashboard.md">Dashboard</a>.
        For more in-depth traffic inspection, you can use the <a href="product-walkthrough/reblaze-traffic/view-log.md">View Log</a>.
        If SSL traffic is used, use your web browser to validate that the right
        certificate is being used.</td>
      <td style="text-align:left">Both the Dashboard and View Log include a Query box to filter their displays.
        Here&apos;s <a href="using-the-product/best-practices/reblaze-filter.md">how to use the Reblaze Query Box</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Test Non-Browser Clients</td>
      <td style="text-align:left">If applicable, generate and test traffic from non-browser clients, and
        verify via the Dashboard that the requests are not blocked/reported.</td>
      <td
      style="text-align:left">This is to validate the (optional) settings configured for non-browser
        clients, as described in the checklist above.</td>
    </tr>
    <tr>
      <td style="text-align:left">Monitor and Optimize Settings</td>
      <td style="text-align:left">As traffic is processed by Reblaze, review the Dashboard (and ideally,
        the View Log) to see the decisions that are being made. Optimize Reblaze
        until it is performing as expected. Once you are satisfied with Reblaze&apos;s
        traffic scrubbing, <a href="product-walkthrough/settings/web-proxy/security-profiles.md#enabling-report-only-mode">move your application(s) from Report mode to Active mode</a>.</td>
      <td
      style="text-align:left">Reblaze&apos;s logs are a rich source of insights into incoming traffic.
        Highly recommended reading: <a href="using-the-product/best-practices/dealing-with-false-positive.md">Understanding and Diagnosing Traffic Issues. </a>
        </td>
    </tr>
  </tbody>
</table>