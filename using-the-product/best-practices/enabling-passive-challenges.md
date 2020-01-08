# Enabling Passive Challenges

As described in [Traffic Concepts](../../product-walkthrough/reblaze-traffic/traffic-concepts.md), out of the box Reblaze includes an **Active Challenge** process. This is very useful in distinguishing humans from bots.

Active Challenges work well, but an even better option is **Passive Challenges**. 

* Active Challenges temporarily redirect the user's browser. This can affect site metrics gathered by products such as Google Analytics. 
* Passive Challenges are simple pieces of Javascript. They do not redirect the user's browser; they merely ask it to solve a challenge, and then insert the Reblaze cookies.

Most importantly, Passive Challenges allow Reblaze to use Biometric Bot Detection—an advanced and sophisticated means of distinguishing humans from automated traffic sources.

## Biometric Bot Detection

With Biometric Bot Detection, Reblaze continually gathers and analyzes stats such as client-side I/O events, triggered by the user’s keyboard, mouse, scroll, touch, zoom, device orientation, movements, and more. Based on these metrics, the platform uses Machine Learning to construct and maintain behavioral profiles of legitimate human visitors. Reblaze learns and understands how actual humans interact with the web apps it is protecting. Continuous multivariate analysis verifies that each user is indeed conforming to expected behavioral patterns, and is thus a human user with legitimate intentions.

{% hint style="info" %}
**We recommend that all customers enable Passive Challenges** if it is possible to do so. Biometric Bot Detection provides much more robust detection of automated traffic than is possible without it.
{% endhint %}

## Implementation

Implementing Passive Challenges is simple. Place this Javascript code within the pages of your web applications:

```text
<script src="/c3650cdf-216a-4ba2-80b0-9d6c540b105e58d2670b-ea0f-484e-b88c-0e2c1499ec9bd71e4b42-8570-44e3-89b6-845326fa43b6" type="text/javascript"></script>
```

{% hint style="info" %}
The code snippet can go into the header or the footer. **The best practice is to place it within the header.** This ensures that subsequent calls contain authenticating cookies.
{% endhint %}

{% hint style="info" %}
**Most customers set up the code snippet as a tag within their tag manager.** This makes it simple to install it instantly across their entire site/application.
{% endhint %}

## Testing

To test the implementation, use a browser to visit a page containing the Javascript snippet. Once it runs, the browser should have a cookie named **rbzid**.

## Disabling Active Challenges \(Optional\)

If you wish to turn off Active Challenges, remove the default "**Deny Bot**" [ACL Policy](../security/profiles/acl-policies.md) from all active [Profiles](../security/profiles/).

{% hint style="info" %}
This will turn off the direct blocking of bots \(where a requestor is blocked merely for being identified as a bot\). However, automated traffic will still be excluded via all other relevant means: the active [ACL Policies](../security/profiles/acl-policies.md), [Dynamic Rules](../security/dynamic-rules.md), [content filtering](../how-do-i.../filter-by-content.md), and so on.
{% endhint %}

{% hint style="danger" %}
**If you have not enabled Passive Challenges** \(and successfully tested them\), disabling Active Challenges is not recommended.
{% endhint %}

