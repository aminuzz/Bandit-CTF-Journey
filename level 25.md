# Bandit Level 25 → 26
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit26.html)
## 📝 **Challenge Description**  
The shell for the user `bandit26` is not in **/bin/bash**, but it's something else. So we need to figure out what it is, how it works, and how we can obtain the password for the next level. 
## 🔍 **What I Initially Tried**  
Based on the level description I needed to figure where the **shell** is for user `bandit26`. After some research this is what I did:
```bash
grep "bandit26" /etc/passwd
```
The `/etc/passwd` file **lists all user accounts** on the system, along with some information about each user so I used the `grep` command to find information about user `bandit26`:
```
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```
Here I saw that the **shell** for user `bandit26` was located in `/usr/bin/showtext`, not your typical shell location. I decided to look into this file to see what was in it:
```bash
cat /usr/bin/showtext
# Output:
#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0
```
As soon as you login via **SSH** using the provided RSA key, the normal shell is bypassed due to the execution of the `more` command. `more` is a pager program, it allows us to scroll through a file however since `exec` is used, this replaces the shell process with the `more` command. So I had to figure out a way to get around this. 
## ✔️ What Worked
After some research on how the `more` command works, I found that there is a specific way to exploit this command by reducing the size of your terminal window:
- The `more` command is a pager that **decides how much content to display at once** based on the **terminal's rows and columns**. Since we do not have access to `~/text.txt`, shrinking the terminal will trick the `more` command giving you a small window to interact with it.
- `more` has a hidden feature, being that if you press `v` on your keyboard, it'll spawn `vim` (the text editor). It thinks that you want to edit the file `more` is being executed on however we can use that to find `bandit26` password.
- Once in `vim` we can use the `:e` command to **open any file you have permission to read**. Since we logged into `bandit26` via the RSA private key, we temporarily have permissions to read the password file.

And that's how I solved this level.
## 🧠 Key Learnings
- Learned how to identify and find the location of a user's shell.
- Learned how to exploit the `more` command using `vim` in order to gain temporary privileges to read a password file.
- Learned how to use `vim` commands in order to open specific files.



## 🔐 Next Step
Now let's move onto **level 26**. 

➡️ [Continue to Level 26 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2026.md)

