# Bandit Level 21 → 22
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit22.html)
## 📝 **Challenge Description**  
The password for this level is a bit obsecure: A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d** for the configuration and see what command is being executed. From there, you can obtain the password. 



## 🔍 **What I Initially Tried**  
My first thought was, what is **cron** I've never heard of this before. The description did give me a hint it had something to do with automation but that wasn't the full picture:
- `cron` is the *daemon* (background service) that keeps running and checks if there's anything scheduled to execute. This can include updates, backups, scripts, etc. 
- When the time matches a job's schedule, `cron` executes the command/script you specified.

Each cron job has this format:
```
MIN HOUR DOM MON DOW COMMAND
```
Where:
- MIN → minute (0–59)
- HOUR → hour (0–23)
- DOM → day of month (1–31)
- MON → month (1–12)
- DOW → day of week (0–7, Sunday=0 or 7)
- COMMAND → script or command to run

In order to find the `cron` job that was running for `bandit22` I had to look into the system-wide cron job folder to see what was going on:
```bash
cd /etc/cron.d
ls
behemoth4_cleanup  cronjob_bandit23  leviathan5_cleanup    sysstat
clean_tmp          cronjob_bandit24  manpage3_resetpw_job
cronjob_bandit22   e2scrub_all       otw-tmp-dir
```

`cronjob_bandit22` caught my attention so I decided to open it to see what the script looked like:
```bash
cat cronjob_bandit22
# Output:
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```
This script runs **immediately after a reboot** and it **also runs every minute forever** after that. 


## ✔️ What Worked

## 🧠 Key Learnings


## 🔐 Next Step
Now let's move onto **level 22**. 

➡️ [Continue to Level 22 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2022.md)

