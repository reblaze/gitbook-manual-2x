---
description: Administration of built-in Security Policy modules
---

# WAF/IPS Policies

Along with its [ACL Policies](acl-policies.md), Reblaze includes WAF/IPS Policies. This section allows you to administer them.

Just like ACL Policies, WAF/IPS Policies are included in [Profiles](./). Unlike ACL Policies, a Profile cannot contain more than one WAF/IPS Policy.

![WAF/IPS Policies Screen](https://lh5.googleusercontent.com/1Fi8pzOZAav1DQo4g7U6t2WtD1uni1K21f5_AQJtsdDJD_YbpP8npfXvzQjxizjamtebuQanXtuTXxTc_S70QGf3IeOmEpA7NaujpHhOXJcM4xbHS2Tq4kOtf0RW37WcznmkmB7q)

Existing WAF/IPS Policies are listed on the left side; selecting one will display its contents on the right for editing.  

When viewing or editing a WAF/IPS Policy, the Active Modules section allows you to enable/disable some of the modules. The four on the left are always active and cannot be turned off. \(However, an ACL Policy that resolves to an action of **Bypass** will exempt a requestor from them.\) These four modules are: 

| **Parameter** | Functionality |
| :--- | :--- |
| **Essential Headers Checkup** | A request without a header is illegitimate \(and generally is an indication of a bot\). This module blocks these requests.  |
| **HTTP Methods** | This module enforces the Allowed HTTP Methods that are defined in the list farther down the page.  |
| **Argument Limitations** | This module enforces the Request Arguments Limitations that are specified below the list of Allowed HTTP Methods.  |
| **RFC Compliance** | This module ensures that every request is RFC compliant. Most penetration tools are non-compliant \(often deliberately so\)—thus, this module alone defeats and excludes a high amount of hostile traffic.  |

The next three modules are optional, but are recommended in most situations: 

| **Parameter** | Functionality |
| :--- | :--- |
| **Bad Robots** | Identifies and blocks malevolent bots, based on their user agents. This works differently than the default **Deny Bot** ACL Policy, which uses active challenges to identify bots. Therefore, when active challenges are disabled, this WAF capability can still be used.  |
| **Dual Encoding** | A common penetration technique is to encode a hostile request multiple times, in an attempt to evade detection and filtering. For example, an injection attack might be encoded in binary, and then sent as if it were plain text. Or, different types of encoding might be mixed together in the same request. This module detects and defeats these attempted attacks. |
| **\* Injection Proof** | This module detects and defeats different kinds of injection attacks: SQL, XSS, and OSC. \(The "\*" is a wildcard.\) |

Below the modules is the list of **Allowed HTTP Methods**. In general, you should enable as few of these as possible, and then disable the rest. 

Sometimes there are methods that are used only by a few specific users. A possible approach for this situation is to disable those methods here, and then define ACL Policies or Signatures by which those specific users are Bypassed from being blocked by this module. This strategy works, but it should only be done in deployments where the specific users can be reliably identified. 

At the bottom of the page are the **Request Arguments Limitations**, **Whitelist Argument Names**, and **Whitelist Rule IDs**. These allow you to permit or deny requests based on the arguments contained in the request. For assistance with these entries, please [contact support](../../../support.md).

![Request Arguments Limitations Section](https://lh6.googleusercontent.com/iAmfXAX0SVqw4X5kHin6Xucepa7ZcLq-P_hx_EEKI8BDbvGV5ONpu2HygmmtEtjr1Zbt0h9NmYKHe06TQYRtylxCmmH53IPsCvLVP0vwENBVfTH2EbXjDUh4UevsiDpqSeOCO2Rb)

