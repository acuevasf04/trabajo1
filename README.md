# **TRABAJO VAGRANTFILE**
<img width="500" height="609" alt="Vagrant" src="https://github.com/user-attachments/assets/f6909fd2-3772-42b1-8e57-bf1903f5f0da" />

## **1. ÍNDICE**

1. [ÍNDICE]()
2. [INTRODUCCIÓN]()
3. [CONFIGURACIÓN VAGRANTFILE]()
4. [CONFIGURACIÓN MÁQUINAS]()
5. [CONFIGURACION BASE DE DATOS]()
6. [CONFIGURACIÓN APACHE]()
7. [ÚLTIMOS RETOQUES]()

## **2. INTRODUCCIÓN**
Vagrant fue creado para la optimización de crecación y administración de máquinas virtuales usando software, simplificando el proceso. En esta práctica se tiene como objetivo la creación y configuración de una pila LAMP. 

## **3. CONFIGURACIÓN VAGRANTFILE**

En este apartado se enseñaran que en el vagrantfile que se ha configurado se han hecho dos máquinas distintas, una que servirá para configurar los servicios de apache y esta tendría acceso a internet y la otra se usaría para los servicios de la base de dato y no tendría acceso a internet. Tambiém se han añadido dos scripts, una para cada máquina, que harán que se instalen los servicios y se automatice el lanzamiento de esta.
<img width="885" height="317" alt="imagen" src="https://github.com/user-attachments/assets/922dcb08-990b-4578-9e9d-d726a705822a" />


## **4. CONFIGURACIÓN MÁQUINAS**


Se empezará primero con la de apache, ya que la máquina de la base de datos, se ha configurado su enrutamiento dentro del script que le hemos añadido.
Primero se entra en el archivo donde se encuentra la configuración NAT, para ello usaremos ```sudo nano /etc/sysctl.conf```. Una vez dentro del archivo, se descomentará la línea ```net.ipv4.ip_forward=1```. Después se usará el comando ```sudo sysctl -p``` para aplicar los cambios sin necesidad de reiniciar la máquina.

<img width="992" height="627" alt="Captura de pantalla 2025-11-03 201349" src="https://github.com/user-attachments/assets/8b00592c-1d2d-469d-b632-cea0cccbbfc8" />

##**5. CONFIGURACIÓN BASE DE DATOS**

La configuración de la base de datos se recomienda que se hagan las primeras ya que las configuraciones de PHP vienen de como llamamos a la base de datos, donde se encuentra, etc. 
Para entrar en la configuración de la base de datos simplemente tenemos que poner el comando ```sudo mariadb -u root``` entrando así como usuario raíz añadir bases de datos, administrar ususarios, entre otras funciones. Para crear la base de datos se usa el comando ```CREATE DATABASE <NOMBRE DE LA BASE DE DATOS>;```.

<img width="997" height="288" alt="imagen" src="https://github.com/user-attachments/assets/2622215a-9fb8-4e81-9558-a30787c91f3b" />

Se creará una tabla dentro de la base de datos que hemos creado previamente usando los comando ```CREATE TABLE <NOMBRE TABLA>``` y añadimos todos los atributos.

<img width="1275" height="392" alt="imagen" src="https://github.com/user-attachments/assets/4e2665e2-9f98-4172-b923-a4ac36d0d2a1" />

Se crearan más usuarios para la base de datos dentro de la máquina usando ```CREATE USER '<NOMBRE USUSARIO>'@'localhost'```
<img width="687" height="46" alt="imagen" src="https://github.com/user-attachments/assets/b10acae8-7cf5-48b9-aef7-2b1d768103a3" />

Hay que añadir un par de empleados en la tabla.
<img width="988" height="117" alt="imagen" src="https://github.com/user-attachments/assets/04509052-3b90-4fa8-993f-0d48135a2bfb" />

## **6. CONFIGURACIÓN APACHE**

Se pasa ahora a la configuración de apache para el lanzamiento de la aplicación web. Para ello hay que acceder a ```/etc/apache2/sites-availables```donde nos encontraremos con el archivo 000-default.config y se le hará una copia para poder realizar desde ahí la configuración. Es importante hacer las configuraciones de apache dentro de la copia, ya que si se corrompe o falla.

Usando la configuración del balanceador, primero hay que descargarse los 3 modificadores de proxy para la configuración. Luego se tiene que acceder a la máquina de la base de datos y salir las tablas. Se tiene que habilitar la página usando el comando ```sudo a2ensite trabajo.config``` y luego recargar los servicios de apache con ```sudo systemctl reload apache2.service``` y comprobar que funciona.

<img width="937" height="613" alt="imagen" src="https://github.com/user-attachments/assets/3d36f880-5815-4714-a09c-9a3964a5c3ff" />

##**7. ÚLTIMOS RETOQUES**
Para los últimos retoques, lo que hay que hacer es instalar PHP y apache en la máquina de la base de datos, para poder acceder a ella a través del navegador. Hay que configurar como en la otra máquina para poder llegar a ella.

<img width="664" height="286" alt="imagen" src="https://github.com/user-attachments/assets/869fff14-0d4d-49dc-b5d7-b631bb03257c" />

Y al final comprobamos de que la máquina funciona entrando al navegador 
