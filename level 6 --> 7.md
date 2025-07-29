# Bandit Level 6 → Level 7

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
I figured these directories were configuration directories for the level so I didn't look into them. At this point I was really confused so I read the question again. That's where I found my mistake, the question states that the file is stored **somewhere** on the server. This means that we had to look through all of the directories on the server but obviously that would take forever so I leveraged the power of the `find` and `file` command to find the path to this file. 

## ✔️ What Worked
Here's the command I ended up using (very similar to the previous level):
```
find / -type f -size 33c -user bandit7 -group bandit6 -exec file {} \; | grep "ASCII text"
```
**What this does:**
- `find /`: searches from the **root** directory and all of its subdirectories.
- `-type f`: ensures we're only looking at files.
- `-size 33c`: filters for files that are exactly 33 bytes (`c` = bytes).
- `-user bandit7`: ensures the file is owned by user bandit7.
- `-group bandit6`: ensures the file is owned by group bandit6.
- `-exec file {} \;`: runs the `file` command on each result to determine its type.
- `| grep "ASCII text"`: filters for human-readable files (i.e. ASCII).
From the output of this command, I found the file path:
```
/var/lib/dpkg/info/bandit7.password: "ASCII text"
```
So I ran:
```
cat /var/lib/dpkg/info/bandit7.password
```
And there it was— the password for `bandit7`!
## 💡Quick Note
While the challenge didn’t require the file to be human-readable, using **file** and **grep "ASCII text"** helped confirm we had the right kind of file — likely to contain a password.

## 🧠 Key Learnings
- Again the `find` command gets the job done here however learning where to specify where the command should look is very important here.
- Knowing the terminology of **somewhere on the server** is very important and moving foward I need to work on reading the question clearly before moving foward with the solution.
- This level was very similar to the previous one but it's good to know the importance of using Linux file filtering techniques to find the file you are looking for.

## 🛠️ Tools Used 
Terminal: Cygwin.
Commands: `find`, `file`, `grep`, `cat`. 
It’s becoming second nature to combine these tools now — this level really made me feel like I’ve got a strong grasp on Linux file filtering.

## 🔐 Next Step
We’ve successfully grabbed the password and are ready for **Level 7**. 

➡️ [Continue to Level 7 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%207%20--%3E%208.md)
