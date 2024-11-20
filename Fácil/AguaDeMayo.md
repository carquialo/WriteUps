DESPLIEGUE

```
bash auto_deploy.sh aguademayo.tar
```

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

`-p-` ⮞ aplicar reconocimiento a todos los puertos  
`--open` ⮞ solo a los que estén abiertos  
`--min-rate 5000` ⮞ para enviar paquetes más rápido  
`-sS` ⮞ para descubrir puertos de manera silenciosa y rápida  
`-vvv` ⮞ conforme descubre un puerto nos lo muestra por pantalla  
`-n` ⮞ no aplica la resolución DNS (tarda mucho en el caso de que no pongamos dicho parámetro)  
`-Pn` ⮞ ignora si esta activa o no la IP  
`-oG` ⮞ exportamos el resultado en formato grepeable (para extraer mejor los datos con herramientas como grep, awk)


![[Pasted image 20240918085614.png]]

Vamos a introducir esta ip por la web.

![[Pasted image 20240918085738.png]]

Nos encontramos con un servidor apache2.

Intentamos buscar con gobuster algún tipo de directorios: 


```
gobuster dir -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
```

![[Pasted image 20240918090106.png]]

Ahí lo tenemos : `/images`
Entramos. 
![[Pasted image 20240918090209.png]]

Nos descargamos ese .jpg.


![[Pasted image 20240918090248.png]]

Nos bajamos esa imagen y vamos aplicar esteneografía. 

Si nos vamos al código de la web al final del todo está este chorizo de caracteres, vamos a ver 

![[Pasted image 20240918091444.png]]


Lo metemos en un descodificador: https://www.dcode.fr/brainfuck-language


![[Pasted image 20240918092109.png]]

Y nos dice `bebeaguaqueessano`.

Tenemos `agua` que es el usuario y `bebeaguaqueessano` que es la contraseña. 


```
ssh agua@172.17.0.2
```


Nos da el siguiente fallo:

![[Pasted image 20240918092446.png]]


```
ssh-keygen -R 172.17.0.2
```

Metemos otra vez y ...

![[Pasted image 20240918092623.png]]

Ya estaríamos adentro. 

Si hacemos un `sudo -l` vemos lo siguiente:

![[Pasted image 20240918092832.png]]

