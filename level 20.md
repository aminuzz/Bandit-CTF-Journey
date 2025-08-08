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
Based off the description I needed to create a TCP server on an open port that would listen for incoming connections. In that case the **setuid binary** will act as the client initiating the interaction with the server. But in this case, the **setuid binary** 

## ✔️ What Worked




## 🧠 Key Learnings



## 🔐 Next Step
Now let's move onto **level 21**. 

➡️ [Continue to Level 21 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2021.md)
