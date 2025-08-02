# Bandit Level 12 → Level 13
[Here's the link 😄](https://overthewire.org/wargames/bandit/bandit12.html)

## 📝 Challenge Description 
In this level, the password for `bandit13` is in the file `data.txt` which is a **hexdump** of a file that has been repeatedly been compressed. 







## 🔍 What I Initially Tried 
It says in the level description that the file is a **hexdump** of a file that **has been repeatedly compressed**. I know when you compress a file, it's to reduce the total size of the file for storage management, performance, etc. Like previous levels the first thing I did was open the file:


```
cat data.txt

Output:
00000000: 1f8b 0808 83c9 8768 0203 6461 7461 322e  .......h..data2.
00000110: 9425 4ea5 6f8b 443a 1354 c192 724a 41ce  .%N.o.D:.T..rJA.
00000120: 7ac2 b460 0a58 993d edf3 a684 20c1 7e19  z..`.X.=.... .~.
00000130: 19de 3818 a633 54c3 4e1b 39e6 59aa 745d  ..8..3T.N.9.Y.t]
00000140: 714b 641f 68d7 c110 2ed7 2b27 10bb 6903  qKd.h.....+'..i.
00000150: 681d 2a8f bd9f d69b c854 2ebd b4b2 57ea  h.*......T....W.
00000160: 2747 3e5c 88ea 6c87 64fe a021 97c5 1ac4  'G>\..l.d..!....
00000170: 1c82 0cc9 774a 0322 2239 940a 0fb3 b525  ....wJ.""9.....%
00000180: f110 93f3 db38 2d9c e030 4c84 f2b8 b872  .....8-..0L....r
00000190: fb49 be6a 4378 4206 5ed3 baf1 a670 bca0  .I.jCxB.^....p..
000001a0: 0bb2 d690 b4e7 f4c0 2657 db18 3ac5 077f  ........&W..:...
000001b0: 5658 13a4 2fae ff04 77fb 87d8 79de e31c  VX../...w...y...
000001c0: cf7c a692 7882 8407 c56d 1442 e1ce 068b  .|..x....m.B....
000001d0: d791 b2a3 c666 e685 2372 11f1 0b77 bf28  .....f..#r...w.(
000001e0: 3ef2 6605 4760 ac1f 11d5 780e c9f2 6066  >.f.G`....x...`f
000001f0: 4ab9 9087 0a80 0461 660b e746 dbc0 44c1  J......af..F..D.
00000200: 247e 109a e4c1 e31b ebef 3814 b9b4 69e3  $~........8...i.
00000210: acea 7dbe 8b3d 107f b304 d825 183f 2bc4  ..}..=.....%.?+.
00000220: 7c3e 58c3 30d7 e181 b973 1c50 501a 7f90  |>X.0....s.PP...
00000230: 614e c3d2 290f 3da4 acba 33aa 4ca9 2082  aN..).=...3.L. .
00000240: 5bfc 7d5a fd0f 0431 3a03 3c27 f8bb 9229  [.}Z...1:.<'...)
00000250: c284 8599 ec57 c051 a8b0 353e 0200 00    .....W.Q..5>...
```
After some research I found that a **hexdump** of a file is a **hexadecimal representation of binary data**. It shows the raw content of a file byte by byte, displaced as hexadecimal numbers. This is useful for inspecting non-text files or examining file corruption, as it reveals the underlying data structure. When looking through the hexdump, I found out that the bytes `1f8b` meant that this file was compressed using the **gzip algorithm**. But first we need to reverse the hexdump before we can start the decompression process.


## ✔️ What Worked
Before we decompress the file, I checked what permissions I had:
```bash
ls -ld
drwxr-xr-x 2 root root 4096 Jul 28 19:03 .
```
As seen here as user bandit12 I only had read and execute permissions within the home directory so I needed to make a temporary directory and work with the files in there:
```bash
mktemp -d
/tmp/tmp.PgXVBPzSYN$
```

After, I copied `data.txt` to the temporary directory (`/tmp/tmp.ZDmWIhuS84`) we just created since we do not have write permissions in the home directory for this level. 
```bash
cp data.txt /tmp/tmp.ZDmWIhuS84
```

Now after some research, I found that the `xxd` command allows us to generate and reverse a hexdump file:
```bash
xxd -r data.txt > new_file.gz
```
After we move on to the next file (`new_file.gz`) and start decompression. I knew it had to be a `.gz` file because in the beginning of the hexdump the first two bytes represented that the file had been compressed with **gzip** hence the reasoning behind the file name. Now with the `gzip` command, I decompressed the file:
```bash
gzip -d new_file.gz 
```

Now since we decompressed `new_file.gz` we're now left with just `new_file` so instead of opening the file using `cat` I decided to see what type of data was in the file using the `file` command:
```bash
file new_file
new_file: bzip2 compressed data, block size = 900k
```

Based off this output, we know this file has been compressed with the **bzip2 algorithm** so after reading through the [man page](https://linux.die.net/man/1/bzip2) this was the command I came up with:
```bash
bzip2 -d new_file
```

Since `new_file` didn't have the `.bz2` ending to it, the algorithm writes the output to the original file with the **.out** file extension to it. Now let's check what type of data is in `new_file.out`:
```bash
file new_file.out
new_file.out: gzip compressed data
```

Again we're back with a `.gz` file, but before we decompress we must rename the file to have the `.gz` extension:
```bash
mv new_file.out new_file.gz
gzip -d new_file.gz
```

Now I checked again what type of data the `new_file` contains:
```bash
file new_file
new_file: POSIX tar archive (GNU)
```

Now the file contains a `tar archive` which is a way to store multiple files into a singular file (an archive) and have the ability to manipulate the archive. This is different from compressing a file since with a **tar archive** it's just a collection of files/directories that are combined into one file. After reading the [man page](https://man7.org/linux/man-pages/man1/tar.1.html) and reanming the file to `new_file.tar` I ran this command:
```bash
tar -xf new_file.tar
```

Then I checked if any new files were created and I found `data5.bin` in the directory:
```bash
bandit12@bandit:/tmp/tmp.dPujjGvAN6$ ls
data5.bin  data.txt  new_file.tar
```

`data5.bin` was also a **tar archive** so I ran the same command as before on this file:
```bash
tar -xf data5.bin
```

I checked again if a new file was created and I found a file called `data6.bin`. I checked what type of data it contained and yet again it was a `bzip2` file. Knowing it was a `bzip2` file, I renamed it just for simiplicity sake and decompressed it:
```bash
file data6.bin
data6.bin: bzip2 compressed data, block size = 900k

mv data6.bin data6.bz2
bzip2 -d data6.bz2
```

Now we're left with a file called `data6` and after checking the contents of the file it was another **tar archive** so I had to extract the files:
```bash
file data6
data6: POSIX tar archive (GNU)

tar -xf data6
```

After listing out the files from the directory I found `data8.bin` so like usual I checked what type of data the file contained:
```bash
file data8.bin
data8.bin: gzip compressed data
```

Yet again we are dealing with a `gzip` file so I had to decompress it with the `gzip` command



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
