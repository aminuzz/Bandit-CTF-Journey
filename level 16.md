# Bandit Level 16 → Level 17
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit17.html)

## 📝 Challenge Description 
In order to move on to the next level, we must submit the password of the current level to a **port on localhost in the range 31000 to 32000**. We have to find out which of these ports have a **SSL/TLS** server running on them. Only **1** of them will give you the credentials for the next level, the others will simply reply back to you whatever you send to it.



## 🔍 What I Initially Tried
Based off the level description I knew we had to utilize `nmap` in a way where I could scan specific ports on localhost. After reading through the [nmap man page](https://svn.nmap.org/nmap/docs/nmap.usage.txt) I found that we can specify the what port ranges we want to scan using the `-p` flag. Also since we need to find which specific ports have the **TLS** service running on them, the `-sV` flag allows us to determine the service/version information for each port. 

Here's the command:
```bash
nmap -sV -p 31000-32000 localhost
```
After a minute, `nmap` shows these ports that are open:
```text
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-08-05 21:04 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00011s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
```

Based off the `nmap` scan, I noticed two ports were open that had **ssl** running on them, port `31518` and port `31790`. Instinctively I tried initiating a connection to the first port:
```bash
openssl s_client -connect localhost:31518
```
Like usual it outputted the certifcate so I tried pasting in the password for the next level, however that didn't work:
```text
read R BLOCK
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
KEYUPDATE
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
KEYUPDATE
closed
```

I kept getting a **KEYUPDATE** message and I didn't know what this really meant so I looked through the [openssl/s_client documentation](https://docs.openssl.org/3.0/man1/openssl-s_client/#options) to see why this could happen. 

Under the **CONNECTED COMMANDS** section, I was quick to find out why this message kept appearing:
```
k
Send a key update message to the server (TLSv1.3 only)
```
The reasoning behind this is that certain commands are treated differently when sending text back to the server and in this case the **letter k** sends a key update message back to the server hence why the message **KEYUPDATE** kept appearing on my end. The letters **Q, R, k, and K** all have special functions that come with them so in order to ignore them, the documentation says to use the `-quiet` flag:

```bash
openssl s_client -quiet -connect localhost:31518
```
This was the output:
```
Can't use SSL_get_servername
depth=0 CN = SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = SnakeOil
verify return:1
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```
As you can see, the password I pasted was echoed back to the terminal meaning that port `31790` had to be the correct port. Also looking back, you can see that port `31518` had both `ssl/echo` services on running on it showing another clear indication that the other port was the correct one.

## ✔️ What Worked
After all of that this is what I ran:
```bash
openssl s_client -quiet -connect localhost:31790
```

This gave us a **RSA Private Key** to allows us to log in to the next level:
```
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----
```

From there, to get the password for the next level I needed to save this key in a file where I can use it to `ssh` into the next level however I didn't have permission to write files within the home directory so I had create a temporary one and do it from there. Here's what I did:
```bash
mktemp -d 
# Output: /tmp/tmp.l8GVcgokHN
cd /tmp/tmp.l8GVcgokHN
vi key.txt
# Pasted the key into this file
chmod 600 key.txt
# Made sure the key wasn't accessible by others
ssh -i key.txt bandit17@bandit.labs.overthewire.org -p 2220
cat /etc/bandit_pass/bandit17
```

After everything, this was the password for **bandit17**:
```
EReVavePLFHtFlFsjn3hyzMlvSuSAcRD
```

## 🧠 Key Learnings
- Learned how to scan specific ports using `nmap` and scan for specific services.
- Learned how to effectively read through documentation to solve a specific problem for a command.
- Utilized a private RSA key to log in to another machine and making sure the permissions were set correctly on it.
## 🛠️ Tools Used 
**Terminal:** Cygwin  
**Commands:** `nmap`, `openssl`, `s_client`, `vim`, `ssh`, `mktemp`, `cd`

## 🔐 Next Step
We’ve successfully grabbed the password and are ready for **Level 17**. 

➡️ [Continue to Level 17 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2017.md)
  
