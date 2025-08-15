# Bandit Level 32 → 33
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit31.html)

## 📝 **Challenge Description**  
The description for this level doesn't give us much information however upon logging in we are greeted with a **Uppercase Shell**. 
## 🔍 **What I Initially Tried**  
Based off the description, an uppercase shell executes commands in **uppercase** however this provides us with limited usability. I couldn't use regular commands like `ls` or `cat` so I needed a way to spawn a shell similar to how we spawned a shell in **vim** using the `:!bash` command. 
## ✔️ What Worked
After some research I found that typing `$0` spawns a shell. The reason for this is that it's a special variable that expands to the name of the shell or the shell script being executed. This initializes a new instance of the shell.

From here I just grabbed the password for `bandit33` via opening its password file:
```bash
WELCOME TO THE UPPERCASE SHELL
>> $0
$ cat /etc/bandit_pass/bandit33
tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0
```


## 🧠 Key Learnings
- Learned how to spawn a shell from within a restricted shell environment via `$0` command.
- Learned how restrictive shell environments can enforce command transformations. 


## 🔐 Next Step
Level 33 → 34 does not exist as of right now, so this is the end of the journey, for now. Next I will be working through and documenting my journey through pwn.college so stay tuned! 🤓🤓🤓🤓


