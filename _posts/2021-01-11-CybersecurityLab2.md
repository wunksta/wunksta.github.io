Continuing with Metasploitable, I used the results from Zenmap to check for exploits on the next open port 22. It appears that OpenSSH version 4.7 is in use but is using protocol 2.0. 
In this case, we need to use two exploits, ssh_login and ssh_login_pubkey.  

I started Metasploit Framework and entered the command use auxiliary/scanner/ssh/ssh_login and then typed show options. I set RHOSTS to the Metasploitable VM and then set Metasplpoit Framework to use the USERPASS_FILE located in the wordlists folder titled root_userpass.txt then typed run to start the exploit.


