# Bandit Level 17 → 18
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit18.html)
## 📝 **Challenge Description**  
For this level there are 2 files in the home directory: **passwords.old** and **passwords.new**. The password for the next level is in **passwords.new** and is the only line that has been changed between **passwords.old** and **passwords.new**. 



## 🔍 **What I Initially Tried**  
This level was pretty straightfoward all I had to was figure out what the difference was between both of the files. Using the `diff` command this can make this process a lot easier without opening each file and inspecting the contents manually. 

## ✔️ What Worked
This is what I did:
```bash
diff passwords.new passwords.old
```
This was the output:
```
diff passwords.new passwords.old
42c42
< x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
---
> QqPdv6c2Ncstw7dg4MbSh4vxwY7pHJmE
```
This means that line 42 in `passwords.new` was **changed** compared to line 42 in `passwords.old`. According to the level description the password fpr the next level was in `passwords.new` meaning this is the password for the next level:
```
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```


## 🧠 Key Learnings
- Learned how to find the differences between two files using the `diff` command.
  
## 🛠️ Tools Used
**Terminal:** Cygwin  
**Commands:** `diff`


## 🔐 Next Step
Now let's move onto **level 18**. 

➡️ [Continue to Level 18 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%202%20--%3E%2018.md)
