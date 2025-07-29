# Bandit Level 7 → Level 8

## 📝 Challenge Description 
In this level, the password for `bandit8` is stored in the file called `data.txt` next to the word **millionth**.







## 🔍 What I Initially Tried 
At first, I opened `data.txt` with the cat command to inspect the contents of the file and see if I could spot the password manually:
```bash
cat data.txt
```
However, the file was far too large to scan manually — skimming through all of it wasn’t practical so I needed to figure out a way where I can sort the file or pinpoint the exact location of the word **millionth** to find the password. From the previous level, I figured that the `grep` is perfect for this, as it allows you to search for specific terms within a file and it'll show you the exact location where that term is. 


## ✔️ What Worked
Here's the command I ended up using:
```
grep millionth data.txt
```
**What this does:**
- `grep millionth`: filters out/searches for the keyword (**millionth**)
- `data.txt`: refers to the file we are looking in
From the output of this command, I found the password:
```
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```
And there it was the password for `bandit8`!


## 🧠 Key Learnings
- The `grep` command is extremely helpful for locating specific keywords in large files. Without it, finding the right line in a file like `data.txt` would take far too long.


## 🛠️ Tools Used 
Terminal: Cygwin.
Commands: `grep`, `cat`. 
I'm slowly getting used to using file filtering techniques in Linux. It's a lot to know at first but once you get used to using them, you won't forget it.

## 🔐 Next Step
We’ve successfully grabbed the password and are ready for **Level 8**. 

➡️ [Continue to Level 8 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level9.md)
