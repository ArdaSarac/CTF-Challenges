In this CTF I have to find secret ingredients(flags).

Methodology:
1-Connecton to the VM 
  Connected to the target VM provided by TryHackMe via SSH to perform network scanning.

2-Nmap Scan 
  Command: nmap -sS -sV -p- -A -T4 10.10.86.250
  Output:Nmap scan report for 10.10.86.250 
         Host is up (0.16s latency).
         Not shown: 998 closed tcp ports (reset) 
         PORT STATE SERVICE 22/tcp open ssh
         80/tcp open http
  The reason why I used -A and -T4 is because there is no detection risk at CTF's.I wouldn't do that in real-world.
  22/tcp:This port is commonly used for remote login.
  80/tcp: HTTP service is running. This indicates that a web server is active.

3-Accesing the Web Page:
  Using the IP address. I navigated to the web page and discovered that it was a static web page without interactive elements.So ı proceeded to inspect the source code of the web page to check for hidden information or comments that might be  useful.While reviewing the HTML, I found;
  <!--
    Note to self, remember username!
    Username: R1ckRul3s
-->
The username found might be useful in the future so I note it to my Linux machine.

4-Directory Enumeration with Dirbuster
  command: dirbuster -u http://10.10.86.250 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
  The scan produced several results, including both common assets and interesting files. Some of the most notable findings were: login.php and robots.txt
  In the login.php file I found the login page and in the robots.txt file there was a word and it was Wubbalubbadubdub so I tried this as password for R1ckRul3s and I GOT IN as www-data!!!
  After logging in there was just a Command Panel at website, I ran ls command to list files,the following files and directories listed;
  
  Sup3rS3cretPickl3Ingred.txt
  assets
  clue.txt
  denied.php
  index.html
  login.php
  portal.php
  robots.txt
  
I attempted to read the contents of all files using the cat command.However, I encountered permission errors for all files, as I was unable to read them with the cat command, and I received a "permission denied" message.So I attempted to use more and less commands to read the files in case the cat command was restricted.After several attempts I read only Sup3rS3cretPickl3Ingred.txt file and I found the first ingredient.
 
 1st ingredient:mr. meeseek hair
 


  






  
  
