**Autor:** [Prendelo](https://dockerlabs.es)

**Dificultad:** Fácil

**Fecha de creación:** 31/05/2024

------------------------------------------

DESPLIEGUE

```
sudo bash auto_deploy.sh buscalove.tar
```


![[Pasted image 20241019134516.png]]


La IP es:

```
172.19.0.2
```


----------------------------------------------


RECONOCIMIENTO

```
nmap -p- -sS -sV -sC --min-rate 5000 -n -vvv -Pn 172.19.0.2
```


`-p-` ⮞ aplicar reconocimiento a todos los puertos  
`-sS` ⮞ para descubrir puertos de manera silenciosa y rápida
`--min-rate 5000` ⮞ para enviar paquetes más rápido  
`-n` ⮞ no aplica la resolución DNS (tarda mucho en el caso de que no pongamos dicho parámetro)  
`-vvv` ⮞ conforme descubre un puerto nos lo muestra por pantalla  
`-Pn` ⮞ ignora si esta activa o no la IP  


![[Pasted image 20241019135003.png]]

Esa máquina vulnerable tiene dos puertos abiertos: 22 que es el puerto de ssh y el puerto 80 de http. 

Echamos un vistazo en la web.

![[Pasted image 20241019135233.png]]

Lo que podemos hacer es usar gobuster por si hay algún directorio. 



``` 
gobuster dir -u http://172.19.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
```

![[Pasted image 20241019135837.png]]

Tenemos una de wordpress. Entramos. 

![[Pasted image 20241019140513.png]]

Vemos algo extraño cuando miramos en los enlaces :

![[Pasted image 20241019140659.png]]


Intentaremos probar si existe un Local File Inclusion (LFI) y lo haremos con `wfuzz`

```
wfuzz -c --hc=404 -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt http://172.19.0.2/FUZZ
```



==NO está terminada==

