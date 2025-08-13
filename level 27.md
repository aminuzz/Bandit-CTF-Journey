# Bandit Level 27 → 28
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit28.html)

## 📝 **Challenge Description**  
There is a git repository at `ssh://bandit27-git@localhost/home/bandit27-git/repo` via the port `2220`. The password is located within the repository. Note that the password for the user `bandit27-git` is the same as for the user `bandit27`.

## 🔍 **What I Initially Tried**  
From previous experience in order to solve this level, we have to **clone** this repository onto `bandit27`'s machine and look for a file that contains the password. But cloning via **SSH** works a bit differently when compared to cloning via **HTTPS**:
- Cloning over **SSH** is far more secure compared to **HTTPS** because there are no credentials being passed over the network, only cryptographic signatures.
- It is also a lot harder for attackers to intercept or brute-force compared to credentials sent over **HTTPS** where attackers can have the chance to intercept network traffic and steal them.
  
So overall, cloning via **SSH** is the safer option however using **HTTPS** is easier to set up and maintain. 
## ✔️ What Worked
Moving on, how can we use `git clone` to solve this level? It's fairly simple. Before we do anything, let's create a temporary directory:
```bash
mktemp -d
/tmp/tmp.3ovzPl9DXW
cd /tmp/tmp.3ovzPl9DXW
git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo
```
`git clone` allows us to clone the repository onto our local machine (in this case `bandit27 server`). This gives us a copy of the repository to work with so if we were to make changes, it wouldn't affect the original repository. This is effectively why `git` is so important, it allows us to track, make changes, and copy code without the huge headache of doing everything manually. 

From there I navigated into the `repo` folder to find a `README` file which contained the password for the next level:
```bash
cd repo
ls
README
cat README
The password to the next level is: Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```



## 🧠 Key Learnings
- Learned how to clone a git repository via **SSH**.
- Learned how **git** can help us track, modify, copy, and merge code all through a command line interface. 




## 🔐 Next Step
Now let's move onto **level 28**. 

➡️ [Continue to Level 28 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2028.md)
