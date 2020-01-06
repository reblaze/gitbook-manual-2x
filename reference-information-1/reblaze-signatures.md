# Reblaze Signatures

### **Introduction** 

The Reblaze system blocks traffic if it matches configured WAF signatures, exceeds triggering thresholds, matches ACL rules, or violates RFC specifications. When a blocking event occurs, Reblaze reports it according to reference IDs.

The reference IDs are listed below, categorized into groups according to their description. In some cases, external links are included with more details on the specific type of attack being described.

### **WAF Signatures**

#### Operating System Command Injection \(OSCI\)

OSCI attacks are aimed at the operating system. The attacker seeks to manipulate the operation of the system, or to take control completely. For example, an attacker might attempt to get the content of OS files such as /etc/shadow. An OCSI attack can be included in the request headers, arguments, or cookies. More details on this type of attack can be found on the [OWASP website](https://www.owasp.org/index.php/Command_Injection). 

**Reblaze reference ID 400000-499999**

#### Remote File Inclusion \(**RFI\)**

RFI attacks target applications that allow scripts to be included in files. These attacks are typically used for planting backdoors. [Here's an example of an RFI attack using PHP.](https://www.owasp.org/index.php/PHP_File_Inclusion)

**Reblaze reference ID 300000-399999**

#### Local File Inclusion \(**LFI\)** 

An LFI attack is similar to RFI, but it includes one or more local files instead of remote links. The attacker seeks to upload a file to the server. [Read more about LFI](https://www.owasp.org/index.php/Testing_for_Local_File_Inclusion).

**Reblaze reference ID 300000-399999**  


#### SQL Injection \(**SQLi\)**

Threat actors use SQL injection to attack databases by executing SQL commands. SQLi is a common attack, with many possible ways for attackers to exploit vulnerabilities. [Read more about SQLi.](https://www.owasp.org/index.php/SQL_Injection) 

**Reblaze reference ID 1000000-1999999**  


#### Cross-Site Scripting \(**XSS\)**

XSS attacks are a type of injection, in which malicious scripts are injected into otherwise benign and trusted sites and applications. [Read more about XSS](https://www.owasp.org/index.php/Cross-site_Scripting_%28XSS%29).

**Reblaze reference ID 2000000-2999999**  


#### **Generic Attacks**

Many attacks take advantage of vulnerabilities in the OS or in the targeted application, without falling into one of the more prominent categories. Reblaze classifies them into this “generic” category.

**Reblaze reference ID 3000000-3999999**  


#### **RFC2616 rule check violation**

This signature refers to a violation of HTTP protocol RFC-2616. For example, [the RFC requires requests to contain a content-length header](https://tools.ietf.org/html/rfc2616#section-14.13); a request that does not include one violates the RFC.

**Reblaze reference ID 3000000-3999999**  


#### **Known malicious bot**

This signature refers to the recognition of user-agent headers of known attack tools and applications: for example, the “Grabber” vulnerability scanner. 

**Reblaze reference ID 3000000-3999999**

\*\*\*\*

#### **PHP Eval/Exec**

This attack is sometimes referred to as Direct Dynamic Code Evaluation. It exploits an application that does not properly validate user inputs. More information can be found at [OWASP here](https://www.owasp.org/index.php/Direct_Dynamic_Code_Evaluation_%28%27Eval_Injection%27%29).  
****

#### **Over-capacity**

Reblaze blocks requests when a capacity threshold is exceeded: for example, the number of requests per second from a single IP. Usually, these thresholds reflect Reblaze’s DDoS protection. However, in some cases, some of this may be coming from the upstream server rather than Reblaze; in this situation, a “by origin” is added to the event description in the logs. 

**Reblaze reference ID: None. This block results in HTTP error 503.**  


#### **Unrecognised Host Header**

Reblaze blocks headers for any site not found in its list of configured sites: for example, a proxy request. \(This includes IP addresses as well.\) Only FQDN \(fully qualified domain names\) are allowed.

**Reblaze reference ID: None**  


#### **Multiple encoding detected**

A common penetration technique is to encode a hostile request multiple times \(for example, URL encode and base64\), in an attempt to evade detection and filtering by the WAF or other security measures. [Read more about multiple encoding attacks here](https://www.owasp.org/index.php/Double_Encoding).

**Reblaze reference ID: 8888001**  


#### **Challenge**

This refers to requests that are blocked because they fail Reblaze’s bot/human detection challenges.

#### **Autoban/etc**

This refers to traffic that is blocked by the application. It does not include categories such as HTTP errors 400, 408 or 500.

#### **ACL-IP**

A blocking event that resulted from an ACL containing an IP or subnet.

#### **ACL-Geo**

A blocking event that resulted from an ACL containing an IP or subnet that matched geographical criteria.

#### **ACL-Anonymizer**

A blocking event that resulted from an ACL containing an IP or subnet that is part of an anonymous proxy provider.

#### **ACL-TOR**

A blocking event that resulted from an ACL containing an IP or subnet found on a list of TOR gateways.

#### **ACL-VPN**

A blocking event that resulted from an ACL containing an IP or subnet known to be used by a VPN provider.

#### **ACL-ASNum**

A blocking event that resulted from an ACL containing an IP or subnet from a specified AS number.

#### **ACL-Cloud** 

A blocking event that resulted from an ACL containing an IP or subnet known to be used by a cloud provider. 

#### **Method not allowed**

A request was rejected because it contained an HTTP method that the WAF was configured to reject. For example, a common configuration is to accept HEAD, GET, and POST requests, while rejecting all others.

#### **x-denied@acl-custom-sig**

A violator blocked by the ban list \(via a Dynamic Rule\).

#### **bypassed@dpi-max-length**

When a request’s payload exceeds the configured threshold, the WAF signatures are bypassed. This mechanism ensures that the WAF will not loop forever and consume 100% of the CPU.

### **Rate limit Signatures**

#### **Custom naming**  

This blocking event occurs when rate limits are triggered. The text is taken from the name of the rule that triggered the event.

#### **IP in rate limit whitelist**

This message notes that the IP is in the rate limit whitelist ACL.

#### **Org in rate limit whitelist** 

This message notes that this organization’s AS number is in the rate limit whitelist ACL.  
****

