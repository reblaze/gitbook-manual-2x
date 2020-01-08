# Quickly Block an Attacker

Sometimes [ACL Policies](../../product-walkthrough/security/profiles/acl-policies.md) can make it difficult to find and block a specific attacker.

For example, let's say an ACL Policy \(named "Allow US Traffic"\) for an ecommerce store allows all traffic originating from the United States. But then an attacker, using an IP within the US, begins to scrape prices and other data from the store. 

If an ACL Policy were added to Deny that IP address, it wouldn't work. The hierarchy of ACL Policy enforcement means that the "Allow US Traffic" Policy will take precedence, and the 'Deny' Policy for that IP will never be invoked.

One way to quickly solve this problem is to add an ACL Policy with a name ending in a suffix of "XDeny" \(for example, "Block US Scraper XDeny"\). As was discussed in the "[Special ACLs](../../product-walkthrough/security/profiles/acl-policies.md#special-acls)" section, that suffix moves the ACL Policy to the top of the hierarchy. 

Therefore, that ACL Policy will be invoked and enforced for that IP address, and the attacking IP will be blocked, before the "Allow US Traffic" Policy has a chance to grant it access.

{% hint style="warning" %}
Long-term use of this capability is not optimal; using it too frequently can tend to create a collection of ACL policies that is messy, confusing, and difficult to manage. The optimal approach is to use it as a tool for solving a specific problem temporarily, while a robust set of ACL Policies are constructed and tested that will solve the problem correctly. 
{% endhint %}

