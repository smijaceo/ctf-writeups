Nmap:
`Nmap scan report for 10.201.6.37`
`Host is up (0.13s latency).`
`Not shown: 65532 closed tcp ports (reset)`
`PORT     STATE SERVICE VERSION`
`22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)`
`| ssh-hostkey:` 
`|   2048 f3:85:ec:54:f2:01:b1:94:40:de:42:e8:21:97:20:80 (RSA)`
`|   256 77:c7:c1:ae:31:41:21:e4:93:0e:9a:dd:0b:29:e1:ff (ECDSA)`
`|_  256 07:05:43:46:9d:b2:3e:f0:4d:69:67:e4:91:d3:d3:7f (ED25519)`
`80/tcp   open  http    Apache httpd 2.4.29 ((Ubuntu))`
`|_http-title: Apache2 Ubuntu Default Page: It works`
`|_http-server-header: Apache/2.4.29 (Ubuntu)`
`8000/tcp open  http    (PHP 7.2.32-1)`
`|_http-generator: Bolt`
`|_http-title: Bolt | A hero is unleashed`
`| fingerprint-strings:` 
`|   FourOhFourRequest:` 
`|     HTTP/1.0 404 Not Found`
`|     Date: Tue, 21 Oct 2025 17:25:34 GMT`
`|     Connection: close`
`|     X-Powered-By: PHP/7.2.32-1+ubuntu18.04.1+deb.sury.org+1`
`|     Cache-Control: private, must-revalidate`
`|     Date: Tue, 21 Oct 2025 17:25:34 GMT`
`|     Content-Type: text/html; charset=UTF-8`
`|     pragma: no-cache`
`|     expires: -1`
`|     X-Debug-Token: ff3a94`
`|     <!doctype html>`
`|     <html lang="en">`
`|     <head>`
`|     <meta charset="utf-8">`
`|     <meta name="viewport" content="width=device-width, initial-scale=1.0">`
`|     <title>Bolt | A hero is unleashed</title>`
`|     <link href="https://fonts.googleapis.com/css?family=Bitter|Roboto:400,400i,700" rel="stylesheet">`
`|     <link rel="stylesheet" href="/theme/base-2018/css/bulma.css?8ca0842ebb">`
`|     <link rel="stylesheet" href="/theme/base-2018/css/theme.css?6cb66bfe9f">`
`|     <meta name="generator" content="Bolt">`
`|     </head>`
`|     <body>`
`|     href="#main-content" class="vis`
`|   GetRequest:` 
`|     HTTP/1.0 200 OK`
`|     Date: Tue, 21 Oct 2025 17:25:33 GMT`
`|     Connection: close`
`|     X-Powered-By: PHP/7.2.32-1+ubuntu18.04.1+deb.sury.org+1`
`|     Cache-Control: public, s-maxage=600`
`|     Date: Tue, 21 Oct 2025 17:25:33 GMT`
`|     Content-Type: text/html; charset=UTF-8`
`|     X-Debug-Token: 4d6e09`
`|     <!doctype html>`
`|     <html lang="en-GB">`
`|     <head>`
`|     <meta charset="utf-8">`
`|     <meta name="viewport" content="width=device-width, initial-scale=1.0">`
`|     <title>Bolt | A hero is unleashed</title>`
`|     <link href="https://fonts.googleapis.com/css?family=Bitter|Roboto:400,400i,700" rel="stylesheet">`
`|     <link rel="stylesheet" href="/theme/base-2018/css/bulma.css?8ca0842ebb">`
`|     <link rel="stylesheet" href="/theme/base-2018/css/theme.css?6cb66bfe9f">`
`|     <meta name="generator" content="Bolt">`
`|     <link rel="canonical" href="http://0.0.0.0:8000/">`
`|     </head>`
`|_    <body class="front">`
`1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :`
`SF-Port8000-TCP:V=7.95%I=7%D=10/21%Time=68F7C20E%P=aarch64-unknown-linux-g`
`SF:nu%r(GetRequest,29E1,"HTTP/1\.0\x20200\x20OK\r\nDate:\x20Tue,\x2021\x20`
`SF:Oct\x202025\x2017:25:33\x20GMT\r\nConnection:\x20close\r\nX-Powered-By:`
`SF:\x20PHP/7\.2\.32-1\+ubuntu18\.04\.1\+deb\.sury\.org\+1\r\nCache-Control`
`SF::\x20public,\x20s-maxage=600\r\nDate:\x20Tue,\x2021\x20Oct\x202025\x201`
`SF:7:25:33\x20GMT\r\nContent-Type:\x20text/html;\x20charset=UTF-8\r\nX-Deb`
`SF:ug-Token:\x204d6e09\r\n\r\n<!doctype\x20html>\n<html\x20lang=\"en-GB\">`
`SF:\n\x20\x20\x20\x20<head>\n\x20\x20\x20\x20\x20\x20\x20\x20<meta\x20char`
`SF:set=\"utf-8\">\n\x20\x20\x20\x20\x20\x20\x20\x20<meta\x20name=\"viewpor`
`SF:t\"\x20content=\"width=device-width,\x20initial-scale=1\.0\">\n\x20\x20`
`SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<title>Bolt\x20`
`SF:\|\x20A\x20hero\x20is\x20unleashed</title>\n\x20\x20\x20\x20\x20\x20\x2`
`SF:0\x20<link\x20href=\"https://fonts\.googleapis\.com/css\?family=Bitter\`
`SF:|Roboto:400,400i,700\"\x20rel=\"stylesheet\">\n\x20\x20\x20\x20\x20\x20`
`SF:\x20\x20<link\x20rel=\"stylesheet\"\x20href=\"/theme/base-2018/css/bulm`
`SF:a\.css\?8ca0842ebb\">\n\x20\x20\x20\x20\x20\x20\x20\x20<link\x20rel=\"s`
`SF:tylesheet\"\x20href=\"/theme/base-2018/css/theme\.css\?6cb66bfe9f\">\n\`
`SF:x20\x20\x20\x20\t<meta\x20name=\"generator\"\x20content=\"Bolt\">\n\x20`
`SF:\x20\x20\x20\t<link\x20rel=\"canonical\"\x20href=\"http://0\.0\.0\.0:80`
`SF:00/\">\n\x20\x20\x20\x20</head>\n\x20\x20\x20\x20<body\x20class=\"front`
`SF:\">\n\x20\x20\x20\x20\x20\x20\x20\x20<a\x20")%r(FourOhFourRequest,16C3,`
`SF:"HTTP/1\.0\x20404\x20Not\x20Found\r\nDate:\x20Tue,\x2021\x20Oct\x202025`
`SF:\x2017:25:34\x20GMT\r\nConnection:\x20close\r\nX-Powered-By:\x20PHP/7\.`
`SF:2\.32-1\+ubuntu18\.04\.1\+deb\.sury\.org\+1\r\nCache-Control:\x20privat`
`SF:e,\x20must-revalidate\r\nDate:\x20Tue,\x2021\x20Oct\x202025\x2017:25:34`
`SF:\x20GMT\r\nContent-Type:\x20text/html;\x20charset=UTF-8\r\npragma:\x20n`
`SF:o-cache\r\nexpires:\x20-1\r\nX-Debug-Token:\x20ff3a94\r\n\r\n<!doctype\`
`SF:x20html>\n<html\x20lang=\"en\">\n\x20\x20\x20\x20<head>\n\x20\x20\x20\x`
`SF:20\x20\x20\x20\x20<meta\x20charset=\"utf-8\">\n\x20\x20\x20\x20\x20\x20`
`SF:\x20\x20<meta\x20name=\"viewport\"\x20content=\"width=device-width,\x20`
`SF:initial-scale=1\.0\">\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20`
`SF:\x20\x20\x20\x20<title>Bolt\x20\|\x20A\x20hero\x20is\x20unleashed</titl`
`SF:e>\n\x20\x20\x20\x20\x20\x20\x20\x20<link\x20href=\"https://fonts\.goog`
`SF:leapis\.com/css\?family=Bitter\|Roboto:400,400i,700\"\x20rel=\"styleshe`
`SF:et\">\n\x20\x20\x20\x20\x20\x20\x20\x20<link\x20rel=\"stylesheet\"\x20h`
`SF:ref=\"/theme/base-2018/css/bulma\.css\?8ca0842ebb\">\n\x20\x20\x20\x20\`
`SF:x20\x20\x20\x20<link\x20rel=\"stylesheet\"\x20href=\"/theme/base-2018/c`
`SF:ss/theme\.css\?6cb66bfe9f\">\n\x20\x20\x20\x20\t<meta\x20name=\"generat`
`SF:or\"\x20content=\"Bolt\">\n\x20\x20\x20\x20</head>\n\x20\x20\x20\x20<bo`
`SF:dy>\n\x20\x20\x20\x20\x20\x20\x20\x20<a\x20href=\"#main-content\"\x20cl`
`SF:ass=\"vis");`
`Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel`

`Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .`
`Nmap done: 1 IP address (1 host up) scanned in 96.60 seconds`


We see Bolt being hosted on port 8000.

We find a password:
![[Pasted image 20251021123924.png]]

We find a user:
![[Pasted image 20251021123941.png]]

Go to CMS login screen
http://10.201.6.37:8000/bolt/login

Shows us that it is version 3.7.1
![[Pasted image 20251021125847.png]]

This version is vulnerable to a authenticated RCE:
use msfconsole to find "use exploit/unix/webapp/bolt_authenticated_rce"

Set all options and set target to type 1

![[Pasted image 20251021130009.png]]

After some basic file traversal we find flag.txt
![[Pasted image 20251021130029.png]]

Quick writeup! Thanks for stopping by!