# Bandit Level 19 → 20
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit20.html)
## 📝 **Challenge Description**  
In order to get the password for the next level, we have to use the **setuid binary** in the homedirectory. The password for the next level can be found in the usual place (/etc/bandit_pass), after you use the **setuid** binary.



## 🔍 **What I Initially Tried**  
Initially, I did some research on file permissions in Linux and how it relates to the **setuid binary**. This is what I learned:

```bash
ls -l hi.txt
-rw-rw-r-- 1 bandit19 bandit19 12 Aug  7 23:06 hi.txt
```
The first character `-` shows that this is a **file**. If it were a directory, you'd see a `d` instead (you can check this with `ls -ld directory_name`).

The next nine characters are split into **three groups** of permissions:
- **"First three → Owner (user)"**
- **"Second three → Group"** (Group as in a group of users)
- **"Last three → Others"**  (Other users that are not the owner or part of the group)

Each position can be:
- **"r = read"**
- **"w = write"**
- **"x = execute"**

For directories, execute permission means you can `cd` into it **and** access its contents.

In **setuid binaries**, you'll sometimes see an `s` in the **owner's execute position** (e.g. `-rwsr-xr-x`). This means that the program runs with the permissions of the file's owner instead of the user running it. 

Additionally, with the `hi.txt` example we can see a number (`1`) which denotes the **link count** which is how many references point to that particular file/directory. For regular files it's usually **1** however for directories it's a different case. For directories it's at least `2` since we take into account **the directory itself** and the **parent directory**. If the directory includes any **sub-directories**, they are counted as well.

Following the **link count** we have:
- **User owner** → the account that owns the file (`bandit19` here).
- **Group owner** → the group that owns the file (also `bandit19` here).
- **File size** → in bytes (so `12` here means 12 bytes long).
- **Date/time** → **last modification time**, not creation time.
- **Name** → `hi.txt`

Now with this information, we can move onto solving this level.

## ✔️ What Worked
First I checked where the **setuid binary** was:
```bash
ls -a
.  ..  bandit20-do  .bash_logout  .bashrc  .profile
```

I noticed the file `bandit20-do` was highlighted in red and checking the permissions of the file verified that this had to be the **setuid binary** file. Going back to the definition, this binary allows us to run commands as if we were the owner of the file. 

```bash
ls -l
-r-------- 1 bandit20 bandit20 33 Jul 28 19:03 /etc/bandit_pass/bandit20
```
Since the password for `bandit20` can only be read by `bandit20`, we can use the **setuid binary** to open the contents of the password file as if we were user `bandit20`:
```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

And there we have it, the password for `bandit20`:
```
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

## 🧠 Key Learnings
- Learned how to utilize the **setuid binary** in order to escalate our privileges to gain access to files that were originally not accessible.
- Learned how to interpret file/directory permissions in Linux in depth. 


## 🔐 Next Step
Now let's move onto **level 20**. 

➡️ [Continue to Level 20 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2020.md)
