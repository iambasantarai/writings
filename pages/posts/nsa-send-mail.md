---
title: Configure sendmail server on CentOS
date: 2024/04/18
description: Sending email with Sendmail MTA (Mail Transfer Agent)
tag: 8th sem, lab-work, practical, Network and System Administration
author: Basanta Rai
---

# Configure sendmail server on CentOS

Sendmail is an MTA (Mail Transfer Agent) that uses SMTP protocol for sending email.

## Getting started

1. **Install sendmail**

To install Sendmail with its dependencies, use the following command :

```sh
yum install sendmail sendmail-cf m4
```

(Note: m4 is a macro processor that you need to use to compile Sendmail configuration file. )

you can also use following command to verify your installation.

```sh
rpm -qa | grep sendmail
```

> query in RPM(Red Hat Package Manager) database to list all installed packages and then filter the list to only show packages related to Sendmail

2. **Configure sendmail server**

Before directly editing /etc/mail/sendmail.mc for configuration we need to understand why this important file exists in the /etc/mail directory.

```sh
[root@adfa38dc0a7a /]# ll /etc/mail/
total 192
-rw-r--r-- 1 root root    92 Nov 27  2019 Makefile
-rw-r--r-- 1 root root   469 Nov 27  2019 access
-rw-r----- 1 root root 12288 Apr 18 14:13 access.db
-rw-r--r-- 1 root root     0 Apr 18 14:14 aliasesdb-stamp
-rw-r--r-- 1 root root   233 Nov 27  2019 domaintable
-rw-r----- 1 root root 12288 Apr 18 14:13 domaintable.db
-rw-r--r-- 1 root root  5584 Apr  1  2020 helpfile
-rw-r--r-- 1 root root    64 Nov 27  2019 local-host-names
-rw-r--r-- 1 root root   997 Nov 27  2019 mailertable
-rw-r----- 1 root root 12288 Apr 18 14:13 mailertable.db
-rwxr-xr-x 1 root root  2700 Nov 27  2019 make
-rw-r--r-- 1 root root 58498 Apr  1  2020 sendmail.cf
-rw-r--r-- 1 root root  7306 Nov 27  2019 sendmail.mc
-rw-r--r-- 1 root root 41680 Apr  1  2020 submit.cf
-rw-r--r-- 1 root root  1041 Apr  1  2020 submit.mc
-rw-r--r-- 1 root root   127 Nov 27  2019 trusted-users
-rw-r--r-- 1 root root  1847 Nov 27  2019 virtusertable
-rw-r----- 1 root root 12288 Apr 18 14:13 virtusertable.db
```

- access: used to allow or deny other systems to use Sendmail for outbound emails.
- domaintable: used for domain name mapping for Sendmail.
- local-host-names: used to define an alias for a host.
- mailertable: used to override routing for particular domains.
- virtusertable: allowing multiple virtual domains to be hosted on one machine.

Now, necessary modifications in the `sendmail.mc` file

```sh
vi /etc/mail/sendmail.mc
```

After entering the file with `vi` editor type `:set nu` to enable line numbers for god's sake.

Set your `SMTP` hostname by uncommenting `line no 26`

> To uncomment remove `dnl` at the beginning of the line

```
define(`SMART_HOST', `smtp.gmail.com')dnl
```

To update the Sendmail configuration, compile the `/etc/mail/sendmail.mc` file using the `m4` macro processor.

```sh
m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

After recompiling, restart the service

```sh
service sendmail restart
```

3. **Test sendmail**

To test sendmail, we’ll send a sample email to a gmail address.
Run the following command, replacing "youremail@gmail.com" with your actual gmail address:

```sh
echo "This mail is sent using Sendmail server."  | sendmail -v youremail@gmail.com
```

Check your gmail inbox for the email. If it arrives successfully, congratulations! You’ve successfully configured Sendmail.
