# Bandit Level 22 → 23
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit23.html)
## 📝 **Challenge Description**  
Similar to the previous level, a program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d** for the configuration and see what command is being executed. 



## 🔍 **What I Initially Tried**  
Like in the previous level, I went into `/etc/cron.d` to view the **system-wide** cronjobs:
```bash
cd /etc/cron.d
ls
behemoth4_cleanup  cronjob_bandit23  leviathan5_cleanup    sysstat
clean_tmp          cronjob_bandit24  manpage3_resetpw_job
cronjob_bandit22   e2scrub_all       otw-tmp-dir
```
From there I opened `cronjob_bandit23` to see how this **cronjob** behaved:
```bash
cat cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```
Like the previous level's **cronjob**, it runs after reboot and forever after that so I decided to look into contents of the script that was responsible for this:
```bash
cat /usr/bin/cronjob_bandit23.sh
# Output:
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"
```
Here’s how the script works:
- First the script initializes the variable `myname` to be equal to the output of the `whoami` command.
- Then it hashes a sentence with `myname` via the MD5 hash algorithm and saves it into a variable called `mytarget`.
- Then the program prints out the password being copied to a file within the temporary directory. That file is the hash that is saved in the variable `mytarget`.


This is where I got stuck:
- I tried running the script however it only saved the password for user `bandit22` in the temporary directory but not for user `bandit23`.
- I assumed that I needed to find a way to SSH into `bandit23` and run the script as `bandit23` however that wouldn't work since I didn't have the necessary permissions.

However, I came to the realization that these **cronjobs** are system-wide meaning that it didn't matter if `bandit23` ran the script, `bandit22` can still see the output of the hashing process. Since we already have the username, all I had to do was just replicate the hash and open the file myself.

## ✔️ What Worked
This is what I ran:
```bash
echo I am user bandit23 | md5sum | cut -d ' ' -f 1
# Output:
8ca319486bfbbc3663ea0fbe81326349
```
Since I replicated the hash of the string, all we have to do is open up that file with that hash in the temporary directory:
```bash
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
# Output:
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```
There you go, the password for `bandit23`. 

## 🧠 Key Learnings
- Learned how to reverse engineer a Bash script to get a desired outcome.
- Cron jobs can run as any specified user, regardless of which account you’re logged into.
- All Bandit “machines” are actually user accounts on the same server, meaning their cron jobs are visible system-wide.
- Predictable filenames from hashing known values is a common security flaw. If the input is guessable, so is the output.


## 🔐 Next Step
Now let's move onto **level 23**. 

➡️ [Continue to Level 23 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2023.md)
