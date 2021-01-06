First, I will need to create a lab in order to start testing network and operating system security. To do this, I have installed Kali Linux and Metasploitable into Virtualbox. 

After getting these set up I ran Zenmap to check for open ports on Metasploitable. Many were found but I focused on the first one, the FTP service on port 21. Zenmap showed that this was running version vsftpd 2.3.4. I searched online and Rapid7 showed that an exploit existed for this version called VSFTPD v2.3.4 Backdoor Command Execution. 

I started the Metasploit Framework and ran the command 'use exploit/unixx/ftp/vsftpd_234_backdoor. I set the target to 0 and RHOST to the IP of the Metasploitable VM and ran the exploit. I was able to the get a shell on the Metaploitable VM. I ran commands such as ifconfig, whoami and uname -r to confirm. 

The VSFTPD website was compromised back in 2011 and the attacker uploaded a malicious version of VSFTPD which contained a backdoor that listens on TCP port 6200. The code implanted into the source code was

            else if((p_str->p_buf[i]==0x3a)
            && (p_str->p_buf[i+1]==0x29))
            {
              vsf_sysutil_extra();
             }
             
This allows an attacker to send certain bytes into the network buffer and if they match 0x3a) and 0x29, then the vsf_sysutil_extra function is triggered. 

