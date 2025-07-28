 # Bandit Level 0 → 1
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit1.html)
## 📝 **Challenge Description**  
In Level 0, you're already logged in as `bandit0`. Your goal is to find the password for `bandit1`. According to the instructions, the password is stored **in a file called `readme` located in the home directory**.  

Seems simple enough, but it teaches some basics about navigating the Linux file system and reading files from the command line.



## 🔍 **What I Initially Tried**  
After logging in using SSH, I didn’t see anything immediately obvious in the terminal. I thought maybe I had to search deeper or use some fancy commands.

I tried using:
```bash
ls
```
Which actually worked - it showed a file called `readme`.
I then tried: 
```bash
cat
```
...but I forgot to add the file name, so it just hung waiting for input. A classic beginner mistake 😅.

## ✔️ What Worked
Once I realized my mistake, I simply used the `cat` command properly by adding a filename to read the contents of the file:
```bash
cat readme
```

That revealed the password for the next level. Simple and clean.
Here's a quick breakdown:
- `ls` lists the files in the current directory.
- `cat` is used to print the contents of a file to the terminal.

## 🧠 Key Learnings
- Always look in the current directory first with `ls`
- `cat` is a powerful and straightfoward command to view the contents of a file
- When a challenge seems too simple, it probably *is*—just focus on the basics and don't overthink it.


## 🛠️ Tools Used
Still using **Cygwin** for my terminal emulator. I'm considering trying this on a VM or WSL (Windows Subsystem for Linux) soon to get more hands-on Linux experience. 

## 🔐 Next Step
Now we can move on to Level 2. According to the instructions, the password is stored in a file called `-` located in the home directory.

➡️ [Continue to Level 2 →](level2.md)

## 📓 Quick Note
If you are currently working through these levels, you might want to save your passwords in a file so it can be easier for you to reference. I recommend using **Notepad** to jot down the passwords for each level as you progress 😄. 
