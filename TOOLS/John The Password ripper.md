
#### Unshadowing (linux) NT (win)

John can be very particular about the formats it needs data in to be able to work with it, for this reason- in order to crack /etc/shadow passwords, you must combine it with the /etc/passwd file in order for John to understand the data it's being given. To do this, we use a tool built into the John suite of tools called unshadow. The basic syntax of unshadow is as follows:

`unshadow [path to passwd] [path to shadow]`

`unshadow` - Invokes the unshadow tool  

`[path to passwd]` - The file that contains the copy of the /etc/passwd file you've taken from the target machine  

`[path to shadow]` - The file that contains the copy of the /etc/shadow file you've taken from the target machine

**Example Usage:**

unshadow local_passwd local_shadow > unshadowed.txt

**Note on the files**

When using unshadow, you can either use the entire /etc/passwd and /etc/shadow file- if you have them available, or you can use the relevant line from each, for example:

**FILE 1 - local_passwd  
**

Contains the /etc/passwd line for the root user:

root:x:0:0::/root:/bin/bash

**FILE 2 - local_shadow**

Contains the /etc/shadow line for the root user:  

root:$6$2nwjN454g.dv4HN/$m9Z/r2xVfweYVkrr.v5Ft8Ws3/YYksfNwq96UL1FX0OJjY1L6l.DS3KEVsZ9rOVLB/ldTeEL/OIhJZ4GMFMGA0:18576::::::

####   

#### Cracking

We're then able to feed the output from unshadow, in our example use case called "unshadowed.txt" directly into John. We should not need to specify a mode here as we have made the input specifically for John, however in some cases you will need to specify the format as we have done previously using: `--format=sha512crypt`

`john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt`





# Windows 
Or for windows just use --format=NT 




# Single Pass

Single pass cracking is when you know or assume part of the password, it can also use gecos (user data in the : )

#### Word Mangling  

The best way to show what Single Crack mode is,  and what word mangling is, is to actually go through an example:

If we take the username: Markus

Some possible passwords could be:

- Markus1, Markus2, Markus3 (etc.)
- MArkus, MARkus, MARKus (etc.)
- Markus!, Markus$, Markus* (etc.)

This technique is called word mangling. John is building it's own dictionary based on the information that it has been fed and uses a set of rules called "mangling rules" which define how it can mutate the word it started with to generate a wordlist based off of relevant factors for the target you're trying to crack. This is exploiting how poor passwords can be based off of information about the username, or the service they're logging into.  

####   

#### GECOS

John's implementation of word mangling also features compatibility with the Gecos fields of the UNIX operating system, and other UNIX-like operating systems such as Linux. So what are Gecos? Remember in the last task where we were looking at the entries of both /etc/shadow and /etc/passwd? Well if you look closely You can see that each field is seperated by a colon ":". Each one of the fields that these records are split into are called Gecos fields. John can take information stored in those records, such as full name and home directory name to add in to the wordlist it generates when cracking /etc/shadow hashes with single crack mode.

  

#### Using Single Crack Mode

To use single crack mode, we use roughly the same syntax that we've used to so far, for example if we wanted to crack the password of the user named "Mike", using single mode, we'd use:  

`john --single --format=[format] [path to file]`

`--single` - This flag lets john know you want to use the single hash cracking mode.

**Example Usage:**

john --single --format=raw-sha256 hashes.txt

**A Note on File Formats in Single Crack Mode:**

If you're cracking hashes in single crack mode, you need to change the file format that you're feeding john for it to understand what data to create a wordlist from. You do this by prepending the hash with the username that the hash belongs to, so according to the above example- we would change the file hashes.txt

**From:**  

1efee03cdcb96d90ad48ccc7b8666033

**To**

mike:1efee03cdcb96d90ad48ccc7b8666033

### Custom Rules

#### Common Custom Rules
- Capital letter
- Number
- Symbol
- [1..10]
- [a-z]
- [A-Z]
checkout the documentation: https://www.openwall.com/john/doc/RULES.shtml

We then need to define what characters should be appended, prepended or otherwise included, we do this by adding character sets in square brackets `[ ]` in the order they should be used. These directly follow the modifier patterns inside of double quotes `" "`. Here are some common examples:


```
--rules=<custom-flag> 

```



### ZIP2JOHN / RAR2JOHN
password crack zip files

first
```
`zip2john [options] [zip file] > [output file]`

#example
zip2john my_secure_zip_file.zip > hashed_password.txt
```

than 
```
john --wordlist=<wl> hashed_password.txt
```



#### SSH2John

Who could have guessed it, another conversion tool? Well, that's what working with John is all about. As the name suggests ssh2john converts the id_rsa private key that you use to login to the SSH session into hash format that john can work with. Jokes aside, it's another beautiful example of John's versatility. The syntax is about what you'd expect. Note that if you don't have ssh2john installed, you can use ssh2john.py, which is located in the /opt/john/ssh2john.py. If you're doing this, replace the `ssh2john` command with `python3 /opt/ssh2john.py` or on Kali, `python /usr/share/john/ssh2john.py`.

`ssh2john [id_rsa private key file] > [output file]`