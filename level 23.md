# Bandit Level 23 → 24
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit24.html)
## 📝 **Challenge Description**  
In this level like previous levels, there is a program that's running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d** for the configuration and see what command is being executed.

## 🔍 **What I Initially Tried**  
As usual I went into `/etc/cron.d` to view the **system-wide** cronjobs to see if there's any jobs that dealt with `bandit24`:
```bash
cd /etc/cron.d
behemoth4_cleanup  cronjob_bandit22  cronjob_bandit24  leviathan5_cleanup    otw-tmp-dir
clean_tmp          cronjob_bandit23  e2scrub_all       manpage3_resetpw_job  sysstat
```
I noticed **cronjob_bandit24** so I decided to open it:
```bash
cat cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
```
As per usual the **cronjob** is ran as `bandit24` and it runs after reboot then it continuously runs forever. So I decided to open the script to see what the **cronjob** is doing:
```bash
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```
Here's how the script works:
- Since this script runs as the user `bandit24` the variable `myname` will be initialized to the `bandit24`.
- Then the script changes the directory to `/var/spool/bandit24/foo` and prints out `Executing and deleting all scripts in /var/spool/$myname/foo`. This basically sums up what the script does, it executes and deletes all scripts in `var/spool/bandit24/foo` however if the owner of one of the files is `bandit23`, then it'll run that script for 60 seconds then remove it after it is done executing.

Based on this script my assumption was that I had to create my own **Bash** script that would allow me to read the password for `bandit24` and save it in a temporary file. Then I could copy that file to the specified directory and since the **cronjob** is running as `bandit24`, my script would have the permissions (as user `bandit24`) to read the password and write to the password file thus exploiting the **cronjob**. Having a copy of the script and password file in a temporary directory would be necessary just in case if I messed up and had to start again. This is what I did:
```bash
mktemp -d
/tmp/tmp.2Kh9HXGaH8

vi script.sh
touch password.txt
```

## ✔️ What Worked
First I had to create the script that would allow me to read `bandit24`'s password and save the output to `password.txt`:
```bash
#!/bin/bash

cat /etc/bandit_pass/bandit24 > /tmp/tmp.2Kh9HXGaH8/password.txt
```
From the looks of it, it's a very simple Bash script however I felt proud since I never understood Bash and now I am using it solve problems. Moving on, I made sure the permissions for both files were set up and for the directory:
```bash
chmod 777 /tmp/tmp.2Kh9HXGaH8
chmod 777 password.txt
chmod 777 script.sh
```
Quick note:
- Now looking back having the permissions set up to **777** is a bad practice since anyone on the system can access the directories and all of the files within them. I only did this just to save some time but moving foward I'll be making sure I set up appropriate permissions as good practice. 

Then I copied the script (while being in the tmp directory) to the target directory `/var/spool/bandit24/foo` and waited about a minute:
```bash
cp script.sh /var/spool/bandit24/foo
```

After a minute I went back into the temporary directory and opened `password.txt` to see if the password was saved in it:
```bash
cd /tmp/tmp.2Kh9HXGaH8
cat password.txt
```

The password for the next level was displayed on the screen:
`gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8`

## 🧠 Key Learnings
- Wrote a basic Bash script to exploit a **cronjob** to help us get the password for the next level.
- Learned how to manage permissions for files and directories (safely and unsafely).
- Learned how to read and understand if statements in Bash.



## 🔐 Next Step
Now let's move onto **level 24**. 

➡️ [Continue to Level 24 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2024.md)
