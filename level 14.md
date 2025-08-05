# Bandit Level 14 → Level 15
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit15.html)

## 📝 Challenge Description 
In this level, the password for `bandit15` can be retrieved by submitting the password of the current level to **port 30000 on localhost**. 

## 🔍 What I Initially Tried
Reading through the requirements for this level, I needed to understand how I could submit data to a specific **port** — in this case, **30000** on `localhost`. But before I could do that, I had to figure out **what kind of service** or **protocol** was listening on that port.

To start, I used the `nmap` command to scan the open TCP ports on `localhost` and get an idea of what services might be running:

```bash
nmap localhost
# Output:
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-08-05 03:20 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00026s latency).
Not shown: 992 closed tcp ports (conn-refused)
PORT      STATE SERVICE
22/tcp    open  ssh
1111/tcp  open  lmsocialserver
1840/tcp  open  netopia-vo2
4321/tcp  open  rwhois
4444/tcp  open  krb524
8000/tcp  open  http-alt
30000/tcp open  ndmps
50001/tcp open  unknown
```

Based on the challenge, I was expecting that port 30000 was waiting for a TCP connection that if I submitted the password for `bandit14`, in response I would get the password for `bandit15`. This is an example of the **client-server model** where I was the client and I was expecting something from the server, in this case the password for the next level. 

## ✔️ What Worked
To solve this level, I used `netcat` (`nc`) to initiate a **TCP connection** to `localhost` on port 30000 since:
- `nmap` showed port 30000 as **open**,
- by default, both `nmap` and `nc` work over **TCP**, and
- the challenge stated that I needed to **submit** the password to that port, which strongly implies a single TCP request-response setup.

The command I used was:
```bash
nc localhost 30000
```

After running that, I simply **pasted the password** for `bandit14` into the terminal and hit **Enter**. In response, the **server running on port 30000 (which is `localhost`, the same machine) returned the **password for bandit15**. The password was: 
```text
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```



## 🧠 Key Learnings
- Learned how to scan for open TCP ports on a device using `nmap`
- Also learned how to utilize the **client-server model** in this case, I acted as the client requesting for information from the server running on **localhost** using `netcat`.
- After some more research, the exact terminology for this process is this; using `netcat` to open a **raw TCP connection** which acts like a **socket** it allows us to send text as input and recieve a response from the service listening on that port. This is an example of a **TCP socket**. 

## 🛠️ Tools Used 
**Terminal:** Cygwin  
**Commands:** `nc`, `nmap`

## 🔐 Next Step
We’ve successfully grabbed the password and are ready for **Level 15**. 

➡️ [Continue to Level 15 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2015.md)
