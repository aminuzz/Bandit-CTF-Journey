# Bandit Level 0
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit0.html)

## 📝 Challenge Description

For Level 0, the challenge asks how to log into the game via SSH. They provide:
- the **username**: `bandit0`
- the **password**: `bandit0`
- the **host**: `bandit.labs.overthewire.org`
- the **port**: `2220`

Your task is to figure out how to connect to the remote server and gain access to the first level.

Pretty simple for someone experienced, but for a beginner it might seem confusing at first.



## 🔍 What I Initially Tried

I had never used SSH before, so I just tried typing the following:

```bash
ssh bandit0@bandit.labs.overthewire.org 
```
But when I tried that, it didn't work. The command kept timing out or giving me conneciton errors. 
I didn't understand why at first, but then I re-read the instructions and realized they provided a **custom port number (2220)** which is something that SSH doesn't use by default unless you explicitly tell it to.

## ✔️ What Worked

After realizing my mistake, I added the `-p` flag to the SSH command to specifiy the correct port. This was the working command:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```
Here's a breakdwon of how this works:
- `ssh` is the command to securely login to a remote computer/server. 
- `bandit0@bandit.labs.overthewire.org` is the standard way of logging in. It follows this format: `username@host`
- `-p 2220` specifies what port we are using ssh to connect to. The default port is **port 22**.

## 🧠 Key Learnings

This challenge helped me understand some of the fundamentals of connecting to remote systems: 
- **SSH (Secure Shell)** is a network protocol that allows us to access remote machines.
- The default port for SSH is **22**, but it can be changed by the user in this case to **2220**.
- You can specify a custom port by using the **-p** flag/option.
- Carefully reading through the instructions and documentation, if I hadn't caught the port number I would've been stuck.
- Not all command-line errors are **"hard"** problems, you just need to have the mindset of trying to figure out what you did wrong and how you can fix it.


## 🛠️ Tools Used

In this case I am using **Cygwin**, a terminal emulator however you can also use **Powershell** or simply use **Terminal**. 
If you're extra fancy and what to get into the nitty gritty stuff I recommend experimenting setting up a virtual machine with virtualization software. 
**VMware** is a good choice for beginners and you can find dozens of tutorials online on how to get your favorite Linux distro up and running with it.

## 🔐 Next Step

Now we can move on to **Level 1**. According to the instructions, it's stored in a file called `readme` located in the home directory. 

➡️ [Continue to Level 1 →](level1.md)
