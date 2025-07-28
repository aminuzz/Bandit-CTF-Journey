# Bandit Level 5 → Level 6

## 📝 Challenge Description 
In this level, the password for `bandit7` is stored **somewhere** on the server. Unlike the previous level where the password was stored in a specified directory, we have to find a way to leverage the power of the `find` and `file` commands to look through the entire server.

> The file is **owned by user bandit7**, **owned by group bandit6**, and **33 bytes in size**.





## 🔍 What I Initially Tried 
At first, I was a bit confused on how to approach this problem since the problem didn't give me a specified directory to look for so I initially tried looking for one that might catch my attention:
```bash
ls -a
```
I tried using the `-a` flag to see if there was a hidden directory that I have to look into but it was to no avail:
```
.  ..  .bash_logout  .bashrc  .profile
```
I figured these directories were configuration directories for the level so I didn't look into them. At this point I was really confused so I read the question again. That's where I found my mistake, the question states that the file is stored **somewhere** on the server. So it wasn't a specific directory I had to look into..
- One for **file size**: exactly 1033 bytes
- One to exclude **executable** files

## ✔️ What Worked
Here's the command I ended up using:
```
find -type f -size 1033c ! -executable -exec file {} \; | grep "ASCII text"
```
**What this does:**
- `find`: searches the current directory and all subdirectories.
- `-type f`: ensures we're only looking at files.
- `-size 1033c`: filters for files that are exactly 1033 bytes (`c` = bytes).
- `! -executable`: ensures the file is **not** executable.
- `-exec file {} \;`: runs the `file` command on each result to determine its type.
- `| grep "ASCII text"`: filters for human-readable files (i.e. ASCII).
From the output, I found the file path:
```
./maybehere07/.file2: "ASCII text"
```
So I ran:
```
cat ./maybehere07/.file2
```
And there it was— the password for `bandit6`!

## 🧠 Key Learnings
- `find` is incredibly powerful when combined with size, type, and permission flags.
- You can use `! -executable` to filter out anything you can't "run" like a program/script.
- Using `file` alongside `grep` helps validate file content types across multiple unknown files.
- Visual cues (like dotfiles or hidden names) often mean something special in Bandit challenges.

## 🛠️ Tools Used 
Terminal: Cygwin.
Commands: `find`, `file`, `grep`, `cat`. 
It’s becoming second nature to combine these tools now — this level really made me feel like I’ve got a strong grasp on Linux file filtering.

## 🔐 Next Step
We’ve successfully grabbed the password and are ready for **Level 7**. 

➡️ [Continue to Level 7 →](level7.md)
