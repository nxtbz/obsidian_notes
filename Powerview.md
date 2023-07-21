  

Powerview is a powerful powershell script from powershell empire that can be used for enumerating a domain after you have already gained a shell in the system.


1.) Start Powershell - `powershell -ep bypass` -ep bypasses the execution policy of powershell allowing you to easily run scripts

![](https://i.imgur.com/kVdteyd.png)  

2.) Start PowerView - `. .\Downloads\PowerView.ps1`
( mind the EXTRA DOT before executing the command)

3.) Enumerate the domain users - `Get-NetUser | select cn`    

![](https://i.imgur.com/jXfVlgK.png)


4.) Enumerate the domain groups - `Get-NetGroup -GroupName *admin*`    

![](https://i.imgur.com/37PiQa9.png)  

Now enumerate the domain further on your own

Here's a cheatsheet to help you with commands: [https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993](https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993)

Cheatsheet Credit: HarmJ0y
