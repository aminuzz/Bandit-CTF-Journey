# Bandit Level 20 → 21
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit21.html)
## 📝 **Challenge Description**  
In this level, there is a **setuid binary** that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password of `bandit20` and if they match, it will transmit the password for the next level.



## 🔍 **What I Initially Tried**  
Based off the level description, I was assuming that I needed to create some sort of **client-server** interaction in order to get the password for the next level. 

Before I attempted setting up the server, I decided to look into what the **setuid binary** does:
```bash
ls
suconnect
./suconnect
# Output: Usage: ./suconnect <portnumber>
This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.
```
Based on the description I needed to create a TCP server on an open port that would listen for incoming connections. In that case the **setuid binary** will act as the client initiating the interaction with the **TCP server**. The **setuid binary** has permissions as `bandit21` so it reads the password (stored in **/etc/bandit_pass/bandit21**) and sends it over a **TCP** connection back to us if the correct input is provided. 

## ✔️ What Worked
On a separate terminal using the `nc` command, I created a **TCP** server on port `8080` that the **setuid** binary can connect to. From there I pasted the password for `bandit20` and received the password for `bandit21`:
```bash
nc -l 8080
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

On the other terminal this was the output:
```bash
./suconnect 8080
Read: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
Password matches, sending next password
```

So why have two terminals instead of running everything all in one:
- This comes down to the fact that the **setuid binary** is waiting for a response from the server side in order for it to perform a verification test to see if the input provided matches the expected input. So having two terminals, one for the **client (being the setuid binary)** and one for the **TCP server** is necessary for this process. 

## 🧠 Key Learnings
- Learned how to set up a simple **TCP** server using the `nc` command.
- Learned how to utilize a **setuid binary** to initiate a connection to a **TCP** server.
- Reinforced the concept of client (initiates connection) vs server (listens for connection).
- Practiced sending/receiving data over raw TCP manually.


## 🔐 Next Step
Now let's move onto **level 21**. 

➡️ [Continue to Level 21 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2021.md)
