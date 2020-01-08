# Bypass Rate Limits for Loadtesting

Sometimes a customer wishes to "attack" an application or server as part of a loadtest. Under normal circumstances, Reblaze would prevent this, because it would enforce rate limits and block the excessive requests from reaching the upstream network.

The test can be accomplished by creating an [ACL Policy](../../product-walkthrough/security/profiles/acl-policies.md) which allows the source IP \(or range of IPs\), then naming that ACL Policy with a suffix of "OC." \(For example, the ACL Policy might be named "Loadtest OC."\)

As discussed in the [Special ACLs](../../product-walkthrough/security/profiles/acl-policies.md#special-acls) section, the "OC" suffix means that the IP will not be subjected to normal rate limit testing. This allows that IP to generate a large amount of traffic, which will be passed through upstream without being filtered by Reblaze.

