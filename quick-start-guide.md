---
description: A quick-start guide
---

# Getting Started

## **Welcome to Reblaze!** 

In this section you'll find a quick setup guide to get your **planet** \(i.e., your entire Reblaze deployment, containing all its domains and web applications\) up and running. After completing this section, it's advised to read through the rest of this Manual in order to understand the full capabilities of Reblaze. 

{% hint style="info" %}
Reblaze's support team is always available to assist you. At any step of this process, please feel free to [contact us](support.md).
{% endhint %}

The flowchart below describes the process we are about to begin: 

![](.gitbook/assets/getting-started-with-reblaze-flowchart%20%281%29.png)

## **Login**

The initial login process is as follows:

1. Go to the link provided by Reblaze.  

   `https://example-console.reblaze.com/`

2. Enter the initial login credentials \(in lowercase\), which are: `Username = email`
3. Password: Click on "Reset password" in order to set one.
4. A link will be sent to the provided email address. Click on that link, and on the page that follows, choose and enter a password for your user account.
5. You will be redirected to your console’s Login page. Please enter the email address specified above, and the password you just created. Then, next to the field which says “Reblaze Key OTP,” click on the envelope icon. During your initial setup request, you had provided a mobile phone number; that number will now receive an SMS message with an OTP \(One Time Password\), which you will enter here.
6. Click on the Login button.

After you login into the system, the first screen you will see is the Dashboard. This is the main screen for the Reblaze UI; once traffic statistics are available, they will be displayed here. \(The Dashboard screen is described in-depth [here](product-walkthrough/reblaze-traffic/dashboard.md).\)

Before the Dashboard can show anything, your Reblaze planet must be set up. This is done in the **Settings -&gt; Planet Overview** section.

## **Planet Overview**

To add a new web application to Reblaze, you will duplicate the pre-defined default application.

{% hint style="info" %}
The Reblaze interface does not offer the ability to create a new site or application from scratch, because this process is complicated and error-prone. Instead, you will duplicate the default application and then edit it as needed.
{% endhint %}

Once you choose the right domain for your new application, you'll be redirected automatically to the Web Proxy screen, where configurations are made on the selected application. 

There are two settings to configure, and a third that's optional:

1. Set the IP address of your servers under "Host". 

![](.gitbook/assets/image%20%2839%29.png)

2. Set the Domain Names of your aliases. 

![Setting up Domain Names](.gitbook/assets/image%20%2859%29.png)

3. \(Optional\) Add a command line to redirect all HTTP requests to HTTPS. 

![Command line to redirect all HTTP requests to HTTPS](.gitbook/assets/image%20%2869%29.png)

Before proceeding, click on "Security Profiles" to check for the default settings. These are recommended by Reblaze for initial operation. Further changes are recommended only after taking a careful look at the section discussing "Security Profiles", which you can find [here](product-walkthrough/settings/web-proxy/security-profiles.md). 

Click on "Save Changes" and "Publish Changes" to complete the process.  

{% hint style="info" %}
The deployment will not occur until you click "Publish Changes." In general, whenever you work within the Reblaze interface, saving and publishing is always necessary. More information is here: [Saving and Publishing Changes](using-the-product/best-practices/publish-your-changes.md). 
{% endhint %}

{% hint style="danger" %}
**Don't refresh the page until you get a confirmation that the changes were uploaded to the cloud.** 
{% endhint %}

{% embed url="https://youtu.be/TnB1CTlGAi4" caption="Setting up a new site" %}

{% hint style="info" %}
The discussion above was a short introduction to the initial setup of your planet. For a more in-depth discussion of the Planet Overview page and its options, [click here](https://app.gitbook.com/@reblaze-2/s/product-manual/~/drafts/-LwgrUwGW8ZCtoxKBTrI/product-walkthrough/settings/planet-overview).
{% endhint %}

## Setting up SSL Certificates

All connections between your server and clients must be encrypted. This requires an SSL Certificate to be installed on the web server. Once a certificate is installed, client browsers can connect via HTTPS instead of HTTP. 

With Reblaze, you can either upload an existing certificate into Reblaze, or you can generate a new one for free through the Let's Encrypt service. 

### **Adding an existing SSL Certificate to Reblaze**

1. Add your certificate as explained under [SSL Management](product-walkthrough/settings/ssl-management.md). 
2. Copy the relevant details from the [DNS](product-walkthrough/settings/dns.md) section, and redirect your traffic through Reblaze. \(DNS setup varies widely depending on your current configuration, and this Manual cannot discuss every permutation. [Contact support](support.md) if you need assistance with this.\)
3. Go back to "Planet Overview" and publish your changes as explained previously.  
4. Welcome to Reblaze!

### Generating a new SSL Certificate

1. Copy the relevant details from the [DNS](product-walkthrough/settings/dns.md) section, and redirect your traffic through Reblaze. \(DNS setup varies widely depending on your current configuration, and this Manual cannot discuss every permutation. [Contact support](support.md) if you need assistance with this.\)
2. Create a certificate using the "Gen Cert" button in the [Planet Overview](product-walkthrough/settings/planet-overview.md#generates-new-certificate) section \(see image below\).
3. In the Planet Overview section, publish your changes as explained previously.
4. Welcome to Reblaze!

![Look for &quot;Gen Cert&quot; on the right hand side](.gitbook/assets/image%20%2842%29.png)

{% hint style="info" %}
**The DNS section doesn't exist for marketplace deployments.** 
{% endhint %}

