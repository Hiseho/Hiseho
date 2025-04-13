---
title: Your First Server
description: "Let's jump into it and set up your first server !"
summary: ""
draft: false
weight: 810
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  robots: "" # custom robot tags (optional)
---

## Pre-requisites
Before we start, you should have a computer that will act as your server. This can be a dedicated machine or a virtual machine running on your existing computer. You should also have a domain name (optional but ***HEAVILY*** recommended) and some free time to set everything up.

### Things to mind here

- **A computer (the server)** : This can be a dedicated machine or a virtual machine running on your existing computer. A dedicated machine is more convenient as it will be always on and you won't have to worry about it being turned off. A virtual machine is also a good option if you don't want to invest in a dedicated machine right away.

*Note* : A dedicated machine can be a Raspberry Pi, an old laptop or a desktop computer that you don't use anymore. It can be a machine that is recent or old like a 10 years old laptop. Things that you might want to consider when choosing a machine are :
- The power consumption of the machine (laptops (at least mine) will usually draw 5W when Idle)
- The amount of RAM (4GB is a good starting point if you want to run one or two services but most of the time you will find yourself limited and should consider upgrading to 8GB or more)
- Disk (A SSD is faster but when it is not critical, a HDD is also a good option. You should mine the age of the disks as they can fail at any time, especially if old)

- **Another Computer (or a phone or a tablet)** : This is not mandatory but it is highly recommended. You will need this computer to access your server and to set it up. You can use your phone or tablet but it will be less convenient to type on a little screen.

- **A domain name** : This is not mandatory but it is highly recommended. A domain name will make it easier to access your services for you and your friends. You can buy them from a registrar, you can find a list of [Top Level Domains (TLD)](https://en.wikipedia.org/wiki/Top-level_domain). Note that in some cases, you want to have a domain with a good reputation (it is notably crucial if you want to dabble with email (which I do not recommand, especially if you are a beginner)). A good starting point to compare prices is [TLD-List](https://tld-list.com)

- **A password manager** : You should definitely have a password manager. It will help you to keep your passwords safe and secure. I really like [BitWarden](https://bitwarden.com) and recommend it0 You can self-host it but again, something this uptime critical is not something I would recommend to self-host as a beginner.

## Starting Point

Now that you have a computer. Let's start by installing a Linux distribution on it. There are many distributions available, a stable and easy to use would be [Debian](https://www.debian.org/). You can definitely use other distributions (I see you Arch Users) but for a service that should break as little as possible with updates, I would recommend using Debian. You can find a guide on how to install it [here](https://www.debian.org/releases/stable/amd64/). Please remember that a good password strength is the key to a good security. You can use a password manager to generate a strong password for you.

### Things to mind here
- **Desktop Environment** : You can choose to install a desktop environment or not. If you are not familiar with Linux, it might be easier but ideally, you would want a computer with its screen turned off most of the time. You can always install a desktop environment later if you need it, anyway.
- **SSH** : There is a good chance that you will want to access your server remotely. You can do this by installing SSH. It is not mandatory but it is highly recommended. You can install it directly from the installer or you can install it later using `apt install openssh-server`.

## Running as root

You should never run your services as root. It is a bad practice and it can lead to security issues. We will discuss it later in the guide.
**Root** is the highest privilege user on a Linux system. It has access to everything and can do anything, that's why you don't really want services to have that much power.

For convenience here, you can login as root on the server to do the configuration. Just type `root` as the username and the password you set during the installation. You can also use `sudo` to run commands as root on a sudoer user. On a fresh debian, you need to install it first using `apt install sudo`. You can then add your normal user to the sudo group by running `usermod -aG sudo <username>` running as root. This is a kind of super power that you can give to a user. It allows the user to run commands as root.

## SSH

To get something convenient to use, we will start by modifying the SSH configuration. SSH is a protocol that allows you to connect to your server remotely. First thing to do is to edit the file `/etc/ssh/sshd_config` using either `nano` or `vim`. You can use `nano` if you are not familiar with Linux. You can open the file with root permission using the command `sudo nano /etc/ssh/sshd_config` or without the `sudo` if running as root. You will need to enter your password to edit the file if running using `sudo`.

### Things to mind here

**Restarting the service** : After modifying the file, you will need to restart the SSH service for the changes to take effect. You can do this using the command `sudo systemctl restart sshd` or `systemctl restart sshd` if running as root. This will restart the SSH service and apply the changes you made to the configuration file. You **will** be disconnected from the SSH session and you will need to reconnect to the server using SSH so make sure you don't lock yourself out of the server. If you do, you will need to access the server using a keyboard and a screen to fix it.

**Comments** you will see a lot of commented lines (#) in the file. If you want to modify something, do not forget to remove the comment.

- **Port** : If you want to expose your SSH server (which you should not do under any circumstances), you should change the port to something else than 22. This is not a security measure but it will help you to avoid some bots that are scanning the internet for SSH servers. You can change the port by modifying the line `Port 22` to `Port <your_port>`. You can choose any port between 1024 and 65535. Just make sure that it is not already used by another service.

- **PermitRootLogin** : This option allows you to login as root using SSH. It really depends wheter or not you expose your SSH server. It also depends how cautious you are with the computer you use to access your server. If you use a SSH key (which I recommend and we will see later), having it set to yes would mean anyone that can access your computer could login to your server if they have the SSH key password.

- **PasswordAuthentication** : This option allows you to login using a password. It is not recommended to use it as it is less secure than using SSH keys. You can set it to `PasswordAuthentication no` to disable it. If you set it to yes, you will need to use a password to login to your server. The issue is that if your password is compromised, anyone can login to your server. If you set it to no, you will need to use SSH keys to login to your server. This is the most secure way to login to your server and they rarely get compromised, (unless someone has direct access to your computer but if you have a password on it, there's little they could do with it).<br><br>
*❗Do not forget❗*
We do not have a SSH key yet. If you set `PasswordAuthentication no` and you do not have a SSH key, you will not be able to login to your server from your other computer. You should start by setting it to `yes` and then set it to `no` once you have a SSH key stored.<br>

- **PubkeyAuthentication** : This option allows you to login using SSH keys. It is the most secure way to login to your server. You can set it to `PubkeyAuthentication yes` to enable it.

- **AuthorizedKeysFile** : This option allows you to specify the file that contains your SSH keys. You can set it to `AuthorizedKeysFile .ssh/authorized_keys` to use the default file. This is the default value and you don't need to change it.
This file is located in the home directory of the user you are logging in as.


Once that is done and you have restarted the SSH service, on your client computer, you can use the command `ssh <username>@<server_ip>` to login to your server. You will be prompted to enter the password for your user or private key if you set one. If you didn't set a password, you will be logged in directly. We will see how SSH keys work just after this.

## SSH Keys

SSH keys are a pair of cryptographic keys that are used to authenticate to a server. They are more secure than passwords and are the recommended way to login to your server. You can generate SSH keys (preferably on the client not the server) using the command `ssh-keygen -t ed25519`. This will generate a public and a private key. The public key is the one you will copy to your server and the private key is the one you will keep on your client computer. You will be prompted to name it and to enter a password. You can leave the name as default and enter a password or leave it empty. If you leave it empty, anyone with access to your private key will be able to login to your server without a password.
You can also use the command `ssh-keygen -t rsa` to generate RSA keys. This is less secure than ed25519 but it is still a good option if you want to use it.
Once your key is created, find it and copy the content of the public key (the one ending with `.pub`) to your server. You can do this using the command `ssh-copy-id <username>@<server_ip>`. This will copy your public key to your server and add it to the `~/.ssh/authorized_keys` file. You can also do this manually by copying the content of the public key to the `~/.ssh/authorized_keys` file on your server.
If not available, you can find another way to copy the file to your server, for instance copying it and pasting it using `nano` or `vim`.

**❗Do not forget❗**
The private key must be on the computer that wants to connect to the server. The public key must be on the server. You should create the key on the client computer to avoid copying it as it is way longer and if you resort to typing it by hand it will take time.

## HELP, I can't connect to my server with my SSH key

There is a step that you might have missed. Your client computer can hold a lot of keys at a time but will not know which to use unless specified. This can be done by editing a config file. You can create a file called `config` in the `~/.ssh/` directory on your client computer. You can do this using the command `nano ~/.ssh/config`. This file will contain the configuration for your SSH keys. You can add the following lines to the file :

```bash
Host <Name you want to give to your server>
    HostName <server_ip> # The local IP of your server
    User <username> # root or the user you created
    Port <port> #If you changed it
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/<private_key_file>
```

This is convenient as you can now use the command `ssh <Host>` to connect to your server. If you decided to name it `Dandy` for instance using `Host Dandy`, you can now use the command `ssh Dandy` to connect to your server. You can also use the command `ssh <username>@<server ip>` to connect to your server. This is the same as before but now you don't have to remember the IP address of your server.
