# Bandit Level 1 → 2
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit2.html)
## 📝 **Challenge Description**  
In Level 1, the goal is to retrieve the password for `bandit2`. According to the challenge description:

> The password for the next level is stored in a file called `-` located in the home directory.

At first glance, this looks simple — just like Level 1. But the trick here is that the filename is a single dash (`-`), which causes issues with some commands that interpret it as a flag or option.



## 🔍 **What I Initially Tried**  
I started by listing the contents of the directory:
```bash
ls
```
Sure enough, there was a file named `-`.
So I did what worked before:
```bash
cat -
```

But instead of showing the password, it just seemed to hang or act weird. I realized that `cat -` usually means "read from standard input", so the shell wasn't treating the `-` as a filename — it thought I was trying to pipe something or give it a command-line option.

## ✔️ What Worked
After a bit of research and trial and error, I figured out that I could tell the shell explicitly to look for a file named `-` in the current directory by prefixing it with `./`, like this:
```bash
cat ./-
```
And that worked! It showed me the password for `bandit2`. 
Here's the breakdown:
- `./` means "look in the current directory".
- `-` is treated as a literal filename, not an argument or option in this situation.
- So `cat ./-` forces the shell to read and print the contents of the file instead of interpreting it as something else.

## 🧠 Key Learnings
- File names that begin with a dash can confuse command-line programs because `-` is usually reserved for **options/flags**.
- Use `./` to clearly tell the shell you're referencing a file in the current directory, not passing a flag.
- Naming files with special characters might be unusual, but it's a useful way to learn shell quirks.
- Sometimes problems aren't about complicated commands - they're about understanding how the shell interprets what you type.

## 🛠️ Tools Used
Still using Cygwin to access the server. I've also started messing with a **Ubuntu** virtual machine I set up on **VMware** to familiarize myself with the operating system and to deepen my understanding of how Linux really works under the hood.

## 🔐 Next Step
With the password for `bandit2` in hand, it's time to move on to the next level. The next level involves a file with spaces in its name. 

➡️ [Continue to Level 2 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%202%20--%3E%203.md)
