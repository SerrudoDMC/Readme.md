# PROYECTO FINAL GRUPO 8
## INTRODUCCION
###### En el presente documento estaremos viendo como se instala una distribución de Linux  y está la estaremos ejecutando en “Oracle VM VirtualBox.
###### TYPO3 es un sistema de gestión de contenidos gratuito y de código abierto escrito en PHP. Es un CMS de clase empresarial que combina el código abierto con la fiabilidad y la verdadera escalabilidad. Se ejecuta en un servidor web y es compatible con muchos sistemas operativos, como Windows, Linux, macOS, etc. Es un CMS sencillo, con capacidad de respuesta, preparado para dispositivos móviles y seguro, y puede personalizarse y ampliarse fácilmente sin necesidad de escribir ningún código. Es una opción muy popular y estupenda para poner en marcha tu sitio web rápidamente.
###### Acontinuacion, te mostraremos cómo instalar el CMS TYPO3 con el servidor web Apache y Let's Encrypt SSL en Ubuntu (LINUX MINT)

# DESARROLLO/INSTALACION
#### **Requisitos previos**
- Un servidor con Ubuntu 20.04.
- Un nombre de dominio válido apuntado con la IP de tu servidor.
- Un contraseña de root configurada el servidor.

## ¿Como Empezar?

### PASO 1
En primer lugar, se recomienda actualizar los paquetes de tu sistema con la última versión. Puedes actualizar todos los paquetes ejecutando el siguiente comando, para ello tienes que ingresar como super usuario(root):

    sudo su
    apt-get update -y

Una vez que todos los paquetes estén actualizados, puedes pasar al siguiente paso.

###  PASO 2: Instalar el servidor LAMP
A continuación, tendrás que instalar el servidor web Apache, MariaDB, PHP y otras extensiones de PHP en tu servidor. Puedes instalarlos todos con el siguiente comando:

     sudo apt-get install apache2 mariadb-server php libapache2-mod-php php-common php-gmp php-curl php-intl php-mbstring php-xmlrpc php-mysql php-gd php-xml php-cli php-zip curl git gnupg2 -y

Después de instalar todos los paquetes, edita el archivo php.ini y cambia algunos ajustes recomendados:

    sudo nano /etc/php/7.4./apache2/php.ini

Cabe recalcar que la version puede variar `/php/7.4./` dependiendo del sistema operativo.
Continuando ahora agrega las siguientes líneas:

    memory_limit = 256M
    upload_max_filesize = 100M
    post_max_size = 100M
    max_execution_time = 360
    max_input_vars = 1500
    date.timezone = Asia/Kolkata
Guarda y cierra el archivo y luego reinicia el servicio Apache para aplicar los cambios:

    systemctl restart apache2
###  PASO 3: Crear una base de datos para TYPO3
A continuación, tendrás que crear una base de datos y un usuario para TYPO3. En primer lugar, inicia sesión en el shell de MariaDB con el siguiente comando:

    sudo mysql
Una vez iniciada la sesión, crea una base de datos y un usuario con el siguiente comando:

    MariaDB [(none)]> CREATE DATABASE typo3db;
    MariaDB [(none)]> CREATE USER ''@'localhost' IDENTIFIED BY 'password';
A continuación, concede todos los privilegios a la typo3db con el siguiente comando:

    MariaDB [(none)]> GRANT ALL ON typo3db.* TO 'typo3'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;
Posteriormente, vacía los privilegios y sal de MariaDB con el siguiente comando:

    MariaDB [(none)]> FLUSH PRIVILEGES;
    MariaDB [(none)]> EXIT;
En este punto, tu base de datos MariaDB está configurada.

### PASO 4: Instalar TYPO3 CMS
En primer lugar, tendrás que descargar la última versión de TYPO3 desde su sitio web oficial. Puedes utilizar el comando curl para descargarla: 

    sudo curl -L -o typo3_src.tgz https://get.typo3.org/11.5.33
Una vez completada la descarga, extrae el archivo descargado con el siguiente comando:

    sudo tar -xvzf typo3_src.tgz
A continuación, mueve el directorio extraído al directorio raíz de la web de Apache:

    sudo mv typo3_src-11.5.33 /var/www/html/typo3
A continuación, da el permiso y la autorización adecuados con el siguiente comando:


    sudo chown -R www-data:www-data /var/www/html/typo3
    sudo chmod -R 775 /var/www/html/typo3
Una vez que hayas terminado, puedes pasar al siguiente paso.

### PASO 5: Configurar Apache para TYPO3
A continuación, crea un archivo de configuración del host virtual de Apache para alojar el CMS TYPO3. Puedes crearlo con el siguiente comando:

    sudo nano /etc/apache2/sites-available/typo3.conf
Añade las siguientes líneas:

    <VirtualHost *:80>
        ServerAdmin admin@example.com
        DocumentRoot /var/www/html/typo3
        ServerName typo3.example.com
        <Directory /var/www/html/typo3>
        Options +FollowSymlinks
        AllowOverride All
        Require all granted
        </Directory>
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
Guarda y cierra el archivo y luego habilita el archivo de configuración del host virtual y el módulo de reescritura con el siguiente comando:

    sudo a2ensite typo3.conf
    sudo a2enmod rewrite
A continuación, reinicia el servicio Apache para aplicar los cambios:

    systemctl restart apache2
En este punto, el servidor web Apache está configurado para servir a TYPO3. Ahora puedes pasar al siguiente paso.

### PASO 6: Accede a TYPO3 CMS
Ahora, abre tu navegador web y accede a TYPO3 utilizando la URL `http://typo3.example.com.` Deberías ver la siguiente página:
