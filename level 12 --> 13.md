# Bandit Level 11 → Level 12
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit12.html)

## 📝 Challenge Description 
In this level, the password for `bandit13` is in the file `data.txt` which is a **hexdump** of a file that has been repeatedly been compressed. 







## 🔍 What I Initially Tried 
It says in the level description that the file is a hexdump of a file that **has been repeatedly compressed**. From my own experience, compressing a file is used to reduce the size of a larger file to a smaller file. :


```
H ---> U
E ---> R
L ---> Y
L ---> Y
O ---> B

```
The challenge was figuring out how to decrypt this cipher to get the password for the next level. While reviewing the recommended commands for this level, the `tr` command stood out. `tr` is short for translate—it translates text based on the input and output character sets you define. The syntax looks like this:

```bash
tr SET1 SET2
```
One thing to keep in mind is that `tr` requires input via a pipe; it doesn’t work as a standalone command.



## ✔️ What Worked
After some trial and error, this was the command I used:
```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
**What this does:**
- `cat data.txt`: Outputs the contents of `data.txt`.
- `| tr 'A-Za-z' 'N-ZA-Mn-za-m'`: Pipes the output into the `tr` command, which performs a ROT13 transformation.
As a result of this command, I obtained the password for `bandit12`.:
```
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```



## 🧠 Key Learnings
- Learning how to use the `tr` command to decipher the **ROT13** algorithm and how to use it in conjuction with other commands.
- Understood the importance of character set mapping and using pipes to feed input into commands.

## 😕 Common misconceptions
While reading the `tr` command syntax, I was initially confused about which sets of letters to use and how to translate them. After some thinking, I realized that since the cipher rotates each character by 13 positions, I had to split the set of characters into two: one for the rotated characters from A-N and another for the rest. I also made sure to include both uppercase and lowercase characters in the correct order.

## 🛠️ Tools Used 
Terminal: Cygwin

Commands: `tr`, `cat`
 

## 🔐 Next Step
We’ve successfully grabbed the password and are ready for **Level 12**. 

➡️ [Continue to Level 12 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2012%20--%3E%2013.md)
