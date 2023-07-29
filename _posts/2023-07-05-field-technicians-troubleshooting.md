---
title: Field Technicians Troubleshooting
layout: post
post-image: "https://i.ibb.co/nQz3TTS/fieldtechnicianstroubleshooting.png"
description: Crafting roadmaps for uncharted solutions
tags:
- Troubleshooting
- SRE Guides
- Support Docs
- Knowledge Base
- Help Docs
- Technical Writing
- English
---

## Use Case

🔥 The company (let's call it _DoxHut_) was performing **PoCs** and running tests directly on what we can call a production environment. The software solution was implemented on a piece of software running on devices already established within the customer's facilities. Although it was _code_ injected in an application, it required various pieces of hardware installation and frequent maintenance. <br>
<br>
🍍 The challenge, however, was the team available to cover eventual incidents. Since we were **dealing with hardware**, on-site analysis was often inevitable. The team was mainly constituted of two levels: 
- **SREs**, in charge of controlling the servers' stability and, among other things, running a second level of analysis, usually requested by the Field Technicians, once they run the first instance of analysis and got confirmation on the issue not being related to the hardware installation's status. <br>
- **Field Technicians**, mostly constituted by interns, most of them part-time, and distributed across the country so that in-situ assistance was feasible.<br>

🚀 As soon as I learned what they did and how they did it, I noticed most of the incidents were time-sensitive, and the two instances of analysis had to occur swiftly and efficiently. To contribute to this cause, I interviewed **SMEs** from both sides, gathered all information on common issues and the steps to achieve their resolution, created a rough draft, validated it with them, and published the following **Help Docs page** for **troubleshooting** the issues they faced on a daily basis.

<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-J0NKP19PLY"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-J0NKP19PLY');
</script>

## Field Technicians Troubleshooting

![image](/assets/images/images-projectdesk-intro.png)

### Goal

This document aims to provide **Field Technicians** with a comprehensive overview of common issues and practical guidelines on how to effectively address them. It covers a wide range of scenarios, including remote troubleshooting and on-site analysis, offering actionable steps for resolution.

> 💡 Contact **SRE's Team Leader** for further questions via Slack.<br>
> 📡 Is there anything missing? Reach out to our **Tech Writer** via Slack.

### On this Page

- [In-Store Monitoring Service](#in-store-monitoring-service)
- [NAS](#nas)
- [Router](#router)
- [Server](#server)
- [Smart Power Supply](#smart-power-supply)
- [Switch](#switch)

## In-Store Monitoring Service
### Connection Issue

![image](/assets/images/images-fieldtechnicians-in-store1.png)

### VPN is Down

![image](/assets/images/images-fieldtechnicians-in-store2.png)

## NAS
### NAS is Full

![image](/assets/images/images-fieldtechnicians-nas1.png)

### NAS Disconnected

![image](/assets/images/images-fieldtechnicians-nas2.png)

### NAS Disk Broken

![image](/assets/images/images-fieldtechnicians-nas3.png)

## Router
### Router is Broken

![image](/assets/images/images-fieldtechnicians-router1.png)

### K3s Stopped 

![image](/assets/images/images-fieldtechnicians-router2.png)

### LTE/Dongle Issue

![image](/assets/images/images-fieldtechnicians-router3.png)

## Server
### Internal Disk Full

![image](/assets/images/images-fieldtechnicians-server1.png)

### Excessive CPU Use Alert

![image](/assets/images/images-fieldtechnicians-server2.png)

### High-Temperature Alarm

![image](/assets/images/images-fieldtechnicians-server3.png)

### "The Box is Disconnected" Message

![image](/assets/images/images-fieldtechnicians-server4.png)

### Server not Recording

![image](/assets/images/images-fieldtechnicians-server5.png)

### NAS is not Mounted

![image](/assets/images/images-fieldtechnicians-server6.png)

### Wrong Time Settings

![image](/assets/images/images-fieldtechnicians-server7.png)

### Excessive RAM Use

![image](/assets/images/images-fieldtechnicians-server8.png)

## Smart Power Supply
### Power Switch Unreachable (Not Shown/ No Message)

![image](/assets/images/images-fieldtechnicians-powersupply1.png)

### Outlets are Blocked (No Message)

![image](/assets/images/images-fieldtechnicians-powersupply2.png)

## Switch
### Switch is Off

![image](/assets/images/images-fieldtechnicians-switch1.png)

### Server Issue / Server is Off

![image](/assets/images/images-fieldtechnicians-switch2.png)

[Back to Home Page](/)