# Bandit Level 12 → Level 13
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit12.html)

## 📝 Challenge Description 
In this level, the password for `bandit13` is in the file `data.txt`, which is a **hexdump** of a file that has been repeatedly compressed. 

## 🔍 What I Initially Tried 
The level description mentions that `data.txt` is a **hexdump** of a file that has been **repeatedly compressed**. I know that file compression is used to reduce file size for storage and performance. As with previous levels, I started by opening the file:

```bash
cat data.txt
```

This revealed a long hexadecimal output. Here's a sample:
```bash
00000000: 1f8b 0808 83c9 8768 0203 6461 7461 322e  .......h..data2.
```

After researching, I found that a **hexdump** is a **hexadecimal representation of binary data**. It displays the raw content of a file byte by byte, which is useful for examining non-text files or debugging. Notably, the first bytes `1f8b` indicate the file is compressed using the **gzip** algorithm. But before decompressing, we need to reverse the hexdump.

## ✔️ What Worked

### Step 1: Create a temporary directory
`mktemp -d` creates a temporary working directory. This is helpful when you don't have write access in your current working directory.
```bash
mktemp -d
```

### Step 2: Copy the file into the temp directory
`cp` duplicates the `data.txt` file into the temp directory.
```bash
cp data.txt /tmp/tmp.ZDmWIhuS84
```

### Step 3: Reverse the hexdump using `xxd`
`xxd -r` reverses the hexdump back into its binary form.
```bash
xxd -r data.txt > new_file.gz
```

### Step 4: Decompress gzip
`gzip -d` decompresses the gzip-compressed file.
```bash
gzip -d new_file.gz
```

### Step 5: Check file type
`file` helps identify the format of the file.
```bash
file new_file
# Output: bzip2 compressed data
```

### Step 6: Decompress bzip2
`bzip2 -d` decompresses files in the bzip2 format.
```bash
bzip2 -d new_file
```

### Step 7: Check new output
```bash
file new_file.out
# Output: gzip compressed data
```

### Step 8: Rename and decompress again
To process the gzip file again, rename it with the proper extension and decompress it.
```bash
mv new_file.out new_file.gz
gzip -d new_file.gz
```

### Step 9: Unpack tar archive
The file command shows it's a tar archive, which can contain multiple files. Rename it and extract.
```bash
file new_file
# Output: POSIX tar archive (GNU)

mv new_file new_file.tar
tar -xf new_file.tar
```

### Step 10: Continue unpacking layers
New file discovered: `data5.bin`
```bash
tar -xf data5.bin
```
Then:
```bash
file data6.bin
# Output: bzip2 compressed data

mv data6.bin data6.bz2
bzip2 -d data6.bz2
```
Next:
```bash
file data6
# Output: POSIX tar archive (GNU)

tar -xf data6
```
Now, `data8.bin` appears:
```bash
file data8.bin
# Output: gzip compressed data

mv data8.bin data8.gz
gzip -d data8.gz
```
Finally:
```bash
file data8
# Output: ASCII text

cat data8
# The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

## 🧠 Key Learnings
- Learned how to decompress various formats using `xxd`, `gzip`, `bzip2`, and `tar`.
- Used a temporary directory to work safely without write permissions in the home folder.
- Understood how to identify and rename compressed files based on their content.
- Understood how file signatures like `1f8b` can tell you what compression format is being used.

## 🛠️ Tools Used 
**Terminal:** Cygwin  
**Commands:** `xxd`, `gzip`, `bzip2`, `tar`, `cat`, `mv`, `cp`, `mktemp`, `ls`, `file`

## 🔐 Next Step
We’ve successfully grabbed the password and are ready for **Level 13**. 

➡️ [Continue to Level 13 →](https://github.com/aminuzz/Bandit-CTF-Journey/blob/main/level%2013.md)
