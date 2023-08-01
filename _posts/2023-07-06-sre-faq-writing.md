---
title: FAQ
layout: post
post-image: "https://i.ibb.co/2yDYGJz/fatal-error.png"
description: Putting out fires with docs since 2017
tags:
- FAQ
- SRE Guides
- Support Docs
- Knowledge Base
- Help Docs
- Technical Writing
- English
---

## Use Case

🔥 At the company, let's call it "DoxHut," they were running **PoCs** (Proof of Concepts) directly on production. The software solution was implemented on devices already established within the customer's facilities. Although it was code injected into an application, it required various hardware installations and frequent maintenance.

🍍 However, they faced a challenge when it came to handling incidents. The senior **SREs** (Site Reliability Engineers) had a lot on their plates, leading them to onboard new team members, mainly juniors. The newcomers needed proper guidance on their day-to-day tasks, which sometimes meant the more experienced colleagues had to pause their work to assist them with "**basic stuff**."

🚀 When I took on the **tech writer** position, I had the opportunity to get to know each team better. During interviews, I asked them about their pain points. It turned out that they had always wanted to create an **FAQ** for newcomers, but they never had the chance to do so. Gathering testimonies and data, I created a page in our knowledge base with frequently asked questions. After reviewing and publishing it, I shared the page with the team. This sparked discussions, leading to additional items to include, which I promptly addressed in the periodic updates I had planned for this documentation piece.

<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-J0NKP19PLY"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-J0NKP19PLY');
</script>

## SRE FAQ

### Goal

Welcome to the neatly organized section for common **DevOps SREs** requests! Here, you'll find solutions to tasks like creating a user on a machine or setting up a new user, all aimed at saving valuable time for our SREs and unblocking coders more swiftly.

> 💡 We're all about staying up-to-date! If you come across any outdated solutions, don't hesitate to reach out and start a discussion on our **Slack channel** (**#sre-faqs**). Feel free to ping our technical writer, **@NaguiPinetta**, to request an update. We're committed to providing the latest and greatest solutions for you!
<br>

### On this Page
- [How To](#how-to)
- [Useful External Documentation](#useful-external-documentation)
- [Useful Tools](#useful-tools)


## How To
### Set up a new user on a machine:
- For an effortless setup of a new user with `sudo` and **Docker** access, simply follow these straightforward commands. Just replace `user` with your preferred username.

```bash
sudo adduser <user>              # Create the new user
sudo usermod -aG sudo <user>     # Add the user to the 'sudo' group for administrative privileges
sudo gpasswd -a <user> docker    # Add the user to the 'docker' group for Docker access
```

- You can achieve the same result with this convenient one-liner:

```bash
sudo adduser <user> && sudo usermod -aG docker <user>
```
<br>
> 💡 While the one-liner sets up the user with sudo and **Docker** access, it does not grant explicit passwordless sudo permissions. If you want to provide passwordless sudo access, you'll need to modify the sudoers file accordingly. However, please exercise caution when granting passwordless sudo access, and only do so for trusted users. Security should always be a top priority!
<br>

### Generate an SSH key:
- To generate an **SSH** key for secure communication, use the `ssh-keygen` command. For improved security, it is recommended to use the `Ed25519` key type.

```bash
ssh-keygen -t ed25519 -C "<name>@doxhut.xyz"
```

- Replace `name` with your desired identifier, email, or any other information you wish to associate with the key. This command will create an `Ed25519` SSH key pair, consisting of a private key (`id_ed25519`) and a public key (`id_ed25519.pub`). The public key can be shared with remote servers or services you want to authenticate with.
<br>
<br>

>💡 Remember to keep the private key secure and avoid sharing it with others. Security is crucial!

### TLDR Command to Delete a User:
The `userdel` command is used to remove a user account or remove a user from a group in **Linux** systems. Please note that all commands must be executed as root.

For more information about `userdel`, refer to the [manual page](https://manned.org/userdel).

To remove a user:
- Remove a user:

```bash
userdel [name]
```

- Remove a user along with their home directory and mail spool:

```bash
userdel --remove [name]
```

- Remove a user from a group:

```bash
userdel [name] [group]
```

- Remove a user in another root directory:

```bash
userdel --root [path/to/other/root] [name]
```
<br>
> 💡 Remember to replace [name], [group], and [path/to/other/root] with the actual username, group name, and path to the other root directory, respectively. Always exercise caution when using this command as it can result in the irreversible deletion of user data.
<br>

### CVD Upload Script:
A significant change has been made to the **CVD** upload script, where the code has been refactored to support camera coordinates for specific Cam IDs. An example configuration in the upload script is as follows:

```html
cam-config:
  fps: 25
  base-dimension:
  - 1280
  - 720
   origins:
    7:
    - 0
    - 0
    9:
    - 1280
    - 0
```
<br>
This configuration allows for specifying different camera coordinates (`origins`) for specific camera IDs, along with the frames per second (`fps`) and base dimensions (`1280x720`). This change enhances the flexibility and customization options for the **CVD** upload process.

### Reinstall k3s, Set up Rabbit, and GPU Splitting:
- To streamline the process of reinstalling k3s and configuring **Rabbit** with GPU splitting, a convenient script named `k3scli.sh` has been provided. This script is available in all the inference boxes, enabling easy execution of the required tasks.

#### Usage and Options:
- With `k3scli.sh -h`, you can view the available options for running the script:

```bash
root@dev-office-inference-0:/home/agot# k3scli.sh -h
    Usage: k3scli.sh args ...

    Description:
    Options:
        -k Uninstall and install k3s
        -r Install rabbit
        -g Setup GPU sharing
        -a Install AWS CLI
```
<br>

##### Reinstall Everything:
- To perform a complete reinstallation, including k3s, GPU splitting setup, and deploying Rabbit, simply execute the following command:

```bash
k3scli.sh -k -g -r
```
<br>
This command will effectively uninstall the current k3s version, perform a fresh installation, configure GPU sharing, and deploy Rabbit, ensuring a clean and optimized environment for your tasks.

### Killing a Running Process
In case of old processes running in the background and causing slowdowns, it is essential to identify and terminate them. The following commands will help you to pinpoint the troublesome processes and responsibly terminate them.
<br>

#### PS Command - Information about Running Processes:
To list information on running processes, use the `ps` command:

- List all running processes:     

```bash
ps aux
```

- List all running processes including the full command string:   

```bash
ps auxww
```

- Search for a process that matches a string:

```bash
ps aux | grep string
```

- List all processes of the current user in extra full format:   

```bash
ps --user $(id -u) -F
```

- List all processes of the current user as a tree:

```bash
ps --user $(id -u) f
```

- Get the parent PID of a process:     

```bash
ps -o ppid= -p pid
```

- Sort processes by memory consumption:     

```bash
ps --sort size
```
<br>
> 🧷  More information about the ps command can be found [here](https://manned.org/ps).
<br>

#### Kill Command - Terminate a Process:
The <kill> command sends a signal to a process, usually to stop it. Choose the appropriate command based on your scenario:
<br>

> 💡 All signals except for `SIGKILL` and `SIGSTOP` can be intercepted by the process to perform a clean exit. 
<br>

- Terminate a program using the default `SIGTERM` (terminate) signal:

```bash
kill process_id
```
- List available signal names (to be used without the SIG prefix):

```bash
kill -l
```

- Terminate a background job:

```bash
kill %job_id
```

- Terminate a program using `SIGHUP` (hang up) signal. Many daemons will reload instead of terminating:

```bash
kill -1|HUP process_id
```

- Terminate a program using the `SIGINT` (interrupt) signal. This is typically initiated by the user pressing `CTRL + C`:

```bash
kill -2|INT process_id
```

- Signal the operating system to immediately terminate a program (which gets no chance to capture the signal):

```bash
kill -9|KILL process_id
```

- Signal the operating system to pause a program until a `SIGCONT` (continue) signal is received:

```bash
kill -17|STOP process_id
```

- Send a `SIGUSR1` signal to all processes with the given GID (group ID): 

```bash
kill -SIGUSR1 -group_id
```
<br>
> 🧷  More information about the `kill`command can be foun [here](kill - manned.org). 
<br>

> ⚠️ **Caution:** These commands are sensitive and can lead to issues. Killing a process might affect someone else's work. Please use these commands with care and consideration.
<br>

### How to Create S3 Buckets
Follow the guidelines included in this [repo](https://git.agot.ai/users/sign_in).

### How to install
### Adding User for Automations
To set up a new user with administrative privileges for automations, follow these steps:

This command creates a new user with the username `awx` and sets the user's shell to `/bin/bash`. The user will be added to the `sudo` group, granting administrative privileges.

- Create a new user for automations.

```bash
useradd -c "User for automations" -G "sudo" -s /bin/bash -m awx
```

- Set up SSH for the new user.

```bash
mkdir -p /home/awx/.ssh && chmod 0700 /home/awx/.ssh && touch /home/awx/.ssh/authorized_keys && chown -R awx. /home/awx/.ssh && chmod 0600 /home/awx/.ssh/authorized_keys
```

- Edit the sudoers file.

```bash
sudo visudo
```

- Add the following configurations to the sudoers file.

```bash
Defaults    env_reset
Defaults    mail_badpass
Defaults    secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
root    ALL=(ALL:ALL) ALL
%admin  ALL=(ALL) ALL
%sudo   ALL=(ALL:ALL) NOPASSWD: ALL
See sudoers(5) for more information on "#include" directives:
includedir /etc/sudoers.d
```
- Add the SSH public key to the `authorized_keys` file for the new user.

```bash
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMOmhXTjtS4Tehalzfyn6KwPU0CwYpCSRuv2+P/bZrrc user for automation
```
- You can copy and paste each step into your Markdown file or text editor. The code snippets are formatted as code blocks for better visibility and clarity.

## Useful External Documentation
### kubclt Reference Docs
Access [kubectl official documentation](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands).<br>
If you are wondering how to perform a specific action inside a <Kubernetes> cluster, you can find the corresponding command by looking for the closest verb in the left pane. The verbs listed in the documentation are closely related to the actions you want to execute within Kubernetes. This can help you quickly identify the appropriate command for your task.

## Useful Tools
### TLDR
TLDR is a powerful application that provides concise and practical cheatsheets for various console commands. It is like **TLDR RM**, but with a list of the most frequently used rm commands and their explanations. You can find more information about this tool and explore its collaborative cheatsheets on [GitHub - tldr-pages/tldr: 📚 Collaborative cheatsheets for console commands](https://github.com/tldr-pages/tldr). TLDR can save you time and effort by presenting the most relevant information in a clear and easy-to-understand format.
<br>

> This document was last updated on **06/06/2022** by **Nagui Pinetta**.

[Back to Home Page](/)