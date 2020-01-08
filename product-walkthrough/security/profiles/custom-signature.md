---
description: For creating custom matching conditions
---

# Custom Signature

Custom signatures are custom matching conditions that you can use in Rules and Policies to evaluate client requests.

These allow the administrator to "catch" traffic based on any parameter in the request or the response. They can be used in a number of situations. Some examples:

1. "Virtual patching": Identifying an incoming exploit attempt for a newly-discovered vulnerability in the upstream network.
2. Identifying logged-in admin users, so that their requests can be Bypassed. 
3. Identifying specific patterns of traffic that are suspected to be malicious, so they can be blocked.
4. Identifying specific types of requests \(e.g., XMLHttpRequest\), so they can be blocked from specific sections of a website.

![Custom Signature Section](https://lh3.googleusercontent.com/CWdMkganKGSKsl8_KtpvIhqEgiCIFHC6YFVxfw4rBolpXQzhZUk3Dew5Tbb9mf6wfQHWpuVVS9Btn3jRDdqd5ElFB_2LYwGZAcWlehRCUnBurvmNZFzq2MgQLrWGplacAjgYz6bP)

Signatures that have already been defined are listed in the left column, while you can edit and create new ones on the right. Once a Signature has been created, it will be available in the [New Rule](acl-policies.md#creating-a-new-rule) section within the [ACL Policies](acl-policies.md) tab. 

Custom Signatures give you tremendous power and flexibility for evaluating your traffic. They are composed of one or more matching conditions, which can be combined using Boolean AND/OR operators. 

Each matching condition combines the entries in **Either one of the following fields** and **Is matching with**.

## Possible entries for _Either one of the following fields:_ 

| Field Name  | Description |
| :--- | :--- |
| **Args** | Arguments in the request’s header |
| **Arg Names**  | Argument names in the request’s header |
| **Autonomous System Number \(ASN\)**  | The ASN for a specific entity |
| **Country Name / City** | Geolocation  |
| **Host Name**  | Destination Hostname |
| **Query String** | Regex value inside the query string |
| **Referer** | Referer / Via values |
| **Remote Address** | Client Address in the request |
| **Request Cookies**  | Cookie in the request’s header |
| **Request Cookies Names**  | Cookie names in the request’s header |
| **Request Filename**  | The GET request resource |
| **Request Headers** | Specific headers inside the requests |
| **Request Headers Names**  | Scan the request for specific header values |
| **Request Method**  |  An HTTP method: PUT, POST, GET, etc. |
| **Request Protocol**  | HTTP / HTTPS |
| **Request URI** | The URI of the resource being requested  |
| **User Agent** | The User-Agent of the requestor |

## Entries in _Is matching with_

This text box accepts strings or PCRE \(Perl Compatible Regular Expressions\). 

An explanation and some examples are here: [Pattern Matching Syntax](../../../reference-information-1/pattern-samples.md). 

## Creating custom signatures

When you first create a Signature, one condition appears for editing. If you wish to create more than one, click on the Append Condition button at the bottom. This will add another condition for editing. 

You can continue for as many conditions as you want. The conditions will be evaluated according to the Boolean operator specified by the Condition Type selector. 

