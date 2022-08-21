---
title: "Initial Cloudflare Zero Trust Setup"
date: 2022-08-20T13:22:21-04:00
categories:
    - network security 
tags:
    - tutorial
    - zero trust
    - cloudflare
    - parental controls

editPost:
    URL: "https://github.com/zcatk/icloudgo/discussions"
    Text: "Suggest Changes" # edit text
    appendFilePath: false # to append file path to Edit link
---

As promised, I'm here to give you a simple guide to get you up and running on Cloudflare's Zero Trust platform. Take a moment to read my previous post, [Cloudflare Zero Trust](/posts/cloudflare-zero-trust/) in the event you are looking to understand what Cloudflare Zero Trust has to offer. If you've already done your homework or want to dive right into setup, then you found the right place - lets get started.

Please note that this tutorial only walks you through IPv4 setup. I don't have IPv6 active on my network and no native means to use DoT/DoH. The steps are similar, but please keep this in mind.

### Setup Steps Simplified (IPv4)

1) Create or sign-in to your Cloudflare account
2) Select 'Zero Trust' from the left column of services
3) You will recieve an onboarding prompt - select next
4) Select a team name _(this is used to connect Warp clients later)_
5) Select your service tier _(I opted for Free, but your use case may differ)_
6) Complete payment (you must add a card even on the Free tier - I have never been charged)
7) Select 'Gateway' followed by 'Location' (**_Ensure you are connected with your home IP and not through a VPN, proxy, iCloud Relay, etc._**)
    - Select 'Add a location'
    - Enter a name
    - Check your 'Source IPv4' address (if it's wrong - press delete, turn off any VPN, proxy, iCloud Relay service on your device, and then select 'Add IP') 
    - Select 'Set as Default Location'
    - Select 'Add Location' 
8) Change your DNS address on your router
9) Select 'Done' at the top of the page  

Congrats! Your network is now integrated with Cloudflare Zero Trust, but you aren't done yet. 

You now need to determine what services you want to employ. For me, I wanted to protect our network from malware, phishing, and to block inapproproate content (parental controls). This requires you to setup policies, but those policies (DNS, Network, and HTTP) requires different configurations to work. I opted to only use DNS along with the Warp Client to secure our network - here'how: 

### Create a DNS Policy

1) Select 'Gateway' followed by 'Policies' from the left column of your 'Cloudflare Zero Trust' dashboard
2) Select 'Create a DNS Policy'
3) Setup your policy:
    - Name your policy
    - Build an expression
    - Select an action
    - Select 'Save' (_**It may take up to 60 seconds before your policy takes effect**_)
4) Rinse and repeat 

### My DNS Policies:

These policies execute in the order they are sorted, so you may have to reorder these or create an allow policy for unexpected blocks. 

Name | Expression | Action
---|---|---
Security Blocks | Security Categories in All Security Risks | Block
Content Blocks | Content Categories in _as applicable_ | Block
App Blocks | Application in _as applicable_ | Block
DuckDuckGo Safe Search | Domain is DuckDuckGo.com | Safe Search
Bing Safe Search | Domain is Bing.com | Safe Search
Google Safe Search | Domain is Google.com | Safe Search
Yahoo Safe Search | Domain is Yahoo.com | Safe Search
YouTube Restricted | Domain is youtube.com | YouTube Restricted

That's it, you can check to see if your rules are working by visiting the following sites:

Category | Test Domain 
---|---
Cryptomining | [cryptomining.testcategory.com](https://cryptomining.testcategory.com)
Malware | [malware.testcategory.com](https://malware.testcategory.com)
Phishing | [phishing.testcategory.com](https://phishing.testcategory.com)

_A more comprehensive list is available on [Cloudflare Docs](https://developers.cloudflare.com/cloudflare-one/policies/filtering/dns-policies/check-policy/)_

### What's Next

You should be pretty well setup at this point with all of your network devices protected. However, some additional steps remain if you want the same protections when on cellular or on the road. There are also some tricks, [using Regular Expressions](/posts/cloudflare-zero-trust-regular-expressions/), you can employ to provide even more benefits to your network. This tutorial only scratches the surface of what Cloudflare Zero Trust provides, but you should sleep easy knowing your network and family are safer.

Thanks for the read.

_Please reach out with questions, suggestions, and more on our [GitHub Discussion Page](https://github.com/zcatk/icloudgo/discussions)._ 