# Bandit Level 26 → 27
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit27.html)

## 📝 **Challenge Description**  
The level description states to hurry up and grab the password for `bandit27` however it is not that simple 🫢.

## 🔍 **What I Initially Tried**  
Based on the previous level, I knew that `bandit26` wouldn't have an interactive terminal to work with since the shell automatically exits if we don't minimize the window **(look at the previous level's writeup and you'll see what I'm talking about)**. 

I had a feeling that I needed to find a way to spawn a terminal in `vim` to allow us to gain access to a usable shell for user `bandit26`. After some research I stumbled across the [Vim github repo](https://github.com/vim/vim/tree/master) and found a specific feature built in to spawn a terminal. This would allow me to get out of the mess and work with a terminal to find the password for `bandit27`.

## ✔️ What Worked
When I entered the `vim` text editor **(discussed on how I got in the previous level's writeup)**, I typed this in:
```
:term bash
```
This feature runs a terminal emulator in a Vim window **(this is amazing shoutout to the developers I aspire to be like you guys)** and allow us to bypass the restricted terminal and interact with user `bandit26`. From there I listed out the files to see if there was anything I can use to find `bandit27`'s password:
```bash
ls
bandit27-do text.txt
```
We have a **setuid binary** we can use to allow us to run commands with `bandit27`'s permissions. So I used that to open and read `bandit27`'s password file:
```
./bandit27-do cat /etc/bandit_pass/bandit27
# Output:
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```
There you have it, the password for `bandit27`.


## 🧠 Key Learnings
- Learned how to spawn a terminal using built in features in `vim`.
- Utilized a **setuid binary** to temporarily execute privileged commands.




## 🔐 Next Step
Now let's move onto **level 27**. 

➡️ [Continue to Level 27 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2027.md)
