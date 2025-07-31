# Bandit Level 11 → Level 12
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit12.html)

## 📝 Challenge Description 
In this level, the password for `bandit12` is stored in the file called `data.txt`, where all lowercase and uppercase letters have been rotated by 13 positions.







## 🔍 What I Initially Tried 
At first, I opened `data.txt` to see the contents of the file:
```bash
cat data.txt

```
Output:
```bash

VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
```
Based off the output, I did some research on what **base64** encoded data is. I assumed it was a encryption algorithm where I have to decrypt the data in order to get the password however that wasn't the case. **Base64** simply converts binary data into human-readable text. It offers no security so anyone can decode it. So all I had to do was decode the data.



## ✔️ What Worked
After reading the [base64 man page](https://linux.die.net/man/1/base64), I had to use the `-d` flag to decode the data:
```
base64 -d data.txt
```
**What this does:**
- `base64 -d data.txt`: this decodes the base64 data that is present in `data.txt`. 
The decoded output directly revealed the password:
```
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```
And there it was the password for `bandit11`!


## 🧠 Key Learnings
- Knowing the difference between **encoding** and **encryption** is very important because base64 encoding can be confused with encrypting data. Encoding your data with **base64** can be easily reversed unlike encrypting data where you need a specific key for decryption.
- **base64** encoding is just a way to represent binary or special characters using only plain text.

## 😕 Common misconceptions
When I solved this level I was thinking to myself, why encode text into other text because by definition, it translates binary into text however you have to remember any sort of data even the text on the screen you're reading are just bunch of 1s and 0s. For example, if we were to encode the string **"hello"** how would that work? Here's how:

**Step 1**: You start with normal, readable text:
```text
hello
```

**Step 2**: Text is just characters --> which are really numbers
Each character is represented by a number using **ASCII** (or UTF-8):
| Character | ASCII |
| --------- | ----- |
| h         | 104   |
| e         | 101   |
| l         | 108   |
| l         | 108   |
| o         | 111   |

**Step 3**: Those numbers are turned into binary (1s and 0s)
For example:
```
h = 104 → 01101000  
e = 101 → 01100101  
l = 108 → 01101100  
...
```
The full string `hello` becomes a big string of bits:
```
01101000 01100101 01101100 01101100 01101111
```


**Step 4**: Base64 encodes this binary into a new "text format"
It takes chunks of 6 bits at a time and maps them to **printable characters** like `A-Z`, `a-z`, `0-9`, `+`, `/`.
This is how you something like:
```
hello → aGVsbG8=
```

## 🛠️ Tools Used 
Terminal: Cygwin.
Commands: `base64`, `cat`. 
First time hearing about **base64** and how it changes the way you see your data and it's pretty interesting in my opinion. 

## 🔐 Next Step
We’ve successfully grabbed the password and are ready for **Level 11**. 

➡️ [Continue to Level 12 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2011%20--%3E%2012.md)
