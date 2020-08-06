## Linux Privilege Escalation Environmental Variable

PATH is an environmental variable in Linux and Unix-like operating systems which specifies all bin and sbin directories that hold all executable programs are stored. When the user run any command on the terminal, its request to the shell to search for executable files with the help of PATH Variable in response to commands executed by a user. The superuser also usually has /sbin and /usr/sbin entries for easily executing system administration commands. 

It is very simple to view the Path of the relevant user with help of echo command.

echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games

If you notice ‘.’ in environment PATH variable it means that the logged user can execute binaries/scripts from the current directory and it can be an excellent technique for an attacker to escalate root privilege. This is due to lack of attention while writing program thus admin does not specify the full path to the program.

* we will create a new directory with the name as the script. Now inside the script directory, we will write a small c program to call a function of system binaries and our demo.c file we are calling ps command (Process status) which is system binaries.

![](https://github.com/pritessh/Linux-Privilege-Escalation-Environmental-variable/blob/master/images/1.png)

* After then compile the demo.c file using gcc and set SUID permission to the compiled file.


![](https://github.com/pritessh/Linux-Privilege-Escalation-Environmental-variable/blob/master/images/2.png)

## Privilege Escalation 

* First, you need to compromise the target system and then move to the privilege escalation phase. Suppose you successfully login into the victim’s machine through ssh. Then without wasting your time search for the file having SUID or 4000 permission with help of Find command. Hence with the help of following command, an attacker can enumerate any executable file, here we can also observe /home/pritesh/script/shell having suid permissions.


![](https://github.com/pritessh/Linux-Privilege-Escalation-Environmental-variable/blob/master/images/3.png)

* Then we move into /home/pritesh/script and saw an executable file “shell”. So we run this file, and here it looks like this file is trying to run ps and this is a genuine file inside /bin to get Process status.


![](https://github.com/pritessh/Linux-Privilege-Escalation-Environmental-variable/blob/master/images/4.png)

### Echo Command Technique to spawn root privilege


![](https://github.com/pritessh/Linux-Privilege-Escalation-Environmental-variable/blob/master/images/5.png)
