# Bandit Level 31 → 32
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit31.html)

## 📝 **Challenge Description**  
Like the past few levels, there is a git repository at `ssh://bandit31-git@localhost/home/bandit31-git/repo` via the port `2220`. The password for the next level is somewhere in the repository. In this case we have to push a file to the repository and we'll get the password for the next level.
## 🔍 **What I Initially Tried**  
After navigating into the directory and looking through the `README.md` file, the solution looked simple to me:
- All I had to do was create a file called `key.txt` with the contents `May I come in?` and push it to the **master branch**.

After unsucessfully trying to push the file to the main branch I stumbled across the `.gitignore` file which had this in it:
```
*.txt
```

This meant that any files with the `.txt` extension would be ignored by the repository hence why the earlier attempt didn't work. I needed to find a way to get around this and after a simple search, I found my answer.
## ✔️ What Worked
This is what I did:
```
git add -f key.txt
git add .
git commit -m "Added key.txt"
git push origin master
```
The `-f` flag allows us to add ignored files stated by `.gitignore`. From there after inputting the credentials of the current level I got the password for `bandit32`:
```
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 2 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 326 bytes | 326.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: ### Attempting to validate files... ####
remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
remote: Well done! Here is the password for the next level:
remote: 3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
```



## 🧠 Key Learnings
- Learned how to add, stage, commit, and push a otherwise ignored file to a remote repository through the command line.
- Learned how to get around the `.gitignore` file by using `-f` flag on the `git add` command. 


## 🔐 Next Step
Now let's move onto **level 32**. 

➡️ [Continue to Level 32 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2032.md)
