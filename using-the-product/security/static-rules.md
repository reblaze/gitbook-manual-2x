---
description: Constant settings that apply to the entire planet
---

# Static Rules

This section defines security ruleset parameters that apply to your entire Reblaze planet. They are "static" because they are simple settings, and do not vary according to context or circumstance. 

{% hint style="info" %}
The settings in this section are global. They apply to all configured sites on the platform, even if the domain is set to ["Report Mode"](../../product-walkthrough/settings/planet-overview.md#editing-a-web-application).
{% endhint %}

The main page for this section has three tabs: 

* Timeouts
* Sizing
* Speed & Rate

Each tab is discussed in-depth below. 

At the upper right corner of this screen, there is a choice of two different sets of settings: **Default** and **DDoS**. Please ignore the DDoS settings: this mode has been deprecated, and will be removed from a future version of the interface. You should only work with the **Default** settings, since only these settings will be used by Reblaze.  

{% hint style="warning" %}
After working in this section, remember to click on "Save Changes." 
{% endhint %}

{% embed url="https://youtu.be/LQOsj9TbTfs" %}

## Timeouts

The Timeout settings allow the system to monitor the time required to serve resources to each client. Any connection that exceeds the specific limits will be dropped. 

{% hint style="info" %}
**Why timeouts are important**

Some DDoS tools \(e.g., R-U-Dead-Yet, or RUDY\) send a relatively small quantity of traffic requests, but do so as slowly as possible \(often with each byte sent separately\). While a legitimate request can be resolved in milliseconds, a single RUDY machine can tie up server resources for several minutes. Even a few hundred of these machines attacking your server can be very destructive.
{% endhint %}

The Timeout settings allow Reblaze to block unresponsive requestors, whether their unresponsiveness is malicious or not. For most Reblaze deployments, the default timeout settings work very well. They are sufficient to filter out hostile traffic, while still accommodating even those users with low bandwidth.

| Parameter | Timeout |
| :--- | :--- |
| **Header Timeout** | How long to wait for the client to send a request header. |
| **Body Timeout** | If the body is not obtained in one read-step, this timeout begins.  If the timeout expires and the client has still sent nothing, the Reblaze Gateway returns error 'Request time out \(408\)'. |
| **Keep Alive Timeout** | The timeout for keep-alive connections with the client. The Reblaze Gateway will close connections after this time. This setting increases server efficiency; it allows the server to re-use browser connections and save resources.   |
| **Send Timeout**  | Specifies the response timeout to the client. This timeout does not apply to the entire transfer but, rather, only between two subsequent client-read operations. Thus, if the client has not read any data for this amount of time, the Reblaze Gateway shuts down the connection. |

All times are specified in seconds, as shown in the example below. 

![Timeouts Settings Example](../../.gitbook/assets/image%20%28115%29.png)

## Sizing

This tab allows you to place limits on the amount of data that users can upload to the system. ****The defaults usually work well; however, if your application accepts user-generated content or other large files, then changes to these settings might be necessary.

{% hint style="info" %}
Please note that if you increase these settings within Reblaze, then the upstream server should also be configured to accept and store the quantity of data that Reblaze will \(potentially\) pass through.
{% endhint %}

![Default Sizing Example](../../.gitbook/assets/image%20%2843%29.png)

| **Size** | Functionality |
| :--- | :--- |
| **Client’s Body Max Size** | Specifies the maximum accepted body size of a client request, as indicated by the request header Content-Length. Size in MBs.  |
| **Large Client Headers** | Allows additional buffers to be used for large client headers. |

## **Speed & Rate** 

This tab allows you to limit the amount of resources consumed by an IP or individual user. 

Reblaze can limit consumption by the **average** number of requests per second \(the "IP Requests" and "User Requests" settings\), while also allowing temporary **bursts** at a higher rate \("IP Maximum Burst" and "User Maximum Burst"\). 

{% hint style="info" %}
The average and burst limits are more nuanced than is possible to explain in the field labels in the user interface. Please see "[Average and Burst Rate Limiting](static-rules.md#average-and-burst-rate-limiting)" at the bottom of this page for a full explanation.
{% endhint %}

Note that this rate limiting is a global metric across all sites. For example, if one IP address is submitting requests to multiple web applications within a Reblaze planet, all the requests are combined when determining if rate limits have been violated.

<table>
  <thead>
    <tr>
      <th style="text-align:left">IP Parameter</th>
      <th style="text-align:left">Functionality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>IP Requests</b>
      </td>
      <td style="text-align:left">Sets the allowable average request rate per IP, per second.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>IP Maximum Burst</b>
      </td>
      <td style="text-align:left">Sets the allowable additional burst rate per IP, per second. See &quot;Average
        and Burst Rate Limiting&quot; below, for a full explanation.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>IP Concurrent Sessions</b>
      </td>
      <td style="text-align:left">The maximum number of simultaneous sessions per IP. (An HTTP Session ends
        upon a completion of the response sent.)</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Downstream Bandwidth</b>
      </td>
      <td style="text-align:left">
        <p>Downstream bandwidth limitation per response.</p>
        <p>Note: The limit is metered in kilobytes, ie. 1250 KB is equal to 10Mbps.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>User Requests</b>
      </td>
      <td style="text-align:left">Sets the allowable average request rate per user, per second.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>User Maximum Burst</b>
      </td>
      <td style="text-align:left">Sets the allowable additional burst rate per user, per second. See &quot;Average
        and Burst Rate Limiting&quot; below, for a full explanation.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>User Concurrent Sessions</b>
      </td>
      <td style="text-align:left">The maximum number of simultaneous sessions per user.</td>
    </tr>
  </tbody>
</table>Here's an example screenshot:

![Speed &amp; Rate limit example](https://lh5.googleusercontent.com/WAcHG_JvHXynYjY7nBm2-Af0Lkl17uf8TmXI5msYFgMuRO41QDfrWBPHBWOMRqzy81jZr2GIG0subutVJk6O1esxMvh8QvZp4JrP03Z5Sz-Yj8ewvs-z3EUBUKEWP3WJzxqJizZw)

**When a requestor exceeds any of these thresholds, subsequent requests will be answered with error code 503 \(Service Unavailable\).** 

{% hint style="info" %}
For most use cases, the two most important Speed & Rate parameters are IP Requests and IP Maximum Burst. 
{% endhint %}

### Average and Burst Rate Limiting

In the Speed & Rate section, the rate limiting settings can be nonintuitive. Here is an explanation of how they work.

**IP/User Requests** sets the allowable per-second average of incoming requests, enforced on an incremental basis \(where "increment" refers to the number of milliseconds allowed for one request\). **IP/User Maximum Burst** sets a higher per-increment ceiling.

**Example:** IP Requests is set to 100 r/s. Thus, 100 requests are allowed per second. However, the system does not enforce rate limits on a per-second basis; it used a granularity of milliseconds. Therefore, it will allow one request every 10 milliseconds. \(100 r/s, divided by 1000 ms/s, equals 1r/10ms.\) 

Without burst limits—i.e., if IP Maximum Burst is set to zero—the system will reject every request that was received less than 10ms after the previous one.

Now the Reblaze admin sets IP Maximum Burst to 20. This means that Reblaze will accept 21 requests \(1 original plus 20 additional\) per 10 milliseconds. In other words, when a request is received, up to 20 more can be received and accepted within the following 10 ms. If instead 25 total requests are received during that time, the last four requests will be denied with a 503 error. 

