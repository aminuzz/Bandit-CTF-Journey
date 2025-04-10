# Bandit Level 2 → 3

📝 **Challenge Description**  
In Level 3, the goal is to retrieve the password for `bandit3`. This time, the challenge says:

> The password is stored in a file called "spaces in this filename" located in the home directory.

This is another lesson in how filenames with special characters — in this case, *spaces* — can mess with the terminal if you're not careful.

---

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
