# Reblaze REST API

## **Reblaze REST API operations v2.x**

Below are listed the available operations under Reblaze's API. The listings include descriptions, and examples using curl over Bash under Ubuntu 18. 

The parameter $HOST refers to the console FQDN, while $KEY refers to the API key.  

### **Operations**

#### **List Sites**

Lists all sites that are currently set up on the management console. 

| **`curl -s -XGET https://$HOST/api/$KEY/sites/list`** |
| :--- |


#### Duplicate Site

Duplicates/creates new site based on an existing site. You can choose to overwrite the upstream, or use the one that is currently set on the source site. The duplicate site will also create a referring CNAME based on the source site DNS settings.

| **`curl -s -XPOST https://$HOST/api/$KEY/sites/duplicate -d "canonicalname=src.example.com&newdomain=dst.example.com&upstreamhost=8.8.8.8"`** |  |
| :--- | :--- |


#### **Remove Site**

Removes the site from the sites list. This operation also removes the referring CNAME.

| **`curl -s -XGET https://$HOST/api/$KEY/sites/list`** |
| :--- |


#### **Set Names \( Domain aliases \)**

Sets the domains that a site supports. You can add up to 100 domains per site. A domain can also contain wildcards \(e.g, \*.domain.name\).

| **`curl https://$HOST/api/$KEY/sites/setnames --data "canonicalname=src.example.com&names=www.example.com,www2.example.com"`** |
| :--- |


#### **List Upstream**

Lists the upstream settings of a site.

| **`curl https://$HOST/api/$KEY/sites/listupstream?canonicalname=www.example.com`** |
| :--- |


#### **Set Upstream**

Modifies upstream settings. You can add an upstream, change its state, or modify the upstream address. The upstream is a one-line JSON encoded in base64, as shown below. Parameters are described below the code example.

```java
one_line_json='[
  {
    "http_port": "80",
    "https_port": "443",
    "weight": "1",
    "fail_timeout": "10s",
    "monitor_state": "0",
    "down": false,
    "host": "1.2.3.4",
    "max_fails": "1",
    "backup": false
  },
  {
    "http_port": "80",
    "https_port": "443",
    "weight": "1",
    "fail_timeout": "10s",
    "monitor_state": "0",
    "down": false,
    "host": "4.3.2.1",
    "max_fails": "1",
    "backup": false
  }
]'
```

| Argument | Description |
| :--- | :--- |
| **http\_port** | Upstream HTTP listening port |
| **https\_port** | Upstream HTTPS listening port |
| **weight** | The relative weight of the upstream for load-balancing purposes within a farm. Reblaze distributes traffic with a round-robin sequence, according to these weights. For example, if two servers are both set to 'weight=1', they will receive equal amounts of traffic. If the first is set to 'weight=3' while the second is set to 'weight=1', the first server will receive three requests for every single request that the second server receives. |
| **fail\_timeout** | When a server fails, this is the length of time that Reblaze will wait before trying to send traffic to it again. Example: "10s" indicates a fail timeout of 10 seconds. This field uses [TTL Expression Syntax](../../reference-information-1/custom-ttl-values.md). |
| **max\_fails** | The maximum number of failed communication attempts that are allowed for this server. Once this number of failures occurs, Reblaze will consider the server to be inactive. If other servers are available, Reblaze will failover the traffic to them. If this was the only server available, Reblaze will return an error to the client \(either 504 Timeout, or 502 Bad Gateway\). |
| **monitor\_state** | This sets the state for Health Monitoring purposes. \(This does not specify if the server is up or down; it merely sets the current state as if Health Monitoring had just checked the server and returned that state.\) If backup is **true**, then this value should be either "backup\_active" or "backup\_down". If backup is **false**, then this should be 0, or "active\_down." \("active\_down" means the server is supposed to be active, but is down instead.\)  |
| **down** | The state of the server. |
| **backup** | If true, Reblaze will treat this server as a backup. In other words, Reblaze will not attempt to communicate with it unless all the primary servers \(i.e., those for which the Backup setting is not set\) are unavailable. |
| **host** | The server host, as IP/FQDN. |

#### **Encode the json with base64**

| **`one_line_json_base64=$( echo $one_line_json | base64 )`** |
| :--- |


#### **Set the Upstreams**

| **`curl https://$HOST/api/$KEY/sites/setupstream --data "back_hosts=$one_line_json_base64&canonicalname=www.example.com"`** |
| :--- |


#### **Add Certificate**

Adds a new certificate to the [SSL Management](../../product-walkthrough/settings/ssl-management.md). 

| **`curl $API_URL$API_ADD --data-urlencode  "cert_body=$SSL_CRT" --data-urlencode "private_key=$SSL_KEY" | awk '{print $4}' | cut -d '"' -f2`** |
| :--- |


#### **Attach Certificate**

Attaches a domain to a SSL certificate.

| **`curl $API_URL$API_ATTACH --data "canonicalname=$CANONICAL_NAME&sslid=$CERT_ID"`** |
| :--- |


#### **Detach Certificate**

Removes an attached domain from SSL. 

| **`curl $API_URL$API_DETACH --data "canonicalname=$CANONICAL_NAME"`** |
| :--- |


#### **Publish Changes**

| **`curl -XPOST $API_URL$API_PUBLISH`**  |
| :--- |


