# Bandit Level 28 → 29
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit29.html)

## 📝 **Challenge Description**  
Like the previous level, there is a git repository at `ssh://bandit28-git@localhost/home/bandit28-git/repo` via the port `2220`. We have to clone the repository and find the password for the next level.

## 🔍 **What I Initially Tried**  
Very similar to the previous level I had to clone the repository in a temporary directory:
```bash
mktemp -d
/tmp/tmp.6DfXRwcwDZ
cd /tmp/tmp.6DfXRwcwDZ
git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo
```

After looking into the repo I opened the `README.md` file to see if that had any information about the password:
```
cd repo
ls
cat README.md
```
This was the output:
```
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```
Since the password is not stated in here, the password has to be somewhere within the repo. With `git` we can any file changes, uploads, etc that happens in the repo so my thought process was there had to be a commit with the password in it. 
## ✔️ What Worked
Based on my assumption this is what I did:
```bash
ls -a
. .. .git README.md
```
All of the files, changes, commits, etc are all stored in the **.git** folder so I went in there and checked the log history using `git log` to see the logs of the commits. Combine that with the `-p` flag which shows the differences in each commit, the password was right there:
```
cd ./.git
git log -p
```
Output:
```
commit 03c4d9be32dd9d43d35ae4da0b42ca2a64dfa60b (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Mon Jul 28 19:03:48 2025 +0000

    fix info leak

diff --git a/README.md b/README.md
index d4e3b74..5c6457b 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials

 - username: bandit29
-- password: 4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
+- password: xxxxxxxxxx


commit 5ce2fc341ca715d03961781a40988477cc95de7d
Author: Morla Porla <morla@overthewire.org>
Date:   Mon Jul 28 19:03:48 2025 +0000

    add missing data

diff --git a/README.md b/README.md
index 7ba2d2f..d4e3b74 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials

 - username: bandit29
-- password: <TBD>
+- password: 4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7


commit 428350b04db7581254a1324e6ab5abeed0c5b3ec
Author: Ben Dover <noone@overthewire.org>
Date:   Mon Jul 28 19:03:48 2025 +0000

    initial commit of README.md
```
Using `git log` we can view the history of commits starting from the top one being the most recent all the way to the bottom being the first commit. As you can see, the 2nd commit had the password field as `TBD` but it was changed to the password for the next level which is `4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7`.




## 🧠 Key Learnings
- Learned how to use `git log` to analyze commit history for a repository.
- Learned how to analyze individual commits to find differences within the code. 




## 🔐 Next Step
Now let's move onto **level 29**. 

➡️ [Continue to Level 29 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2029.md)
