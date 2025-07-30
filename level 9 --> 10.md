# Bandit Level 9 → Level 10
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit10.html)

## 📝 Challenge Description 
In this level, the password for `bandit10` is stored in the file `data.txt` in one of the few-human readable strings, preceded by several **'='** characters. 







## 🔍 What I Initially Tried 
At first, I opened `data.txt` with the cat command to see what was in the file since the level states that the password is one of the few-human readable strings in the file, so I was assuming most of the file wasn't human readable:
```bash
cat data.txt
```
And guess what, my intuition was correct. Most of the file wasn't in human readable text (either compiled or binary data) so I needed to find a way to look for human readable strings in the file. In order to find human readable text (strings) in a file we have to make use of the `strings` command. This will return all of the strings present a specified file. Combine that with the `grep` command to pinpoint the exact location of the password, this should help us solve this level.  


## ✔️ What Worked
So here's the command I ended up using:
```
strings data.txt | grep "=" 
```
**What this does:**
- `strings data.txt`: filters out and outputs strings that are in data.txt
- `| grep "="`: takes the strings that we found from the previous command and outputs the ones that contain "=" signs. 
This was the output of the command:
```
^y=7
=?t)
=&]'
========== the
If=q
U.=4!
k={7
lTOB=
YZ=*
D========== password
w========== is
=*{>
=wu,
h=O"
4,=Y
*y=1
4=+0
7]J=0
zSKc=
]2m==
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
t|HfY=
```
As you can see, the level stated that the password is preceded by a couple of equal signs and based off the output, we can see that the 2nd to last string contains the password for `bandit10`. 


## 🧠 Key Learnings
- Combining the `string` and `grep` commands together helps us locate certain patterns in strings no matter what the contents of the file.
- Using the `grep` command as a placeholder to look for patterns becomes very useful when solving puzzles like this one since you don't have to manually look through each string to find the password for this particular case. 


## 🛠️ Tools Used 
Terminal: Cygwin.
Commands: `string`, `grep`, `cat`
I'm feeling even more confident with my Linux skills, I know there's much more intricate things about Linux and interacting with the command line but I am enjoying every bit of it.


## 🔐 Next Step
We’ve successfully grabbed the password and are ready for **Level 10**. 

➡️ [Continue to Level 10 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level9.md)


