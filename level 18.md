# Bandit Level 18 → 19
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit19.html)
## 📝 **Challenge Description**  
The password for the next level is stored in a file called **readme** in the homedirectory. Unfortunately, someone has modified the **.bashrc** file in a way where it automatically logs you out when you try to log in via **SSH**. 



## 🔍 **What I Initially Tried**  
The challenge description kind of threw me off guard so I decided to see it for myself and try to understand how this worked:
```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220
```

This was the output:
```
Byebye !
```

At this point in my journey, I didn’t fully understand the Bash scripting language, but I assumed the behavior was similar to a for loop, where a condition could trigger a break statement to exit the loop.

The problem now was figuring out how to avoid triggering the **.bashrc** script during login. When you **SSH** into a machine, it typically starts either an **interactive or non-interactive shell session**. In Bandit's case, a standard **SSH** login initiates an interactive login shell, meaning you’re dropped into a terminal that loads your shell configuration files and waits for user input.

A **non-interactive shell**, on the other hand, runs a command passed to it and then exits without loading the full interactive environment.

The **.bashrc file** is usually sourced in **interactive non-login shells**, but in some setups (like this one), **.bash_profile or .profile** may explicitly source **.bashrc**, causing it to execute even during login. In this challenge, the **.bashrc** was modified to immediately terminate the session, making it impossible to interact with the shell.

Initially, I considered generating an RSA key pair and uploading it to `bandit18`, but the solution was much simpler.

## ✔️ What Worked
After looking online this is what I ran:
```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
```
All this does is that the moment we **SSH** into `bandit18` we opened the contents of `readme` and like stated the **.bashrc** file kills the session. This line starts a non-interactive shell session and only executes the command you pass in the quotes. 

With this we can read the password for the next level:
```
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```



## 🧠 Key Learnings
- Learned what the **.bashrc** does and how it plays a role when starting a interactive shell session.
- Learned the differences between a interactive and non-interactive shell session.
- Learned the fundamentals on how **SSH** works and how it allows us to interact with the terminal via loading configuration files like **.bashrc** and **.bash_profile**.


## 🔐 Next Step
Now let's move onto **level 19**. 

➡️ [Continue to Level 19 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2019.md)

