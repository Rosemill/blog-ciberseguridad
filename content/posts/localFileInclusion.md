---
title: "Local File Inclusion (LFI)"
date: 2021-12-13T18:13:08+01:00
draft: false
---

## Definición

Se trata de la vulnerabilidad que afecta a muchos servidores web que permite accedera archivos que no quieren que sean expuestos.

## Peligros

Fácil acceso a archivos confidenciales, el más común /etc/passwd

## LFI, ¿A qué se debe?

Para poder prácticar y entender mejor esta vulnerabilidad recomiendo usar la máquina bts_lab que cuenta con múltiples vulnerabilidades para aprender pentesting web, es fácil de instalar en kali linux o una máquina de ubuntu. Una vez instalado comprobaremos si el sitio es vulnerable a este ataque añadiendo cararcteres aleatorios después del enlace de ejemplo: http://localhost/index.php?file='nombreAleatorio'. Si no sale un nada o algún warning es probable que sea vulnerable a RFI o LFI.

Una vez comprobado escribimos la url de esta forma http://localhost/index.php?file=../../../../../../../../../etc/passwd. Al añadir dos puntos retrocedemos en el directorio del servidor, se añaden varios para asegurar que se llega al directiorio raiz y una vez hay se accede al archivo passwd que contiene todas las contraseñas de los usuarios del servidor.

Esto se debe a que el archivo contiene código susceptible a ser cambiado:
```
    <?php
        include $GET['página'];
    ?>
```
El código correcto que no permite el cambio en el nombre de la página sería el siguiente:

```
    <?php
        include ('página.php');
    ?>
```


