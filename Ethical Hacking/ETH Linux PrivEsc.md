# Linux Privilege Escalation

`ssh user@10.10.168.144 -p 22`

Password is **password321**

Upon running the `id` command.

```ad-success
uid=1000(user) gid=1000(user) groups=1000(user),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev)
```

---

## Service Exploits

MySQL service is running as root and the root user does not have a password assigned for that service. 

We can use popular exploit for User Defined Functions [here](https://www.exploit-db.com/exploits/1518).


