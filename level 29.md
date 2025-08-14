# Bandit Level 29 → 30
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit30.html)

## 📝 **Challenge Description**  
Like the previous level, there is a git repository at `ssh://bandit29-git@localhost/home/bandit29-git/repo` via the port `2220`. We have to clone the repository and find the password for the next level.

## 🔍 **What I Initially Tried**  
After cloning the repository I opened the `README.md` file to see if there was any information about the password for `bandit30`. This is what the `README.md` file stated:
```
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>
```
So I asked myself this, what do they mean by **no passwords in production**?
- This could mean many things but the most logical answer I had was that the password was never **pushed** (updated) to the main branch. For example if you're a developer and you're working on a feature for your app locally however the feature never got implemented, then this would be the reason why. The update exists somewhere but not in the final live code.

With this in mind, how can we find this update? We now have to dig deeper on how `git` works.
## ✔️ What Worked
With this assumption in mind, this is what I did:
```bash
git branch -a
# Output:
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
```
This command lists out all of the branches that exists. This includes local and remote branches. My assumption was that there had to be a branch where the developers of this level used for testing and the one that caught my eye was `remotes/origin/dev`. This was the development branch so I decided to head into that branch:
```bash
git checkout remotes/origin/dev
ls -l
drwxrwxr-x 2 bandit29 bandit29 4096 Aug 14 17:12 code
-rw-rw-r-- 1 bandit29 bandit29  134 Aug 14 17:12 README.md
```
The password for the next level is seen after opening the `README.md` file:
```
cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
```





## 🧠 Key Learnings
- Learned how to list all local and remote branches in a git repository.
- Learned how to switch my working directory to another existing branch. 




## 🔐 Next Step
Now let's move onto **level 30**. 

➡️ [Continue to Level 30 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2030.md)
