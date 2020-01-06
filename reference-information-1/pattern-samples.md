---
description: used for specifying matching conditions
---

# Pattern Matching Syntax

Within the Reblaze interface, there are several features that require matching conditions to be specified. 

The text boxes accept strings or PCRE \(Perl Compatible Regular Expressions\). If you are unsure of PCRE syntax, you can test your expression at sites such as [https://regex101.com](https://regex101.com), which will show you how it will be parsed. 

Below are some examples of syntax for specifying matching patterns.

| Functionality | Syntax | Remarks |
| :--- | :--- | :--- |
| Match **/Images/** or **/images/** or **/IMAGES/** | `~* /images/` | Case insensitive, regular expression matching. |
| Match URLs that ends with **.DOC** or **.PDF** | `~ \.(DOC|PDF)$` | Case _sensitive_, regular expression matching. |
| Match URLs that ends with **.gif** or **.jpg** | `~* \.(gif|jpg)$` | Case _insensitive_, regular expression matching. |
| Match _exact_ URL, e.g. Root **/** or **/admin** | `= /` or `= /admin` | Searching stops immediately \(this match is top priority\). |
| Match all URLs starting with **/documents/** | `/documents/` | System will continue search for a regular expression match. This will be matched only if none will be found. |
| Prioritize URLs starting with **/documents/** | `^~ /documents/` | **^~** means - match and halt searching, i.e. regular expressions will not be checked. |
| Match 'entire site' \(anything else\) | `/` | Matches any URL since all begins with "/". However, regular expressions and longer entries will take priority. |

A common pattern is for matching all static content. This pattern in full is:

```text
~* \.(gcur|htc|aif|aiff|au|avi|bin|bmp|cab|cct|cdf|class|doc|dcr|dtd|exe|flv|gcf|gff|gif|grv|hdml|hqx|ico|ini|jpeg|jpg|js|mov|mp3|nc|pct|pdf|png|ppc|pws|swa|swf|txt|vbs|w32|wav|wbmp|wml|wmlc|wmls|xsd|zip|webp|jxr|hdp|wdp|bz2|map|ttf|ttc|otf|eot|woff|css)$
```



