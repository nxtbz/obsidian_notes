
# Forensics

# Basic search 

File
`find . flag.txt`
Text
`grep -Ri 'flag{' . `



# Disk Analysis 
### sleuthkit 

partions
`mmls disk.flag.img`

inodes from offset bit
`fls -o 360448 disk.flag.img`

content from offset inode 
`icat -o 360448 disk.flag.img 2371`

search (find) recursively 'down-the-bottom.txt' file over disk
`fls -r -o 2048 dds2-alpine.flag.img | grep 'down-at-the-bottom.txt'` 

search (find) strings with 'pico' over disk
`srch_strings -o 411648 disk.flag.img | grep 'pico'`

