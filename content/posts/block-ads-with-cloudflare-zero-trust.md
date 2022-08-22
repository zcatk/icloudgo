---
title: "Block Ads With Cloudflare Zero Trust"
date: 2022-08-21T10:21:47-04:00
categories: 
    - network security
tags:
    - tutorial
    - zero trust
    - cloudflare
    - parental controls
    - REGEX

editPost:
    URL: "https://github.com/zcatk/icloudgo/discussions"
    Text: "Suggest Changes" # edit text
    appendFilePath: false # to append file path to Edit link
---

If you haven't noticed, I'm seriously impressed with Cloudflare Zero Trust, but one feature remained missing - ad blocking. I was a longtime user of Pi-hole and loved the simplicity of it all. If you aren't aware, Pi-hole is deployed on a Raspberry Pi and blocks ads, trackers, and other nasty sites by using DNS block lists. You can also block or allow specific domains with a new rule from the pihole dashboard. They even had a way to block ads using regular expressions (REGEX) - this got me thinking. 

### REGEX Ad Blocking 

Pi-hole allows you to create ad-blocking rules using REGEX. It wasn't until after creating my [first REGEX policy](/posts/cloudflare-zero-trust-regular-expressions) to block abused TLDs that I realized Cloudflare Zero Trust could likely be used to do the same for ads. I found some REGEX for Pi-hole, created a policy, and tested things out - it didn't work. If you haven't read my other post on REGEX - Cloudflare Zero Trust doesn't use traditional REGEX. Instead Cloudflare's Gateway uses Rust to evaluate expressions. Given the simplicity of my TLD REGEX policy, I just created a similarly structured value - it worked.

#### Helpful Posts

In the event you need help:

- [How to create a DNS policy](/posts/initial-cloudflare-zero-trust-setup/#create-a-dns-policy))
- [REGEX Policy Guide](/posts/cloudflare-zero-trust-regular-expressions)

### Ad Blocker Policy

Name | Exp. Selector | Exp. Operator | Exp. Value | Action
---|---|---|---|---
Ad Blocks | Domain | matches regex | _see below_ | Block  

#### Policy Value

```
(advert|adserv|adsystem|doubleclick|2mdn|truecaller|uberads|206ads|360in|360yield|3lift|a2z|aarki|ad2iction|adcolony|addthis|adform|adhaven|adlooxtracking|admicro|adnxs|adpushup|adroll|adsafeprotected|adsbynimbus|adspruce|adsrvr|adswizz|adtelligent|adventori|adzerk|aerserv|amplitude|aniview|anzuinfra|apester|aralego|atdmt|atwola|bannersnack|batmobi|bluecava|blueconic|carambo|casalemediacriteo|crittercismriteo|crittercism|revcontent|ijinshan|imrworldwide|inmobi|marketo|moatads|moatpixel|mookie|perfectaudience|permutive|pubmatic|pushwoosh|rayjump|revcontent|revjet|rfihub|richrelevance|rqmob|rubiconproject|onetag|samba|scopely|scorecardresearch|shareaholic|sharethis|sharethrough|smaato|snapads|speedshiftmedia|supersonicads|swrve|taboola|tremorhub|unity3d|vertamedia|videohub|vungle|wzrkt|xiaomi|yieldlove|yieldmo|yieldoptimizer|baidu|chinanet|yandex|googlesyndication)
```

I built this list by referencing blocklists available on [firebog](https://firebog.net) -  they have a great collection of block lists. The values I selected are unique enough to not trigger unexpected blocks and the values advert, adserv, and adsystem appeared in a large number of the block lists so they triggeres on a lot on their own. Success.

### What's Next

I'm sure there is room for improvement, but this policy has served us well. Modify as needed and I'd be interested in any improvements you make. 

Thanks for the read.

_Please reach out with questions, suggestions, and more on our [GitHub Discussion Page](https://github.com/zcatk/icloudgo/discussions)._ 