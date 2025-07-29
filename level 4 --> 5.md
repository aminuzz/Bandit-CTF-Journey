# Bandit Level 4 → 5
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit5.html)
## 📝 Challenge Description
The instructions for Level 5 state:

> The password for the next level is stored in a file somewhere in the `inhere` directory, **which is human-readable**, **1033 bytes in size**, and **not executable**.

This level steps things up — it’s not just about finding a specific file name anymore, but filtering files based on multiple conditions. It’s a great introduction to chaining command-line tools.



## 🔍 What I Initially Tried 
I first needed to understand what exactly "human-readable" meant. After some digging and experimenting, I learned that the `file` command is a useful tool for determining the type of contents in a file. For example:
```bash
file myname.txt
```
Would output something like:
```
myname.txt: ASCII text
```
This told me that if a file contains "ASCII text", it's considered human readable — i.e., readable by us (plain text or numbers).
So now the task was to:
- Navigate into the `inhere` directory
- Loop through the files in there
- Check which one is human-readable (ASCII)
I ran:
```
cd inhere
ls
```
And saw 10 files with names like `-file00`, `-file01`, etc.

## ✔️ What Worked
To filter out just the file we needed, I used the `find`, `file`, and `grep` commands together. 
Here's the command that worked:
```
find . -type f -exec file {} \; | grep "ASCII text"
```
Let me break it down:
- `find . -type f` specifies the search to files (not directories) in the current directory.
- `-exec file {} \;` runs the `file` command on each of those files. `{}` is replaced by each filename, and `\;` ends the command.
- The output of `file` is piped into `grep` to filter only those files containing "ASCII text". This narrowed it down to a single file that matched.
Then I ran this command:
```
cat ./-file07
```
(You might have to escape or use `./` due to the dash in the filename). 
And there it was — the password for `bandit5`!

## 🧠 Key Learnings
- The `file` command is super useful for identifying what type of data a file contains.
- A "Human-readable" file contains text and numbers. 
- Combining `find`, `file`, and `grep` gives powerful ways to filter through lots of files with specific criteria.
- Command-line power really comes from chaining small, focused tools togther.

## 🛠️ Tools Used 
Still using Cygwin here, though this would work on any UNIX-like terminal — WSL, macOS Terminal, native Linux, etc. The real win here was learning how to make use of `find` and `file` together effectively. 

## 🔐 Next Step
Now that we've got the password, we can move on to the next level which is similar to this one however there are more requirements for the **human readable file**. 

➡️ [Continue to Level 6 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%205%20--%3E%206.md)
