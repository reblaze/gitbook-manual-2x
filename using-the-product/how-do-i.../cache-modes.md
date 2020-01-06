---
description: >-
  as administered in Settings -> Web Proxy -> Application Profiles -> Cache
  Modes
---

# Control Caching Behavior

Web clients can cache resources from a server. Afterwards, a client can access its local cache, which reduces the number of requests sent to the server. 

Servers can instruct clients to implement caching in certain ways. Servers can also set separate caching policies for any intermediary proxies in-between the server and the client.

Reblaze is a proxy between the clients and the **origin** \(the upstream server\). When the origin responds to clients, the outgoing responses pass through Reblaze. You can instruct Reblaze to preserve or alter the caching instructions in those responses.

On the [Application Profiles](../../product-walkthrough/settings/web-proxy/application-profiles.md) page, the **Cache Operation Mode** is where you define Reblaze's caching behavior. There are several aspects to this:

* Whether Reblaze includes caching instructions in the response to the client.
* If so, whether they are the instructions from the origin server, or if Reblaze should override them and send different instructions instead. 
* Whether Reblaze itself caches the response content.

Here are the Cache Operation Modes and their effects.

| **Cache Operation Mode** | Are caching instructions sent to the client? | Are the instructions the same as the origin's? | Does Reblaze cache  response content? | Comments |
| :--- | :--- | :--- | :--- | :--- |
| **Honor Origin** | Yes | Yes | Yes, if the origin says to do so. | Reblaze will comply with the origin, and pass along its caching instructions to the client. |
| **Active Pipe** | Yes | No | Complies with TTL settings   | Reblaze will generate caching instructions for the client in accordance with the Client TTL and CDN TTL settings in the [Application Profiles](../../product-walkthrough/settings/web-proxy/application-profiles.md#overview) section, and will also comply with them itself. |
| **Passive Pipe** | Yes | No | No | Reblaze will generate caching instructions for the client in accordance with the Client TTL and CDN TTL settings in the [Application Profiles](../../product-walkthrough/settings/web-proxy/application-profiles.md#overview) section, but will not store anything itself. |
| **Neutral Pipe** | Yes | Yes | No | Reblaze will pass the origin's caching instructions to the client, without caching anything itself. |
| **Reset Headers** | No | n/a | No | Reblaze will remove all cache headers sent by the origin, and will send the response to the client without any cache directive. |
| **No Cache** | Yes | No | No | Reblaze will send no-cache instructions to the client:  `Cache-Control "max-age=0, no-cache, no-store"` and`Pragma no-cache.` |
| **Private** | Yes | No | Complies with TTL settings | Reblaze will generate caching instructions for the client in accordance with the Client TTL and CDN TTL settings in the [Application Profiles](../../product-walkthrough/settings/web-proxy/application-profiles.md#overview) section, and will also comply with them itself. In addition, the client's instructions will include `Cache-Control private` |

