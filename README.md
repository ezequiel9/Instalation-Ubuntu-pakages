# Instalation-Ubuntu-pakages
Paquetes basicos necesarios para programar en ubuntu


Para evitar posibles problemas si hubiera algún error, es recomendable hacer una copia del archivo /etc/apt/sources.list. Para guardar una copia de seguridad mediante la terminal, ejecutamos el siguiente comando:

    $ sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup



Editamos el archivo encargado de administrar los repositorios con cualquier editor de textos, por ejemplo Gedit:

    $ sudo gedit /etc/apt/sources.list



Después de hacer esto cambiaremos nuestra sources.list suprimiendo las almohadillas (#) en cada línea donde aparece universe o multiverse.

De esa manera ya tendremos todos los repositorios activados, ahora y siempre que cambiemos la sources.list (es imprescindible) ejecutaremos el siguiente comando:

    $ sudo aptitude update
    $ sudo aptitude upgrade



Paso II


Vamos con MySQL

    sudo aptitude install mysql-server-5.0 mysql-client mysql administrator mysql-query-browser 



    sudo apt-get install mysql-server



Casi al final del proceso te va a pedir que ingreses una contraseña (ej: mysql)

Y en aplicaciones >programacion ya tendras las dos herramientas instaladas para trabajar con base de datos 


Paso III


Luego vamos con Apache y PHP5

    $ sudo apt-get install apache2
    $ sudo apt-get install php5



Paso IV


luego instalamos los archivos necesarios para q MySQL soporte php5 y apache2

    $ sudo apt-get install libapache2-mod-auth-mysql
    $ sudo apt-get install php5-mysql



y luego reiniciamos el servicio de apache y mysql

    $ sudo /etc/init.d/apache2 restart
    $ sudo service mysql restart
    
    
    
Con esto debería estar lo básico.


Agrego paquetes extras

Instalo phpmyadmin

    $ sudo apt-get install phpmyadmin

Instalo sublime

    $ sudo add-apt-repository ppa:webupd8team/sublime-text-3
    $ sudo apt-get update
    $ sudo apt-get install sublime-text-installer

Luego de instalar sublime tenemos que descargar pugins como xdebug para sacarle el jugo a este fantastico editor.





Es necesario hacernos propietarios de nuestra carpeta base
    
    $ cd /var/www/
    $  sudo chown -R usuario .



/*==============================================00
Listo, ahora creemos los virtualhost para diferentes entornos
=================================================*/


Crear la Estructura del Directorio
    
    $ sudo mkdir -p /var/www/ejemplo.com/public_html
    $ sudo mkdir -p /var/www/pruebas.com/public_html

Otorgar Permisos
  
    $ sudo chown -R $USER:$USER /var/www/ejemplo.com/public_html
    $ sudo chown -R $USER:$USER /var/www/pruebas.com/public_html

La variable $USER tomará el valor del usuario con el cual actualmente estás identificado. Al hacer esto, nuestro usuario regular ahora es propietario de los directorios public_html donde se almacenará nuestro contenido.

Debemos además modificar los permisos un poco para asegurarnos que el permiso de lectura pueda ser aplicado a archivos y directorios para que las páginas puedan ser desplegadas correctamente:

    $ sudo chmod -R 777 /var/www
    
Ahora creemos una pagina de prueba por cada entorno
    
    <html>
      <head>
        <title>Bienvenido a Ejemplo.com!</title>
      </head>
      <body>
        <h1>Éxito! El Virtual Host ejemplo.com esta funcionando!</h1>
      </body>
    </html>
    
despues de crearlo en el primero podemos copiarlo para el segundo y ahorrar unos minutos

cp /var/www/comunidad/public_html/index.html /var/www/shop/public_html/index.html

modificar algo para que sea distinto con nano o sublime





Crear Nuevos Archivos Virtual Host


Los archivos Virtual Host son archivos que contienen información y configuración específica para el dominio y que le indican al servidor Apache como responden a las peticiones de varios dominios.

Apache incluye un archivo Virtual Host por defecto denominado 000-default.conf que podemos usar para saltarnos al punto. Realizaremos una copia para trabajar sobre ella y crear nuestro Virtual Host para cada dominio.

Iniciaremos con un dominio, configuralo, copialo para el segundo dominio, y después realiza los ajustes necesarios. La configuración por defecto de Ubuntu requiere que cada archivo de configuración de Virtual Host termine en .conf.


Crear el Archivo Virtual Host

    $ sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/comunidad.conf

Abre el nuevo archivo con tu editor como usuario root:

    $ sudo nano /etc/apache2/sites-available/comunidad.conf
                
editarlo para que quede algo aśi

    <VirtualHost *:80>
        ServerAdmin admin@ejemplo.com
        ServerName ejemplo.com
        ServerAlias www.ejemplo.com
        DocumentRoot /var/www/ejemplo.com/public_html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
                
Hacer lo mismo con el otro del otro entorno.






Habilita los nuevos Archivos Virtual Host
    
    $ sudo a2ensite comunidad.conf
    $ sudo a2ensite shop.conf
    
    $ sudo service apache2 restart




Configura Archivos Locales (Opcional)

Si aún no estás utilizando nombres de dominio de tu propiedad para este procedimiento y utilizaste dominios ejemplo en su lugar, puedes al menos hacer pruebas de funcionalidad de este proceso modificando temporalmente el archivo hosts de tu computadora local.



    $ sudo nano /etc/hosts
        
    127.0.0.1   localhost
    127.0.1.1   guest-desktop
    127.0.0.1   comunidad.com
    127.0.0.1   shop.com    
                
     
     
LISTO YA ESTÁ VHOST CONFIGURADO.



/*====================================0
instalar git
=======================================*/
    
    $ sudo apt-get install git
           
  Configurar    
           
    $ git config --global user.name "Pon aquí tu nombre"
    $ git config --global user.email "pon@aqui.tu.correo"            
  
  Para tener texto en color:

    $ git config --global color.ui "auto"              
    
    
    
    
/*=======================================
Por ultimo para agregar al localhost/phpmyadmin
=======================================*/  

Editar el archivos



