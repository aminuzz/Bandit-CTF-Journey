# Bandit Level 3 → 4

## 📝 **Challenge Description**  
In Level 4, the password for `bandit4` is hidden in a file. According to the instructions:

> The password is stored in a **hidden file** in the **`inhere`** directory.

This level introduces the concept of hidden files — the kind that don’t show up with a regular `ls` command.

---

## 🔍 **What I Initially Tried**  
At first, I saw a folder named `inhere` in the home directory. For a moment, I thought it might be a special file, so I tried opening it with `cat` like this:
```bash
cat inhere
```
But that didn't work - the terminal threw an error. Then I realized something important: **directories are usually shown in blue in the terminal** (at least with color support), which is a clue that `inhere` is a folder, not a regular file. 
So I switched gears and moved into it:

```bash
cd inhere
```
Then I ran:
```bash
ls
```
...and nothing showed up. Empty? Nope — that's when I remembered hidden files start with a `.` and aren't displayed by default.

## ✔️ What Worked
To list all files — including hidden ones — I used:
```bash
ls -a
```
That showed a file named: 
```bash
.hidden
```
I opened it with:
```bash
cat .hidden
```
And there was the password for `bandit4`.

## 🧠 Key Learnings
- A folder is often displayed in blue text in the terminal — that's a quick visual cue.
- Hidden files (those starting with a `.`) aren't shown with a normal `ls` — you need `ls-a`.
- You can't `cat` a directory — it'll throw an error because it's not a readable file.
- Sometimes the key is just knowing what *kind* of thing you're dealing with (directory vs file vs hidden file).

## 🛠️ Tools Used
**Cygwin**, still going strong. The colored output it provides really helped me catch that `inhere` was a directory — small things like that can save you from chasing the wrong path. 

## 🔐 Next Step
We've got the password! The next level adds a bit more complexity — it's about finding a specific line based on its attributes like size and permissions. Let's go. 

➡️[Continue to Level 5 →](level5.md)
