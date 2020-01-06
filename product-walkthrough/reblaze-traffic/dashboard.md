---
description: An overview of traffic activity
---

# Dashboard

After logging into Reblaze, the Dashboard screen is the first screen you'll see. It displays all incoming traffic and what happens to it. By default, this screen shows current activity; by using the archives, you can also 'go back in time' to see previous activity.

The user interface has three main sections: 

1. [Filtering and Time Interval Selection](dashboard.md#filtering-and-time-interval-selection)
2. [Traffic Graphs](dashboard.md#traffic-graphs)
3. ["Top" section](dashboard.md#top-section)

## **Filtering and Time Interval Selection**

### Query Box

Allows you to easily filter the display to show exactly what you want. The structure of a filter is **operator:value**.

For example, to show all traffic from France that was blocked:

`country:France, is:blocked`

{% embed url="https://youtu.be/T4YQvZObcok" %}

For a full explanation of Reblaze's Query box, including operators and syntax, [go here](https://app.gitbook.com/@reblaze-2/s/product-manual/using-the-product/best-practices/reblaze-filter).

### **Time Interval Selection**

Enables the user to select a pre-defined time frame, or a custom time period. See the video below:

{% embed url="https://youtu.be/OWb5QP7CDyk" %}

## Traffic Graphs

### **Passed vs. Blocked**

This section shows the traffic that was processed by Reblaze: that which was passed through to the upstream servers, and that which was blocked. Hits are distributed by time and sorted into three different categories: Humans, Challenges, and Blocked. As you can see in the example below, the data is shown in different colors to easily distinguish among the categories. 

![Passed vs. Blocked Graph](../../.gitbook/assets/image%20%2831%29.png)

### **Response Status**

Counts the number of status codes in a certain time period. 

HTTP Status response codes are divided into five categories:

* **1xx**  - Informational Response 
* **2xx**  - Request Successful 
* **3xx** -  Request For Redirection 
* **4xx**  - Client Error
* **5xx** -  Server Error 

For a detailed list of response codes, [go here](../../reference-information-1/response-codes.md). 

As in the Passed vs. Blocked display, the data is shown in different colors. 

![Incoming traffic sorted by 200, 403, and 503 status codes ](../../.gitbook/assets/image%20%2824%29.png)

### **Requests Count**

The number of network requests during a certain period of time. 

![Requests Count Graph](../../.gitbook/assets/image%20%2880%29.png)

### **Bandwidth**

The downstream bandwidth limitation per response. Left-axis units are "k" for kilobytes, and "M" for megabytes.

![Bandwidth Graph](../../.gitbook/assets/image%20%2879%29.png)

### Latency

This displays the time \(in milliseconds\) consumed by Reblaze's processing. 

![Latency Graph](../../.gitbook/assets/image%20%2898%29.png)

### Zooming in

You can zoom in upon the various graphs, in order to examine a smaller window of time. The video below demonstrates this process.

{% embed url="https://youtu.be/74CIjRAVIp0" %}

## "Top" Section

This section displays traffic statistics according to a variety of "top" metrics: the Top Applications, Top Countries, Top Signatures, etc.

In many of these displays, entries contain links. Clicking on them will open the traffic log, filtered to show the item you selected. For example, in the "Top Countries" view, clicking on a country name will open the traffic log to display the most recent requests originating from that country.

#### **Section Characteristics**

| **Name** | **Description** |
| :--- | :--- |
| **Hits** | Total amount of requests |
| **Passed** | Requests that reached the upstream server |
| **Blocked** | Requests that were blocked by one of Reblaze’s correlation engines. |
| **Humans** | Requests that passed Reblaze's human vs. bot challenge process. |
| **Bots** | Requests with originators that were not \(yet\) verified as humans. For a full explanation, see [Counting Bots](traffic-concepts.md#counting-bots). |
| **Challenges** | Requests that were served with bot detection challenges. |
| **Latency** | How much time it takes for a packet of data to get from one designated point to another. Displayed in milliseconds. |
| **Dn** | Amount of traffic in MB that originated from the upstream server towards the clients. |
| **Up** |  Amount of traffic in MB that originated from the client towards the upstream server. |

### **Applications** 

Shows all protected sites for the current Reblaze deployment. Applications marked in red have a **blockage rate above 30%.** The blockage rate is the ratio of requests blocked by the system to the number of total network requests. 

Note that in this section, "Passed" and "Latency" entries aren't shown, and "Cloud", "Anon." and "Blockage" are added. Their meanings are:

| Name | Description |
| :--- | :--- |
| **Cloud** | Cloud Providers \(GCP, AWS, etc.\) |
| **Anon.** | Anonymous Proxy Browsers |
| **Blockage** | Blockage rate |

![Applications section](../../.gitbook/assets/image%20%2845%29.png)

### **Countries** 

Shows your traffic sorted by country. Each country's flag is shown by its name. 

![Countries section](../../.gitbook/assets/image%20%2837%29.png)

{% hint style="info" %}
**On the screenshots below, IP addresses are censored for privacy reasons.** 
{% endhint %}

### **Sources**

Shows traffic data according to IP address. The ASN \(autonomous system number\) for each IP is also shown.

![Sources Section](../../.gitbook/assets/image%20%2878%29.png)

### **Sessions**

Shows the nature of user sessions. Sessions that pass Reblaze's bot mitigation challenge are identified as originating from humans, and are listed here according to the user's RBZ \(Reblaze\) cookie ID. In the screenshot below, note that the first line shows "-" for the ID. These are sessions that did not pass the challenge. 

![Sessions section](../../.gitbook/assets/image%20%2864%29.png)

### **Targets**

Shows the URLs in your site\(s\) that were accessed the most frequently. 

![Targets Section](../../.gitbook/assets/image%20%2825%29.png)

### **Signatures**

Shows the reasons that traffic was blocked. Unlike other displays, this section does not include hits, passed, blocked, etc.—the counter only shows the number of blocks per signature. Here you can see which types of attacks are most common in your environment. In the example screenshot below, the first entry is "-": this shows requests that were blocked, but not by Reblaze \(i.e., they were blocked "by origin"—by the upstream server\). 

In the example screenshot below, the third and fourth entries include a "ref" value. These are Reblaze reference IDs, [explained here](../../reference-information-1/reblaze-signatures.md).

![Signatures section](../../.gitbook/assets/image%20%2857%29.png)

### **Referers**

Shows the referers that were extracted from the request headers.

![Referers Section](../../.gitbook/assets/image%20%2892%29.png)

### **Extensions**

Allows you to view the various file types that are being used by the application. \("None" shows the network requests that weren't counted as file extensions.\) 

![Extensions section](../../.gitbook/assets/image%20%2812%29.png)

### **Browsers**

Shows all the user agents that initiated requests for the application\(s\).

![Browsers section](../../.gitbook/assets/image%20%2890%29.png)

### **Companies**

Shows all of the ASNs \(Autonomous System Numbers\) from which requests were sent. The ASN can identify individual entities, or larger networks: for example, a telecom provider or a cloud provider.

![Companies Section](../../.gitbook/assets/image%20%286%29.png)

### **Latency**

Shows a list of all applications, with the corresponding latency for each. 

![Latency Section](../../.gitbook/assets/image%20%28109%29.png)

