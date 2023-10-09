## Task
xFusionCorp Industries has planned to set up a common email server in Stork DC. After several meetings and recommendations they have decided to use postfix as their mail transfer agent and dovecot as an IMAP/POP3 server. We would like you to perform the following steps:

1. Install and configure postfix on Stork DC mail server.

2. Create an email account john@stratos.xfusioncorp.com identified by B4zNgHA7Ya.

3. Set its mail directory to /home/john/Maildir.

4. Install and configure dovecot on the same server.
## Solution
Connect to the Mail Server.

```sh
thor@jump_host ~$ ssh groot@stmail01
```

Instsall postfix and dovecot.

```sh
[groot@stmail01 ~]$ sudo yum install postfix dovecot -y
```

Open `/etc/postfix/main.cf` file.
```sh
[groot@stmail01 ~]$ sudo vi /etc/postfix/main.cf
```
Add or uncoment this lines.
```
myhostname = stmail01.stratos.xfusioncorp.com
mydomain = stratos.xfusioncorp.com
myorigin = $mydomain
inet_interfaces = all
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
relay_domains =
home_mailbox = Maildir/
```
Start postfix service.
```sh
[groot@stmail01 ~]$ sudo systemctl start postfix
```

Open `/etc/dovecot/dovecot.conf` file.

```sh
[groot@stmail01 ~]$ sudo vi /etc/dovecot/dovecot.cf
```
```
protocols = imap imaps pop3 pop3s
mail_location = maildir:~/Maildir
pop3_uidl_format = %08Xu%08Xv
login_process_size = 64
```
Start dovecot service
```sh
[groot@stmail01 ~]$ sudo systemctl start dovecot
```
## References

[Postfix HOWTO](https://wiki.centos.org/HowTos(2f)postfix.html)
