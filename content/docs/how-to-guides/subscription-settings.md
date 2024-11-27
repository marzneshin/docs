---
title: Subscription Settings
---

Subscription settings are used to tune the subscription endpoints.

# Subscription Rules
Subscription rules determine how the subscription endpoint would correspond
to different user-agents; Each rule consists of a regex pattern to be matched
on the user-agent and the result to be returned. Rules are tried from top to bottom
respectively until one matches the user-agent. In case none of the rules match, the
response would be empty.

![Example rules](/images/subscription_rules.png)

The rules in the picture are the default values right now. First rule for v2rayN
matches versions higher than 6.40, and returns Xray custom config. Older versions
fall in the next rule; the first rule for v2rayNG matches 1.8.16+ and returns
Xray custom config, otherwise the next rule returns base64-links.

# Other Settings
![Other subscription settings](/images/subscription_other.png)

If **Template on Acceptance** is set to true, the subscription endpoint would
return the html template in case `Accept: text/html` is in request headers.
