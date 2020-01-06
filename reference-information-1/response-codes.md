# HTTP Response Codes

HTTP defines forty standard status codes that can be used to convey the results of a client’s request. The status codes are divided into the five categories presented below.  


| CATEGORY | DESCRIPTION |
| :--- | :--- |
| **1xx: Informational** | Indicates that the client's request is being processed. |
| **2xx: Success** | Indicates that the client’s request was accepted successfully. |
| **3xx: Redirection** | Indicates that the client must take some additional action in order to complete their request. |
| **4xx: Client Error** | Indicates an error for which the client is responsible. |
| **5xx: Server Error** | Indicates an error for which the server is responsible. |

Below are examples of the most common HTTP codes you will encounter in the logs:

| HTTP Code | Description |
| :--- | :--- |
| **200** | OK: the standard response for successful HTTP requests. |
| **301** | Used for URL redirection  |
| **400** | Bad Request |
| **401** | Unauthorized—authentication has failed |
| **403** | Forbidden—request refused by Reblaze or origin server |
| **404** | Destination not found |
| **405** | Method not allowed  |
| **408** | Request timeout |
| **413** | Payload too large |
| **414** | Request-URI too long |
| **444** | No Response \(nginx\) |
| **499** | Client Closed Request \(nginx\) |
| **500** | Internal Server Error |
| **503** | Service Unavailable—Server is unable to handle the request  |
| **505** | HTTP version not supported |



