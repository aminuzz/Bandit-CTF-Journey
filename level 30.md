# Bandit Level 30 → 31
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit31.html)

## 📝 **Challenge Description**  
Like in the previous level, there is a repository at `ssh://bandit30-git@localhost/home/bandit30-git/repo` via the port `2220`. We have to look into the repository and get the password for the next level. 

## 🔍 **What I Initially Tried**  
After cloning the repo in a temporary directory, I opened the `README.md` file:
```
cat README.md
just an epmty file... muahaha
```
This was strange to me, my assumption was that it might've been similar to the previous level where the password might be located in a hidden branch however this file doesn't tell us anything about the whereabouts of the password. After some research I found that `git` stores objects in **pack files**. These files contain everything from trees, hashes, commits, etc and compresses them down to one singular object. The idea behind this was that one of these **pack files** had to have the password stored in them so I decided to investigate into these files.
## ✔️ What Worked
This is how I did it:

- First these **pack files** are stored in the **objects** folder so I went on ahead and went in there (while being in the `./.git` folder):
```bash
cd objects/pack
```
- Then I listed out the packs:
```bash
ls -a
.
..
pack-fb4d3237fb2b275d738048ba45fc6e5df5d035ba.idx
pack-fb4d3237fb2b275d738048ba45fc6e5df5d035ba.pack
pack-fb4d3237fb2b275d738048ba45fc6e5df5d035ba.rev
```
From there using `git verify-pack`, I listed out the objects that was stored in the first **pack file**:
```
git verify-pack -v pack-fb4d3237fb2b275d738048ba45fc6e5df5d035ba.idx

738048ba45fc6e5df5d035ba.idx
2d17b02cae752006514a3c2695edc44611e5f0c0 commit 194 138 12
84368f3a7ee06ac993ed579e34b8bd144afad351 blob   33 43 150
bd85592e905590f084b8df33363a46f9ac4aa708 tree   37 48 193
029ba421ef4c34205d52133f8da3d69bc1853777 blob   30 38 241

```
- Since the pack had a `.idx` ending to it this meant that this pack stores hashes of the objects that are stored in here. From there I saw two hashes that piqued my interests. Both being **blobs** which only display the contents of a file and no other information. I opened the first **blob** and stumbled across the password:
```bash
git cat-file -p 84368f3a7ee06ac993ed579e34b8bd144afad351
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
```



## 🧠 Key Learnings
- Learned the basics of what a **pack file** is and what type of data it stores.
- Learned how to unpack a **pack file** via the `git verify-pack` command and differentiating the objects based off the information given.
- Learned how to open a **blob** by using its hash and feeding it into the `git cat-file` command. 




## 🔐 Next Step
Now let's move onto **level 31**. 

➡️ [Continue to Level 31 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2031.md)
