# HTACCESS (Hypertext Access)

> *Archivo de configuración para servidores web basados en Apache HTTP Server. Archivo de texto plano que permite a los administradores del servidor o desarrolladores web configurar directivas específicas para un directorio (y sus subdirectorios) sin necesidad de editar el archivo de configuración principal del servidor. Este archivo se debe posicionar en la carpeta raiz del direcotrio*

---

## Configuraciones Basicas

### 1. Creacion del Archivo
Se crea un nuevo archivo con el nombre **.htaccess**

> Esta configuracion sera aplicada a la web de ejemplo

#### 2. Restringir acceso al listado archivos de las carpetas que no tengan archivo indice (Si se escribe la ruta el archivo abra accesso):
    ~~~
    Options All -Indexes
    ~~~

#### 3. Renstrigir el acceso a una carpeta especifica:
* Crear el archivo htaccess en la carpeta y poner
    ~~~
    Order Deny,Allow
    Deny from all
    ~~~

#### 4. Redirecionar pagina segun error (Los estilos pueden en el mismo arhivo):
    ~~~
    ErrorDocument 404 /NoHayVacaciones/Htaccess/Web_Ejemplo/404.html
    ~~~

#### 5. Configuracion global del servidor
* Crear archivo en la carpeta raiz del servidor(para xampp es **htdocs**)
* Escribir el codigo necesario

#### 6. Proteger directorio con usuario y contraseñas

> Esto es recomendable hacerlo al servidor 

* Archivo htaccess en carpeta raiz y poner
    ~~~
    AuthName "Autorizacion Requerida"
    AuthUserFile C:\xampp\htdocs\NoHayVacaciones\Htaccess\Web_Ejemplo\passwords\.htpasswd (Tener en cuenta la forma de la ruta)
    AuthType Basic
    requiere user Felipe Samuel Daniel Esteban Bianchi
    ~~~

* Crear archivo donde van a estar las contraseñas **htpasswd** (Este archivo va a estar relacionado con **AuthUserFile**)

* Ir a un generador de contraseñas con proteccion (htpasswd Generator) y poner usuario y cts

* En el archivo **htpasswd** poner la contraseña

#### 7. Redireccion a un archivo que no sea archivo indice cuando se abra la carpeta raiz
~~~
RewriteEngine On
RewriteRule ^$ /NoHayVacaciones/Htaccess/Web_Ejemplo/401.html [R=302,L]
~~~

---

## Referencias 📚

Video Tutoriales y Canales de donde obtuve la información:

1. [0# - 💻 HTACCESS](https://www.youtube.com/watch?v=y9KEgh6yXME&list=PLH_tVOsiVGzkGD2sB-cmSkxKzvoMYZrHL&index=1 "Tutorial") - Carlos Alfaro