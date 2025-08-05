# Bandit Level 15 → Level 16
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit16.html)

## 📝 Challenge Description 
In this level, the password for `bandit16` can be retrieved by submitting the password of the current level to **port 30001 on localhost** using SSL/TLS encryption. 

## 🔍 What I Initially Tried
At first I was confused on what SSL/TLS encryption meant so I did my research like usual and this is what I found. 

**SSL/TLS** are cryptographic protocols that are used to ensure that data is transmitted securely over a network. The protocol does it in three ways: 

- **Encryption**: No one can read your data while it's in transit (protects confidentiality)
- **Authentication**: Confirms you're really talking to the right server (e.g., accessing a bank website)
- **Integrity**: Ensures the data wasn't tampered with in transit (via checksums or verifying MAC addresses)

The most common example of **SSL/TLS** being used and the one that we all deal with is when we browse the internet and you see the green lock to the left of the URL. When you click on it, you can see the certificate that the protocol generates ensuring a secure connection to that particular website. Hence the reasoning why we have **HTTPS**, the *s* stands for secure because of the **SSL/TLS** protocol.

Now we know what **SSL/TLS** is how can we solve this level? Similar to the previous level, we just need to initiate a **SSL/TLS** connection to **port 30001** on localhost. So how can we do that?

## ✔️ What Worked
To solve this level, I utilized the **openssl** library and used the **s_client** tool to initiate a **SSL/TLS** connection. Here's how I did it:
```bash
openssl s_client -connect localhost:30001
```
It then generated a server certificate verifying my connection to localhost and a session ticket:
```text
Server certificate
-----BEGIN CERTIFICATE-----
MIIFBzCCAu+gAwIBAgIUBLz7DBxA0IfojaL/WaJzE6Sbz7cwDQYJKoZIhvcNAQEL
BQAwEzERMA8GA1UEAwwIU25ha2VPaWwwHhcNMjQwNjEwMDM1OTUwWhcNMzQwNjA4
MDM1OTUwWjATMREwDwYDVQQDDAhTbmFrZU9pbDCCAiIwDQYJKoZIhvcNAQEBBQAD
ggIPADCCAgoCggIBANI+P5QXm9Bj21FIPsQqbqZRb5XmSZZJYaam7EIJ16Fxedf+
jXAv4d/FVqiEM4BuSNsNMeBMx2Gq0lAfN33h+RMTjRoMb8yBsZsC063MLfXCk4p+
09gtGP7BS6Iy5XdmfY/fPHvA3JDEScdlDDmd6Lsbdwhv93Q8M6POVO9sv4HuS4t/
jEjr+NhE+Bjr/wDbyg7GL71BP1WPZpQnRE4OzoSrt5+bZVLvODWUFwinB0fLaGRk
GmI0r5EUOUd7HpYyoIQbiNlePGfPpHRKnmdXTTEZEoxeWWAaM1VhPGqfrB/Pnca+
vAJX7iBOb3kHinmfVOScsG/YAUR94wSELeY+UlEWJaELVUntrJ5HeRDiTChiVQ++
wnnjNbepaW6shopybUF3XXfhIb4NvwLWpvoKFXVtcVjlOujF0snVvpE+MRT0wacy
tHtjZs7Ao7GYxDz6H8AdBLKJW67uQon37a4MI260ADFMS+2vEAbNSFP+f6ii5mrB
18cY64ZaF6oU8bjGK7BArDx56bRc3WFyuBIGWAFHEuB948BcshXY7baf5jjzPmgz
mq1zdRthQB31MOM2ii6vuTkheAvKfFf+llH4M9SnES4NSF2hj9NnHga9V08wfhYc
x0W6qu+S8HUdVF+V23yTvUNgz4Q+UoGs4sHSDEsIBFqNvInnpUmtNgcR2L5PAgMB
AAGjUzBRMB0GA1UdDgQWBBTPo8kfze4P9EgxNuyk7+xDGFtAYzAfBgNVHSMEGDAW
gBTPo8kfze4P9EgxNuyk7+xDGFtAYzAPBgNVHRMBAf8EBTADAQH/MA0GCSqGSIb3
DQEBCwUAA4ICAQAKHomtmcGqyiLnhziLe97Mq2+Sul5QgYVwfx/KYOXxv2T8ZmcR
Ae9XFhZT4jsAOUDK1OXx9aZgDGJHJLNEVTe9zWv1ONFfNxEBxQgP7hhmDBWdtj6d
taqEW/Jp06X+08BtnYK9NZsvDg2YRcvOHConeMjwvEL7tQK0m+GVyQfLYg6jnrhx
egH+abucTKxabFcWSE+Vk0uJYMqcbXvB4WNKz9vj4V5Hn7/DN4xIjFko+nREw6Oa
/AUFjNnO/FPjap+d68H1LdzMH3PSs+yjGid+6Zx9FCnt9qZydW13Miqg3nDnODXw
+Z682mQFjVlGPCA5ZOQbyMKY4tNazG2n8qy2famQT3+jF8Lb6a4NGbnpeWnLMkIu
jWLWIkA9MlbdNXuajiPNVyYIK9gdoBzbfaKwoOfSsLxEqlf8rio1GGcEV5Hlz5S2
txwI0xdW9MWeGWoiLbZSbRJH4TIBFFtoBG0LoEJi0C+UPwS8CDngJB4TyrZqEld3
rH87W+Et1t/Nepoc/Eoaux9PFp5VPXP+qwQGmhir/hv7OsgBhrkYuhkjxZ8+1uk7
tUWC/XM0mpLoxsq6vVl3AJaJe1ivdA9xLytsuG4iv02Juc593HXYR8yOpow0Eq2T
U5EyeuFg5RXYwAPi7ykw1PW7zAPL4MlonEVz+QXOSx6eyhimp1VZC11SCg==
-----END CERTIFICATE-----

TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - 6f ad 3b f6 b8 49 af 9b-fa 78 e2 c4 c9 e5 66 35   o.;..I...x....f5
    0010 - ce 6c 4f 79 75 75 0c 00-38 c7 5e 28 e1 8e e5 11   .lOyuu..8.^(....
    0020 - b6 24 90 97 87 0f 02 c6-8c 5b 23 01 8f ad a3 6d   .$.......[#....m
    0030 - 5b 5c ec 67 ee 32 b9 c2-2e ce 28 b3 8e 5c 2e f6   [\.g.2....(..\..
    0040 - ee 5d 29 bf 88 e4 13 2e-ee 37 25 6f d5 8d 31 92   .])......7%o..1.
    0050 - 4b d0 70 5b 8c 32 9a 4d-ba 8e 37 18 90 4b 9a 4a   K.p[.2.M..7..K.J
    0060 - ea c4 f3 09 d0 f9 c1 3a-b9 20 c6 66 2d 7a 04 af   .......:. .f-z..
    0070 - b3 6d f8 a3 12 f0 34 40-69 13 66 7b e5 04 fd 2c   .m....4@i.f{...,
    0080 - 6c 70 75 7c 61 48 76 4e-77 0d a9 58 bf 9b fe 35   lpu|aHvNw..X...5
    0090 - a3 70 d6 d5 a4 d0 9e eb-33 45 da 2e 68 c1 c7 ab   .p......3E..h...
    00a0 - bc e7 dc 3c eb d1 a1 39-d6 ee b8 d6 1e e3 70 c4   ...<...9......p.
    00b0 - 7e 4a 4e 39 ec 04 07 f2-42 23 ae 45 16 94 8f 54   ~JN9....B#.E...T
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0

```

The certificate wasn't signed by a trusted Certificate Authority (CA) however it's still safe to proceed since this is expected of a CTF environment. 

After that I pasted the password for `bandit15` into the terminal and the terminal echoed back the password for `bandit16`:
```
read R BLOCK (You can pretty much ignore this, it represents how the server deals with input)
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```



## 🧠 Key Learnings
- Learned about the **SSL/TLS** protocol and how it protects data in transit over the internet.
- Learned how to utilize the **openssl** library and specifically the **s_client** tool to initiate a **TLS** connection onto localhost. 

## 🛠️ Tools Used 
**Terminal:** Cygwin  
**Commands:** `openssl`, `s_client`
Another example of a well known and useful protocol that I never knew about but interact with on a day to day basis and I'm excited on what's next to learn.

## 🔐 Next Step
We’ve successfully grabbed the password and are ready for **Level 16**. 

➡️ [Continue to Level 16 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2016.md)
