
# Forensics



# Disk Analysis 
### sleuthkit 
forensics tools 

partions
`mmls disk.flag.img`

inodes from offset bit
`fls -o 360448 disk.flag.img`

content from offset inode 
`icat -o 360448 disk.flag.img 2371`
