# Bandit Level 8 → Level 9
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit9.html)
## 📝 Challenge Description 
In this level, the password for `bandit9` is stored in the file called `data.txt` and is the only line of text that occurs only once. 







## 🔍 What I Initially Tried 
Coming into this level, I assumed it would be similar to the previous one which was filtering out unnecessary lines to find the password. So I started by sorting the file:
```bash
sort data.txt
```
That didn’t help much because `sort` just arranges the lines alphabetically, but the challenge is to find the only line that appears once. I checked the [sort command manual page](https://man7.org/linux/man-pages/man1/sort.1.html) and found the `-u` flag, which removes duplicates:

```bash
sort -u data.txt
```
But that backfired. It removed all duplicates and the unique line I was looking for, since it only keeps one instance of each line meaning we can't tell which ones were truly unique.

Then I noticed the `uniq` command in the hint section. Reading the [uniq man page](https://man7.org/linux/man-pages/man1/uniq.1.html), I learned the -u flag prints only lines that appear once in a row. To make that work properly, the input needs to be sorted first. That’s where [piping](https://ryanstutorials.net/linuxtutorial/piping.php) came in—I could combine both commands to isolate the unique line.



## ✔️ What Worked
So this is the command I ended up using:
```
sort data.txt | uniq -u
```
**What this does:**
- `sort data.txt`: sorts the lines of text in data.txt (in alphabetical order)
- `| uniq -u`: use the output of the previous command and use it as input for this command which prints unique lines of text
From the output of this command, I found the password:
```
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```
And there it was the password for `bandit9`!


## 🧠 Key Learnings
- Reading through **man pages** is an important skill when learning the basics of Linux because it provides all of the documentation you need for that specific command.
- Again reading the question carefully and understanding what the question is asking is very important especially when it comes to solving these puzzles. 


## 🛠️ Tools Used 
Terminal: Cygwin
Commands: `sort`, `uniq`. 
Before this, reading documentation wasn't something I considered much however from now on if I am confused on how a command works, I'm going to read through the documentation first and look for examples on how it is used. 

## 🔐 Next Step
We’ve successfully grabbed the password and we're ready for **Level 9**. 

➡️ [Continue to Level 9 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%209%20--%3E%2010.md)

