---
title: "Cloudflare Gateway With DoH"
date: 2022-08-21T10:18:09-04:00
categories: 
    - network security
tags:
    - tutorial
    - zero trust
    - cloudflare
    - WARP

editPost:
    URL: "https://github.com/zcatk/icloudgo/discussions"
    Text: "Suggest Changes" # edit text
    appendFilePath: false # to append file path to Edit link
---

There are a few different options when looking to use DNS over HTTPS with Cloudflare Zero Trust. I considered dusting of my Raspberry Pi, yet again, to deploy Cloudflared to tie into my Zero Trust setup but didn't want to bother with the setup and management of another network device. Instead, I opted to live with non-encrypted DNS across my home network with the exception of our desktops, laptops, tablets, and phones. For those devices, I installed the Cloudflare WARP client to not only deliver DoH, but to also do so when away from home. This takes a bit more configuration to tie into your Zero Trust setup, but I'm here to walk you through a basic setup without having to navigate the confusing and misleading instructions found in Cloudflare's documentation.

### Basic WARP Client Configuration

1) Install the WARP client on your devices - here's the [download links](https://developers.cloudflare.com/cloudflare-one/connections/connect-devices/warp/download-warp/) for Android, iOS, macOS, Windows, Linux, and Chrome 

2) Create an access group 

- Select 'Access Groups', under 'Access', from the left column of your Zero Trust dashboard 
- Select 'Add Group'
- Enter a group name
- Select ' Set as default group'
- Define a group rule for inclusion. I set mine to only include those with an email ending with our families custom domain (_i.e example.net_) 
- Select 'Save' at the top of the page

3) Update your WARP client settings on Cloudflare

- Select 'Settings', at the bottom, of the Zero Trust dashboard's left column
- Select 'Manage' device enrollment settings
- Select 'Add a rule'
- Provide a name
- Rule action: Allow
- Selector: Emails ending in; Value: _example.com_ (or even specific email - whatever works for you)
- Select your group below
- Select 'Save'
- Select 'Back to Settings'

4) Modify your WARP Admin settings

- Admin override: Disabled
- Captive portal detection: Enabled; 3 minutes
- Mode switch: Enabled 
- Lock WARP switch: Enabled
- Allow device to leave organization: Diabled
- Allow updates: Disabled
- Auto connect: Enabled; 1 minute
- Support URL: Disabled
- Service mode: Gateway with WARP

5) Login to your team from each device with WARP

- Open the WARP app on your device
- Navigate to 'Account'
- Select 'Login with Cloudflare for Teams'
- Enter your team name
- Complete the authentication (one-time pin is configured by default)
- Enter your email and select 'Send me a code'
- Check your email for the pin to complete sign-on or select the link

### Testing Your Configuration

[Cloudflare's Zero Trust Help Page](http://help.teams.cloudflare.com)

### Success

Congrats - your device is now enrolled with Cloudflare Zero Trust. This is really useful as you can now apply policies to specific users. You can also review logs to troubleshoot blocks or to identify user activities warranting further review. 

### What's Next

This is as far as I went with our configuration, but you can go a step further by installing and trusting Cloudflare's certificates. This would allow you to deploy a proxy service and enable A/V scanning, HTTP filtering, browser isolation, and more. This seemed too intrusive for what we needed in our household, but it's nice knowing it's an option and something I might try later in a lab environment (expect a post if I do).  

_Please reach out with questions, suggestions, and more on our [GitHub Discussion Page](https://github.com/zcatk/icloudgo/discussions)._ 