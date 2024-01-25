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

Una vez instalada, desplegaremos la aplicación sobre el puerto 80 de nuestra máquina anfitriona para comprobar que funciona:

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

Para ello, realizaremos un "docker inspect" sobre cada uno de los contenedores y redireccionaremos la salida a un fichero de texto para que nos sea más fácil localizar la dirección IP de cada uno de ellos.

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

Ahora que conocemos las direcciones IP de ambos contenedores, ejecutaremos el comando "ping" desde uno de ellos. En nuestro caso, lo vamos a hacer de Kali Linux a DVWA.

- Abrimos la ventana que teníamos con la shell interactiva en Kali Linux.

- Realizamos un "ping" a la máquina DVWA.

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/db4e80231ab1fc4a86b4ce6f510392318c2229df/Pr%C3%A1cticas/img/img34.png"/>
</p>

# Tunelizar el tráfico de Kali Linux a través de BurpSuite

Como el objetivo de este proyecto es que nuestra máquina capte toda la comunicación que haya entre la máquina Kali y la DVWA, vamos a instalar BurpSuite en nuestra máquina anfitriona para utilizarla de proxy.

Una vez lo hayamos instalado, nos iremos a nuestro Docker Desktop y nos dirigiremos al siguiente sitio:

Configuración --> Resources --> Proxies

En este apartado, configuraremos el proxy de Burp Suite para que todo el tráfico pase por él:

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/bcb606717b85a3726be5ee021be34bf4bcc28138/Pr%C3%A1cticas/img/img35.png"/>
</p>

Nota: Es importante que pulsemos en "Apply & Restart" para aplicar los cambios.

A continuación, instalaremos el certificado de BurpSuite en Kali para las peticiones HTTPS, ya que sino, cuando tratemos con webs que usen dicho protocolo, saldrá que estamos usando un certificado inseguro.

Para ello, tendremos que irnos a BurpSuite y seguir los siguientes pasos:

- En el panel principal, nos vamos a "Settings".

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/bcb606717b85a3726be5ee021be34bf4bcc28138/Pr%C3%A1cticas/img/img36.png"/>
</p>

- En la siguiente ventana que nos sale, le daremos a "Import/export CA certificate".

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/bcb606717b85a3726be5ee021be34bf4bcc28138/Pr%C3%A1cticas/img/img37.png"/>
</p>

- Ahora le daremos a la opción "Export certificate in DER format".

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/bcb606717b85a3726be5ee021be34bf4bcc28138/Pr%C3%A1cticas/img/img38.png"/>
</p>

- A continuación, le daremos a "Select file" y le pondremos un nombre personalizado al certificado que vamos a exportar.

<p align="center">
<img src="https://github.com/AntonioPC94/PPS-23-24/blob/bcb606717b85a3726be5ee021be34bf4bcc28138/Pr%C3%A1cticas/img/img39.png" alt="img28" alt="Descripción imagen 1" width="35%"/> <img src="https://github.com/AntonioPC94/PPS-23-24/blob/bcb606717b85a3726be5ee021be34bf4bcc28138/Pr%C3%A1cticas/img/img40.png" alt="img29" width="20%"/>
</p>

-  Una vez exportados, nos iremos al directorio donde lo hayamos guardado para ver que este se ha creado correctamente.

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/bcb606717b85a3726be5ee021be34bf4bcc28138/Pr%C3%A1cticas/img/img41.png"/>
</p>

- Ahora la idea es moverlo al contenedor de Kali, para hacerlo podemos hacer uso del propio Docker Desktop. Para ello, nos iremos al apartado "Containers", buscaremos el contenedor de Kali, y por último, le daremos al apartado "Files" para poder ver el sistema de archivos de dicho sistema.

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/794c3f52abab06273bf11cc48642a0bf014f4a03/Pr%C3%A1cticas/img/img42.png"/>
</p>

- A continuación, arrastraremos el certificado a la carpeta "root" del sistema Kali.

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/794c3f52abab06273bf11cc48642a0bf014f4a03/Pr%C3%A1cticas/img/img43.png"/>
</p>

- Ahora nos iremos a la sesión interactiva de Kali y entraremos dentro de la carpeta "root". Una vez dentro, convertiremos el certifcado ".der" en una clave pública, para ello haremos uso de "openssl":

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/794c3f52abab06273bf11cc48642a0bf014f4a03/Pr%C3%A1cticas/img/img44.png"/>
</p>

- Bien, ahora que tenemos la clave pública, la moveremos al directorio "/usr/local/share/ca-certificates/.

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/794c3f52abab06273bf11cc48642a0bf014f4a03/Pr%C3%A1cticas/img/img45.png"/>
</p>

- Por último, actualizaremos los certificados con el siguiente comando.

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/794c3f52abab06273bf11cc48642a0bf014f4a03/Pr%C3%A1cticas/img/img46.png"/>
</p>

Como se observa en la imagen anterior, un nuevo certificado ha sido añadido de manera exitosa.

# Captura de peticiones con BurpSuite

Ahora nos iremos a BurpSuite, concretamente al apartado "Proxy" y "HTTP History" y realizaremos dos peticiones distintas desde la sesión interactiva que tenemos abierta de Kali.

<p align="left">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/794c3f52abab06273bf11cc48642a0bf014f4a03/Pr%C3%A1cticas/img/img47.png"/>
</p>


## Petición HTTP



## Petición HTTPS



