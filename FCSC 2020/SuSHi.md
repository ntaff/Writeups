# Intro - SuSHi - 1067 solves

We just have to connect in SSH at the given server with the given parameter, seems pretty easy !
(Adresse = Address ; Port = Port ; Utilisateur = User ; Mot de passe = Password)

```
Adresse : challenges2.france-cybersecurity-challenge.fr
Port : 6000
Utilisateur :	ctf
Mot de passe : ctf
```

To connect, use this command : `ssh ctf@challenges2.france-cybersecurity-challenge.fr -p 6000`, 
press enter, and then type "yes" and "ctf" (the password).
Next, just type `ls -la` to see the hidden files, and `cat .flag` to obtain the precious !

 ```
 __    __            _                 __           _     _   ___ 
/ / /\ \ \__ _ _ __ | |_      __ _    / _\_   _ ___| |__ (_) / _ \
\ \/  \/ / _` | '_ \| __|    / _` |   \ \| | | / __| '_ \| | \// /
 \  /\  / (_| | | | | |_    | (_| |   _\ \ |_| \__ \ | | | |   \/ 
  \/  \/ \__,_|_| |_|\__|    \__,_|   \__/\__,_|___/_| |_|_|   () 
ctf@SuSHi:~$ ls -la
total 24
drwxr-xr-x 1 ctf-admin ctf 4096 Apr 25 10:39 .
drwxr-xr-x 1 ctf-admin ctf 4096 Apr 25 10:38 ..
-rw-r--r-- 1 ctf-admin ctf  220 May 15  2017 .bash_logout
-rw-r--r-- 1 ctf-admin ctf 3526 May 15  2017 .bashrc
-r--r--r-- 1 ctf-admin ctf   71 Apr 25 10:38 .flag
-rw-r--r-- 1 ctf-admin ctf  675 May 15  2017 .

ctf@SuSHi:~$ cat .flag 
FCSC{ca10e42620c4e3be1b9d63eb31c9e8ffe60ea788d3f4a8ae4abeac3dccdf5b21}
 ```
