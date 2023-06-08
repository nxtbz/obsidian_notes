
export URL=bandit.labs.overthewire.org

Warning: Permanently added '[bandit.labs.overthewire.org]:2220' (ED25519) to the list of known hosts.
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

bandit0@bandit.labs.overthewire.org's password: 

      ,----..            ,----,          .---.
     /   /   \         ,/   .`|         /. ./|
    /   .     :      ,`   .'  :     .--'.  ' ;
   .   /   ;.  \   ;    ;     /    /__./ \ : |
  .   ;   /  ` ; .'___,/    ,' .--'.  '   \' .
  ;   |  ; \ ; | |    :     | /___/ \ |    ' '
  |   :  | ; | ' ;    |.';  ; ;   \  \;      :
  .   |  ' ' ' : `----'  |  |  \   ;  `      |
  '   ;  \; /  |     '   :  ;   .   \    .\  ;
   \   \  ',  /      |   |  '    \   \   ' \ |
    ;   :    /       '   :  |     :   '  |--"
     \   \ .'        ;   |.'       \   \ ;
  www. `---` ver     '---' he       '---" ire.org


Welcome to OverTheWire!

If you find any problems, please report them to the #wargames channel on
discord or IRC.

--[ Playing the games ]--

  This machine might hold several wargames.
  If you are playing "somegame", then:

    * USERNAMES are somegame0, somegame1, ...
    * Most LEVELS are stored in /somegame/.
    * PASSWORDS for each level are stored in /etc/somegame_pass/.

  Write-access to homedirectories is disabled. It is advised to create a
  working directory with a hard-to-guess name in /tmp/.  You can use the
  command "mktemp -d" in order to generate a random and hard to guess
  directory in /tmp/.  Read-access to both /tmp/ is disabled and to /proc
  restricted so that users cannot snoop on eachother. Files and directories
  with easily guessable or short names will be periodically deleted! The /tmp
  directory is regularly wiped.
  Please play nice:

    * don't leave orphan processes running
    * don't leave exploit-files laying around
    * don't annoy other players
    * don't post passwords or spoilers
    * again, DONT POST SPOILERS!
      This includes writeups of your solution on your blog or website!

--[ Tips ]--

  This machine has a 64bit processor and many security-features enabled
  by default, although ASLR has been switched off.  The following
  compiler flags might be interesting:

    -m32                    compile for 32bit
    -fno-stack-protector    disable ProPolice
    -Wl,-z,norelro          disable relro

  In addition, the execstack tool can be used to flag the stack as
  executable on ELF binaries.

  Finally, network-access is limited for most levels by a local
  firewall.

--[ Tools ]--

 For your convenience we have installed a few useful tools which you can find
 in the following locations:

    * gef (https://github.com/hugsy/gef) in /opt/gef/
    * pwndbg (https://github.com/pwndbg/pwndbg) in /opt/pwndbg/
    * peda (https://github.com/longld/peda.git) in /opt/peda/
    * gdbinit (https://github.com/gdbinit/Gdbinit) in /opt/gdbinit/
    * pwntools (https://github.com/Gallopsled/pwntools)
    * radare2 (http://www.radare.org/)

 Both python2 and python3 are installed.

--[ More information ]--

  For more information regarding individual wargames, visit
  http://www.overthewire.org/wargames/

  For support, questions or comments, contact us on discord or IRC.

  Enjoy your stay!


# Level 0-1 
login with ssh with the given username and pwd.
`ssh bandit0@<url> -p 2220` 

password for level1 is in the readme
`cat readme`

```
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
```

##### level 1
To find the password for level 2
After login `ssh bandit1@... -p2220` we can prompt and see around with `ls`.
All we see is `-` also known as a 'dashed filename'  

##### Level 2
Filename with spaces
`cat *` aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG



##### Level 3 
Hidden files 
`ls -la` & `cat .hidden` 

##### Level 4
Only Human Readeble files

there are multiple ways to go at it, but you want to scan the map, or its contents for a file that is 'human readable', again, the files have a 'dashed' naming convention, which makes outputting it with `cat` just a little bit cumbersume. 

Let's scan for human readable files
`file -- *` or `file . -size 1033c` 

turns out `-file07` is ASCII text, so with `cat ./-file07` we will get the password.

##### Level 5
another find, but more dir's and files this time. 
`file <dir> -size <x> ! -executable -exec file {} + ` will go a little deeper and will ingore executables and such.

##### Level 6
Find entireserver, user, group, filesize  
`file / -user bandit6 -group bandit7 -size 33c` 
  
##### Level8 
The password for the next level is stored in the file **data.txt** next to the word **millionth**
`find data.txt`
`cat data.txt | grep milionth`


##### Level9
The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once

```
sort data.txt | uniq -u 
```

#### level10
The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

```
string data.txt | grep ===
```


#### level 11

The password for the next level is stored in the file **data.txt**, which contains base64 encoded data
```
man base64 
cat data.txt | base64 -d 
#or
base64 -d data.txt
```

#### level 12
The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

```
<tr> 
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
>the password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
```

#### level 13

The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

(warning, rabbit hole)

```
# first outout data Hexfile BACK (reverse) to 'a' datafile
cat data.txt | xxd -r > data

# turns out the data file is from another 'type'
file data
>data: gzip compressed data, was "data2.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unix


# rename the file to data2.gz, and unzip
mv data2.bin data2.gz
gzip -d data2.gz

# and this rabbit hole continues for 10x times

mv data3 data4.gz  
gzip -d data4.gz  

file data4  
>data4: POSIX tar archive (...

mv data4 data5.tar  
tar -xf data5.tar  
tar -xf data6.tar  
bzip2 -d data7.bz  
tar -xf data8.tar  
mv data8.bin data9.gz  
gzip -d data9.gz  

file data9  
>data9: ASCII textbandit12@bandit:/tmp/secttp$ 

cat data9  
>The password is ==**8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL**==

```




#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11
#### level 11


bandit13 wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
bandit12 JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
bandit11 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
bandit10 G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
bandit9 EN632PlfYiZbn3PhVK3XOGSlNInNE00t
bandit8 TESKZC0XvTetK0S9xNwm25STk5iWrBvP
bandit7 z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
bandit6 P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
