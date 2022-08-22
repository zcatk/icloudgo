---
title: "Cloudflare Zero Trust Regular Expressions"
date: 2022-08-21T10:20:14-04:00
categories: 
    - network security
tags:
    - tutorial
    - zero trust
    - cloudflare
    - REGEX

editPost:
    URL: "https://github.com/zcatk/icloudgo/discussions"
    Text: "Suggest Changes" # edit text
    appendFilePath: false # to append file path to Edit link
---

The use of Regular Expression (REGEX) for your Cloudflare Zero Trust Gateway policies delivers some seriously powerful solutions. I ran into issues when attempting to get things working because I was attempting to use traditional REGEX. That is until I found, buried in Cloudflare's documentation, that Gateway used Rust to evaluate expressions rather than what I was accustomed to using. At the suggestion of Cloudflare, I visited [Rust REGEX](https://rustexp.lpil.uk) to build and test expressions. 

### Abused Top Level Domains (TLD) 

I designed my first REGEX expression to block the most abused TLDs reported on [The Spamhaus Project](https://www.spamhaus.org/statistics/tlds/). I also added a few additional TLDs that I wanted to block on our network. 

### DNS Block Policy   

I then created a new DNS policy ([How to Create a DNS Policy](/posts/initial-cloudflare-zero-trust-setup/#create-a-dns-policy)) in the Cloudflare Zero Trust dashboard as follows:

Name | Exp. Selector | Exp. Operator | Exp. Value | Action
---|---|---|---|---
TLD Blocks | Domain | matches regex | _see below_ | Block  

#### Policy Value

```
[.](surf|rest|tokyo|ml|cam|icu|cf|gq|best|tk|cn|ru|xyz)
```

### What' Next

Allow up to 60 seconds after saving for your policy to take effect. That's it - test your new policy by attempting to access a domain with one of the TLDs you blocked. 

Thanks for the read. Using REGEX can simplify your policies and introduce some powerful solutions - like [blocking ads](/posts/block-ads-with-cloudflare-zero-trust) on your network.  

_Please reach out with questions, suggestions, and more on our [GitHub Discussion Page](https://github.com/zcatk/icloudgo/discussions)._ 