# Entorno Pentesting Dockerizado

<p align="center">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/405a8361ca5eac67d03db241d73d5af4005598d0/Pr%C3%A1cticas/img/Docker.png"/>
</p>

Trabajo realizado por: Antonio Peñalver Caro

#

# Instalación Kali Linux

Lo primero que haremos, será decargar la imagen oficial de Kali Linux de Docker Hub.

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/b80d66065fd392c13657a677be156089f30e4010/Pr%C3%A1cticas/img/img21.png"/>
</p>

Una vez instalada, accedemos al contenedor utilizando el siguiente comando:

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/b80d66065fd392c13657a677be156089f30e4010/Pr%C3%A1cticas/img/img22.png"/>
</p>

Ahora que estamos dentro, actualizaremos los repositorios de la máquina e instalaremos las "net-tools".

<p align="center">
<img src="https://github.com/AntonioPC94/PPS-23-24/blob/1dba84d1d1a13a71a285c53a5137932d9cacd634/Pr%C3%A1cticas/img/img23.png" alt="img28" alt="Descripción imagen 1" width="35%"/> <img src="https://github.com/AntonioPC94/PPS-23-24/blob/1dba84d1d1a13a71a285c53a5137932d9cacd634/Pr%C3%A1cticas/img/img24.png" alt="img29" width="30%"/> <img src="https://github.com/AntonioPC94/PPS-23-24/blob/1dba84d1d1a13a71a285c53a5137932d9cacd634/Pr%C3%A1cticas/img/img25.png" alt="Descripción imagen 3" width="30%"/>
</p>

# Instalación DVWA

Lo primero que haremos, será descargar la imagen oficial de DVWA de Docker Hub.

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/ae0dacfa09c706ee7f16f883ab76b16644e5f20e/Pr%C3%A1cticas/img/img26.png"/>
</p>

Una vez instalada, desplegaremos la aplicación sobre el puesto 80 de nuestra máquina anfitriona:

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/ae0dacfa09c706ee7f16f883ab76b16644e5f20e/Pr%C3%A1cticas/img/img27.png"/>
</p>

Ahora si nos vamos al navegador de nuestra máquina anfitriona y colocamos la siguiente URL, nos debería de aparecer la aplicación de DVWA desplegada:

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/4e24cdebbd22317570263fcfd69fe00bce2e1e2b/Pr%C3%A1cticas/img/img28.png"/>
</p>

# Creación y configuración de una red en Docker

Para que las dos máquinas anteriores puedan comunicarse, es conveniente que estén en la misma red. Para ello, vamos a crear una red en Docker y conectaremos ambos contenedores a ella.

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/a0ee3d97aa76e493123ce432f3149002fe8bdbfb/Pr%C3%A1cticas/img/img29.png"/>
</p>

# Comprobando la conexión

Ahora para comprobar que ambas máquinas se ven, vamos a averiguar qué dirección IP tienen cada uno de los contenedores dentro de la red que acabamos de crear.

Para ello, realizaremos un "docker inspect" sobre cada uno de los contenedores y redireccionaremos la salida a un fichero de texto para que nos sea más fácil localizar la dirección IP.

## Dirección IP Kali

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/a97ff15fa56ecb7bdac4cd034e8e38cfae4dd548/Pr%C3%A1cticas/img/img30.png"/>
</p>

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/a97ff15fa56ecb7bdac4cd034e8e38cfae4dd548/Pr%C3%A1cticas/img/img31.png"/>
</p>

## Dirección IP DVWA

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/a97ff15fa56ecb7bdac4cd034e8e38cfae4dd548/Pr%C3%A1cticas/img/img32.png"/>
</p>

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/a97ff15fa56ecb7bdac4cd034e8e38cfae4dd548/Pr%C3%A1cticas/img/img33.png"/>
</p>

## Ping entre máquinas

Ahora que conocemos las direcciones IP de ambos contenedores, para ello ejecutaremos el comando "ping" desde uno de los contenedores. En nuestro caso, lo vamos a hacer de Kali Linux a DVWA.

- Abrimos una shell interactiva en nuestro contenedor Kali Linux:

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/a97ff15fa56ecb7bdac4cd034e8e38cfae4dd548/Pr%C3%A1cticas/img/img33.png"/>
</p>

- 

