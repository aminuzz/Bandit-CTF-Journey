# Bandit Level 13 → Level 14
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit14.html)

## 📝 Challenge Description 
In this level, the password for `bandit14` is stored in the file with this path: `/etc/bandit_pass/bandit14` and it can only be read by user **bandit14**. It also states that for this level, you don't get the next password however you get a **private SSH key** that can be used to log in to the next level. The level also notes that **localhost** is a hostname that refers to the machine you are working on.

## 🔍 What I Initially Tried
After some digging, I learned that SSH is more than just a secure remote connection protocol. It uses public-key cryptography to authenticate users securely.

In a typical setup, you generate a pair of keys: a public key and a private key. The public key is placed on the remote server `(in ~/.ssh/authorized_keys)`, and the private key stays on your local machine. When you initiate an SSH connection, the server sends a challenge. Your client signs it using your private key, and the server verifies the signature using the public key. If the verification succeeds, you’re granted access, all without ever sending your private key over the network.

Moving on, the term `localhost` refers to the **loopback network interface**, which essentially means your **own machine**. When you connect to `localhost`, you're communicating with your device via network protocols without ever leaving it. 

It's commonoly associated with the IP address `127.0.0.1` (IPv4) or `::1` (IPv6), and it's often used for **testing, development, or running services locally** like web servers, APIs, etc. 

## ✔️ What Worked
Now with this mind, after reading the [ssh man page](https://linux.die.net/man/1/ssh) I ran this command:
```bash
ssh -i sshkey.private bandit14@localhost -p 2220
```
- The `-i` flag specifies the private key file we want to use for authentication.
- We are connecting as the user `bandit14` on `localhost`, which refers to the same machine we are currently on (on the `bandit13` server).
- Since the private key for `bandit14` is already provided to us on the `bandit13` account, we can authenticate **without needing the password**.

Once logged in as `bandit14`, I retrieved the password using:
```bash
cat /etc/bandit_pass/bandit14
# Output: MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```


## 🧠 Key Learnings
- Learned how to utilize a **private key** to authenticate an SSH connection via logging in through `localhost`

## 🛠️ Tools Used 
**Terminal:** Cygwin  
**Commands:** `ssh`

## 🔐 Next Step
We’ve successfully grabbed the password and are ready for **Level 14**. 

➡️ [Continue to Level 14 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2013.md)
  
