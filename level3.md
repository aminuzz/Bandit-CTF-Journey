# Bandit Level 2 → 3

📝 **Challenge Description**  
In Level 3, the goal is to retrieve the password for `bandit3`. This time, the challenge says:

> The password is stored in a file called "spaces in this filename" located in the home directory.

This is another lesson in how filenames with special characters — in this case, *spaces* — can mess with the terminal if you're not careful.



🔍 **What I Initially Tried**  
I started by listing the files like usual:
```
ls
```
And sure enough, I saw the file listed as:
```
spaces in this filename
```

So I tried to run:
```
cat spaces in this filename
```
But that didn't work. The shell interpreted each word as a separate argument, so `cat` thought I was aksing it to read multiple files named `spaces`, `in`, `this`, and `filename` - none of which existed. 

## ✔️ What Worked
To handle spaces in filenames, I wrapped the filename in quotes:
```
cat "spaces in this filename"
```
Alternatively, using escape sequences also works:
```
cat spaces \\ in\\ this\\ filename
```
Either of those methods told the shell to treat the whole thing as one file name, and I was able to read the password for `bandit3`. 

## 🧠 Key Learnings
- Spaces in the filename must be either quoted `("file name")` or escaped `(file\\ name)`.
- The shell splits command arguments based on spaces, so filenames with spaces need special handling.
- Always check `ls` to see exactly how the filename appears - don't guess.
- This level builds more comfort with shell syntax and escaping characters.

## 🛠️ Tools Used
Still on Cygwin. At this point, I'm getting comfortable with basic shell usage and reading through the documentation for certain terminal commands. 

## 🔐 Next Step
Now that we've got the password for `bandit3`, the next level introduces hidden files. 

➡️ [Continue to Level 4 →](level4.md)
