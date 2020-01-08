---
description: Access Control List Policies
---

# ACL Policies

The ACL Policies section allows you to define [Policies and Rules](profile-concepts.md) by which Reblaze will scrub your incoming traffic. Once the Policies have been defined, they are assigned to specific resources \(e.g., a section of your website\) in the [Web Proxy](../../../product-walkthrough/settings/web-proxy/) section.

In the discussion below, "ACL" and "ACL Policy" refer to the same thing: the Policies that can be administered in this section. 

![Example of an ACL Policy](../../../.gitbook/assets/image%20%2814%29.png)

Existing ACLs are listed on the left. Selecting one will display it in the middle of the screen for editing. 

To create a new ACL, click the "Create New" button toward the top of the screen, then "ACL Policy." Or, duplicate an existing ACL and then edit the newly-created copy.

{% hint style="info" %}
As shown above, Reblaze comes with a default set of ACL Policies. \(They are designated with the Reblaze logo.\)

These Policies are not editable, because they are managed and maintained by Reblaze. They are updated as necessary with no action required on your part. \(Typically these include dynamic elements that need frequent updating—for example, a list of IP addresses with a recent history of malicious activity.\) 
{% endhint %}

Each ACL contains one or more Rules. These are listed in the middle of the screen. To create a new Rule and add it to the current ACL, use the settings on the right part of the screen. \(See below for more on this.\) When you are finished with the Rule setup, click on the Add button. The Rule will be added to the Policy that you are currently defining or editing. 

To remove a Rule from a Policy, click on the "X" to the right of its name. 

## **Creating a New Rule** 

![The Add a Rule section](https://lh4.googleusercontent.com/KIViGQL4voohIwkoJ4U1PnMp5cbQxln0GMsnbUz6eO564bYP4eNIDhNjoPwstNgNAZFjbTee8OeUk0D6o3T-6bJt4dbY0pLfLKUEEzjW-gBeu_aeV-1emNeF3f5mqt6KB7IXn-js)

| Fields | Description |
| :--- | :--- |
| **Operation** | The action that will result when the Rule’s Match condition occurs.   |
| **Match** | The type of parameter that will be tested to see if a Match occurs. |
| **\(unlabeled\)** | The value for the Match condition. |

Each of these fields is explained further below.

### Operation

The Operation field has three possible values:

* **Bypass**: the requestor will be granted access to the requested resource, without further evaluation or filtering of the request. However, although a Bypassed request will not be subject to further filtering, it will still show up in the logs \(as “reason:bypassed”\).
* **Allow**: the requestor will not be presented with a challenge, but will still be evaluated by the WAF.
* **Deny**: the requestor will not be allowed to access to the requested resource

When constructing an ACL Policy from multiple Rules, the Rules are arranged in the hierarchy shown above \(Bypass, then Allow, then Deny\). Rules are evaluated in order from top to bottom. When a Rule resolves to an action, that action is implemented, and further evaluation ceases.

### Match

There are five available options for Match:

* Class
* Company
* Country
* IP Address
* Custom Signature

The first four of these are common matching conditions that are always available. The fifth choice allows you to select custom matching conditions that you constructed by using the [Custom Signature](custom-signature.md) feature.

### Match Argument

This is the third, unlabeled field in the New Rule dialog. The correct entry will depend on the option that was selected for Match.

#### Class

If you selected Class, enter one of these strings as the Match Argument:

* anon-proxy 
* bot 
* cloud 
* tor 
* vpn

#### Company or Country

If you selected either of these, enter the first few characters of the company name or country, and then choose the full name from the list that appears. \(If the text box does not populate itself appropriately as you type the first few characters, check your spelling.\)

#### IP Address

Enter the specific IP or range of IPs \(e.g., 178.184.0.0/16\).

#### Custom Signature

Enter the first few characters of a Signature that you created previously in the [Custom Signature](custom-signature.md) tab, and then choose the one you want from the list that appears. \(If the text box does not populate itself with matching Signatures, check your spelling.\)

### Video demo

{% embed url="https://youtu.be/C0KWA8OtjJQ" caption="Creating an ACL Policy" %}

## Special ACLs

By adding the following characters as a suffix to the ACL's name, the ACL will behave as follows:

| Suffix | Description | Examples |
| :--- | :--- | :--- |
| **OC** | Over-capacity override: ignore [Static Rules](../static-rules.md) rate limits. | Loadtest OC |
| **XDeny** | "God Mode": bypass the Rule Operation hierarchy. | Global DR XDeny |

For an example of using the OC suffix, see [Bypassing Rate Limits for Loadtesting](../../how-do-i.../bypassing-rate-limits-for-loadtesting.md).

For an example of using XDeny, see [Quickly Blocking an Attacker](../../how-do-i.../quickly-blocking-an-attacker.md).

