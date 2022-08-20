---
title: "Cloudflare Zero Trust"
date: 2022-08-19T18:02:37-04:00
categories: 
    - network security
tags:
    - parental controls
    - firewall
params:
    ShowPostNavLinks: true
    ShowCodeCopyButtons: true

editPost:
    URL: "https://github.com/zcatk/icloudgo/tree/master/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

### My Home Network Security Journey

I've used Cloudflare DNS for a number of websites over the years, but only recently discovered some of their more interesting offerings. I had used a pfSense appliance on our home network along with pfBlocker to keep our network secure and my kids off of inappropriate sites. Unfortunately, my SG-3100 started to act up and pfBlocker was also not as reliable. I dusted off a Raspberry Pi, loaded up Pi-hole, and threw it on my network with some improvements, but I missed many of the features pfSense offered. I found myself with what seemed like a simple problem - secure my network and keep my kids off of innapropriate sites. However, no single solution seemed to answer the mail and nothing prevented anyone from simply using cellular instead of WiFi on their phone to bypass any restrictions - not to mention hotspots for other devices. 

So the problem stood. Careful to avoid any disruption to our eero mesh network and the downtime schedule it provides, I turned on filters with our cellular provider and set our upstream DNS to Cloudflare Family (1.1.1.3, 1.0.0.3). This worked okay, but didn't prevent my teen from simply changing his device DNS, or using a VPN to bypass restrictions. I also had no oversight of what was blocked on the network. I needed parental controls, a robust firewall, and I missed the benefits of a network adblocker like Pi-hole. Really, I just wanted to regain control of my network. 

That's until I discovered ***Cloudflare Zero Trust***.

### What Is Cloudflare Zero Trust?

Let me start by pointing out Cloudflare Zero Trust is totally **FREE** for home/small office use (up to 50 users). I'm not trying to sell you on anything - there is no referral. I am seriously impressed by this service because not only does it work flawlessly, but Cloudflare's Zero Trust is **FREE**. You don't get all of the features without a subscription, but it provided everything I was looking for and didn't cost a dime. Here's Cloudflare's explanation of their Zero Trust Service:   

>Increase visibility, eliminate complexity, and reduce risks for remote and office users alike. Stop data loss, malware and phishing, and secure users, applications, and devices.
>>Clouflare.com

Confused as to what that means? I was too, but also intrigued by what it may offer. The short answer is a lot - here is a quick list from Cloudflare:

1) Zero Trust access for all of your applications.

- Authenticate users on our global edge network
- Onboard third-party users seamlessly
- Log every event and request

2) A Secure Web Gateway to protect users and devices.

- Enforce your company’s Acceptable Use Policy (AUP)
- Block risky sites with custom blocklists and built-in threat intel
- Enhance visibility and protection into SaaS applications

3) A fast and reliable solution for remote browsing.

- Execute all browser code in the cloud
- Mitigate the impact of attacks
- Seamless, lightning-fast end user experience

4) A Cloud Access Security Broker to safeguard data in the cloud.

- Protect users and sensitive data at rest in SaaS applications
- Detect insider threats and unsanctioned application usage, or Shadow IT
- Ensure best practices to prevent data leaks and compliance violations 

### Cloudflare Zero Trust Gateway

Again, I needed a way to secure my home network from phising, malware and, innaproproate content (parental controls). Not only that, but I also wanted to secure mobile devices while away or on cellular and prevent anyone from disabling the service or changing their device DNS to circumvent restrictions. Well, I am here to tell you Cloudflare Zero Trust can do all of that and much more. I have only scratched the surface of what this service provides as I have only employed their Gateway service along with WARP+ and some DNS policies. Don't underestimate this setup though as I'm convinced this outpaces nearly any home network security configuration regardless of price (in case you missed it earlier, it's **FREE**).

### What's Next

I plan to write a series of tutorials to help others with setting up and configuring Cloudflare Zero Trust. Cloudflare's documentation was not the best and there really isn't a lot of info out there to help.

Thanks for the read and I hope this was helpful in getting you started in making your family or office network safer.   
