# Bandit Level 7 → Level 8

## 📝 Challenge Description 
In this level, the password for `bandit8` is stored in the file called `data.txt` next to the word **millionth**.







## 🔍 What I Initially Tried 
At first, I opened `data.txt` with the cat command to see what was in the file, and see if I could find the password manually:
```bash
cat data.txt
```
However, that pretty much seemed impossible because the file had so much text in it and skimming through the entire file to find the password would take forever so I needed to figure out a way where I can sort the file or pinpoint the exact location of the word **millionth** to find the password. From the previous level, I figured that the `grep` command could help us here since it allows us to search for a specific term that you can specify and it'll show you the exact location where that term is. 


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
And there it was— the password for `bandit8`!


## 🧠 Key Learnings
- Again another file filtering command, `grep`, has helped me solved this level so it's good to know how to utilize Linux filtering techniques to quickly sort and filter out information from large files. the `find` command gets the job done here however learning where to specify where the command should look is very important here.


## 🛠️ Tools Used 
Terminal: Cygwin.
Commands: `grep`, `cat`. 
I'm slowly getting used to using file filtering techniques in Linux. It's a lot to know at first but once you get used to using them, you won't forget it.

## 🔐 Next Step
We’ve successfully grabbed the password and are ready for **Level 8**. 

➡️ [Continue to Level 8 →](level 8 --> 9.md)
