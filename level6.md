# Bandit Level 5 → Level 6

## 📝 Challenge Description 
In this level, the password for `bandit6` is stored **somewhere** in the `inhere` directory — but unlike the previous level, it could be deeper within subdirectories. The exact requirements are:

> The file is **human-readable**, **1033 bytes in size**, and **not executable**.

This one steps up the challenge from last time by making us scan through multiple folders and apply all conditions precisely.



## 🔍 What I Initially Tried 
At first, I treated it like Level 4 and navigated directly into `inhere`:
```bash
cd inhere
ls
```
But this time, instead of plain files, I saw directories named:
```
maybehere00 maybehere01 maybehere02 ...
```
I figured the file could be inside any of these, so I needed a way to scan through every file within all the subdirectories. 
Also, I knew from the last level that a "human-readable" file shows as `ASCII text` when checked with the `file` command. 
So I decided to use the `find` command again, but this time I needed to add two extra filters:
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
