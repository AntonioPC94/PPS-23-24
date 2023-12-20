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

Ahora lo que vamos a hacer, es crear una nueva base de datos y un nuevo usuario para Sonarqube a través del intérprete de comandos PostgreSQL.

Para iniciar sesión en el shell de PostgreSQL, utilizaremos el siguiente comando:

`sudo -u postgres psql`

Ahora ejecutaremos las siguientes consultas para crear una nueva base de datos y un nuevo usuario para Sonarqube:

<p align="center">
  <img src=""/>
</p>

Una vez creada la base de datos y el usuario para Sonarqube, comprobaremos que estos han sido creados ejecutando las siguientes consultas:

<p align="center">
  <img src=""/>
</p>

Por último, saldremos de PostgreSQL con la consulta "\q".

# Configurar el sistema

Para instalar Sonarqube en Linux, debemos tener un usuario dedicado que vaya a ejecutar Sonarqube y algunas configuraciones adicionales como "ulimit" y los parámetros del kernel.

A continuación, crearemos un nuevo usuario para Sonarqube, y configuraremos los parámetros personalizados del kernel a través del archivo "sysctl.conf", y configuraremos "ulimit".

Para la creación del usuario, utilizaremos el siguiente comando:

`sudo useradd -b /opt/sonarqube -s /bin/bash antoniopc`

Ahora abriremos el fichero "/etc/sysctl.conf" con el editor para añadirle las siguientes líneas:

`vm.max_map_count=524288`
`fs.file-max=131072`

<p align="center">
  <img src=""/>
</p>

Sonarqube requiere que el parámetro del kernel vm.max_map_count sea mayor que "524288" y que fx.file-max sea mayor que "131072".

Para aplicar los cambios realizados en el fichero "sysctl.conf", utilizaremos el siguiente comando:

`sudo sysctl --system`

<p align="center">
  <img src=""/>
</p>

Ahora vamos a modificar el "ulimit" del sistema, los cambios que hagamos sobre este fichero, se revertirán una vez reiniciemos la máquina. Entonces, para que la configuración sea permanente, vamos a crear un archivo de configuración en "/etc/security/limits.d/" llamado "99-sonarqube.conf" utilizando el siguiente comando:

`sudo nano /etc/security/limits.d/99-sonarqube.conf`

Añadiremos la siguiente configuración al archivo y lo cerraremos:

<p align="center">
  <img src=""/>
</p>

Una vez completada la configuración, descargaremos el paquete de Sonarqube y configuraremos su instalación.

# Descarga del paquete Sonarqube

Sonarqube puede instalarse de dos maneras diferentes, mediante un archivo zip y una imagen Docker. En nuestro caso, lo vamos a instalar mediante un archivo zip que descargaremos de la página oficial de Sonarqube.

La última versión disponible de Sonarqube, es la 10.3.0.82913, la cual instalaremos en los siguientes pasos.

Antes de descargar el paquete Sonarqube, ejecutaremos el siguiente comando para instalar un paquete básico como "unzip" y "wget".

`sudo apt install unzip software-properties-common wget`

Ahora, descargaremos el paquete Sonarqube mediante el siguiente comando:

`wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.3.0.82913.zip`

Una vez descargado, veremos en nuestro directorio de trabajo, un archivo zip "sonarqube-10.3.0.82913.zip" en el cual se almacena el paquete Sonarqube.

<p align="center">
  <img src=""/>
</p>

Lo que vamos a hacer a continuación, es extraer el contenido de dicho archivo y lo vamos a mover al directorio "/opt/sonarqube".

`unzip sonarqube-10.3.0.82913.zip`

`mv sonarqube-10.3.0.82913 /opt/sonarqube`

Por último, cambiaremos la propiedad del directorio "/opt/sonarqube" al usuario "antoniopc" mediante el comando "chown" como se indica a continuación:

`sudo chown -R antoniopc:antoniopc /opt/sonarqube`

# Configurar Sonarqube





























 
