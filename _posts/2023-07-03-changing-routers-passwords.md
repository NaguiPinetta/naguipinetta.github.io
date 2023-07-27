---
title: Changing Routers Passwords on Teleport
layout: post
post-image: "https://i.ibb.co/9p7XPrg/teste.png" 
description: Crafting roadmaps for uncharted solutions
tags:
- SRE Guides
- Support Docs
- Knowledge Base
- Help Docs
- Technical Writing
- English
---
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-J0NKP19PLY"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-J0NKP19PLY');
</script>

# Changing a Router's Password on Teleport

![intro](/assets/images/images-changingpasswords-intro.png)

## On this Page:

- [Actions Required](#actions-required)
- [Prerequisites](#prerequisites)
- [Creating Passwords for Stores' Routers on LastPass](#creating-passwords-for-stores-routers-on-lastpass)
- [Accessing a Server](#accessing-a-server)
- [Setting SREs SSH RSA Keys](#setting-sres-ssh-rsa-keys)
- [Bonus: Setting Server’s Time](#bonus-setting-servers-time)

## Actions Required

- Create passwords and sections for servers on **LastPass**
- Access servers and change routers passwords
- Add **SREs' SSH RSA keys** to the routers authorized keys
- Set server time

## Prerequisites

- Having a **LastPass user**
- Having a **Teleport User**
- Having **Teleport installed**
- Having necessary **SSH RSA Keys**
- Knowing which servers to make changes to.

## Creating Passwords for Stores' Routers on LastPass

To create a section for each store’s router password on **LastPass**:

1. Access **DoxHut's LastPass Password Manager** panel.<br>

2. Create a **New Item** by clicking the plus icon located at the bottom right corner. This action will open a modal where you must fill in a few fields. <br>

    ![createnew](/assets/images/images-changingpasswords-createnew.png)<br>

3. Fill in the **Name** field with the server’s name.<br>

4. Fill in the **Folder** field with the “**Shared-stores**” value.<br>

5. Fill in the **Username** with “**root**.”<br>

6. Create a strong password (use the **LastPass' Generate Secure Password** tool).<br>

7. Copy the password and paste it into the **Site Password** field.<br>

8. Save this configuration by clicking **Save**.<br>

9. Repeat the whole process for each of the servers listed below.<br>

    ![createnew2](/assets/images/images-changingpasswords-createnew2.png)

## Accessing a Server

1. List the existing servers by running: <br>
`tsh ls` <br>

   You will see all servers listed as shown next 

   ![console-servers](/assets/images/images-console-servers.png)

2. Select a server and access it:<br>
`tsh ssh doxhut@doxhut-2-xavier-0` (example)

3. Then, access the router:<br>
`ssh root@192.168.1.1`

4. Once in the router, change its password by running:<br>
`passwd`

5. You will get a confirmation message and that’s it!<br>

## Setting SREs SSH RSA Keys
To set an **SREs SSH RSA key** in the router:<br>

1. Run:<br>
`cd /root`

2. List all directories:<br>
`ls -hal`

3. Open .ssh:<br>
`cd .ssh`

4. Then, edit the authorized keys:<br>
`vim authorized_keys`

5. Once on the **Vim editor**, press **“i”** to activate the editor mode.<br>

6. Paste one of the **SSH RSA keys**.<br>

7. Press **“Esc”** to exit edit mode.<br>

8. Press **“o”** to jump into the next line.<br>

9. Press **“i”** to activate the editor mode and paste a second key.<br>

10. Repeat the process for key you must insert in the file.<br>

11. Finally, make sure you are not in the editor mode, and type **“:wq”** to save changes and quit. <br>

## Bonus: Setting Server’s Time

Since you are already on the server, use the chance to set the server’s time by running:

`uci set system.ntp.enable_server='1' ; uci commit system ; /etc/init.d/sysntpd restart`<br>

> 💡 **Note**: You will not get any confirmation message for the last step.

<br><br>

[Back to Home Page](/)