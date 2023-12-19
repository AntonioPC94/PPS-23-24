# Instalación y configuración de Sonarqube

<p align="center">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/916d98cd1fd54515996150b73ece4ca245cae9dd/Pr%C3%A1cticas/img/Sonarqube.png"/>
</p>

Trabajo realizado por: Antonio Peñalver Caro

#

# Instalar Java OpenJDK

Lo primero que haremos, será instalar OpenJDK v11, ya que SonarQube lo requiere. Pero antes que nada, actualizaremos los repositorios de la máquina con el siguiente comando:

`sudo apt update`

A continuación, instalaremos Java OpenJDK v11 mediante el siguiente comando:

`sudo apt install default-jdk`

Nota: Con la opción "default-jdk", nos instalará la versión que queremos.

Una vez instalado, comprobaremos la versión de Java utilizando el siguiente comando:

`java -version`

<p align="center">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/81f62576fd4b7e2dfc5c8ce1df802f8430355953/Pr%C3%A1cticas/img/img01.png"/>
</p>

# Instalación de PostgreSQL

SonarQube admite varios sistemas de bases de datos, como PostgreSQL, Microsoft SQL Server y la base de datos Oracle. Aunque en nuestro caso, instalaremos PostgreSQL, concretamente su versión 13.

Lo primero que vamos a hacer, es utilizar el siguiente comando para añadir al sistema la clave GPG de PostgreSQL:

`wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -`

Para ver que la clave ha sido añadida con éxito, usaremos el siguiente comando:

`apt-key list`

<p align="center">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/81f62576fd4b7e2dfc5c8ce1df802f8430355953/Pr%C3%A1cticas/img/img02.png"/>
</p>

Una vez tengamos la clave, añadiremos el repositorio de PostgreSQL a nuestro sistema utilizando el siguiente comando:

`sudo sh -c "echo 'deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main' > /etc/apt/sources.list.d/pgdg.list"`

Ahora que tenemos el repositorio de PostgreSQL, actualizaremos de nuevo los repositorios del sistema:

<p align="center">
  <img src="https://github.com/AntonioPC94/PPS-23-24/blob/81f62576fd4b7e2dfc5c8ce1df802f8430355953/Pr%C3%A1cticas/img/img03.png"/>
</p>

Ahora, instalaremos la base de datos PostgreSQL v13 mediante el siguiente comando:

`sudo apt install postgresql-13`

Una vez instalado, ejecutaremos el siguiente comando para verificar el servicio y asegurarnos de que se está ejecutando:

`sudo systemctl is-enabled postgresql`
`sudo systemctl status postgresql`

<p align="center">
  <img src=""/>
</p>



 
