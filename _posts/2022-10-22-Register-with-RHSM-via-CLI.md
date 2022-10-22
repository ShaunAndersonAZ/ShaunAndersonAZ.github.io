---
published: true
header:
  overlay_image: #/assets/images/rocky-mtns.jpg
  caption: #"[CC License](https://creativecommons.org)"
categories:
---

# Register with RedHat Subscription Manager via Command Line
This is a simple thing that you don't do very often.  So it always trips me up. Short and sweet, here we go.

## Register system
Using the subscription-manager command, register the new system.
`#>subscription-manager register --user <username> --password <password>`

Gotcha here is that it wanted the actual username, not my email which I though was my username as I use it to authenticate to the Redhat Partner portal.

Once you are registered you can query which subscriptions you have access to.
`#>subscription-manager list --available`

This will output the various Subscriptions. Once you find the subscription you want to utilize, find the 'Pool ID'
`
SKU:                 RH3387200
Contract:            12949065
Pool ID:             8a82c58b7fc28cd5017fe701d51a35b1
Provides Management: No
Available:           2
Suggested:           1
`

Next, *attach* to that subscription pool.
`subscription-manager attach --pool=8a82c58b7fc28cd5017fe701d51a35b1
Successfully attached a subscription for: Red Hat Enterprise Linux, Self-Support (128 Sockets, NFR, Partner Only)
`

Finally you can run `yum update` to check for updates.

# Script required for comments to be enabled.
<script src="https://utteranc.es/client.js"
        repo="shaunandersonaz/shaunandersonaz.github.io"
        issue-term="pathname"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>

