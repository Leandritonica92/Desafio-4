#                                                                            **DESAFIO 4**
---
## Objetivos del desafío: 
## El objetivo de este ejercicio es aprender a configurar y utilizar roles de AWS IAM desde la linea de comandos (CLI) para permitir la escritura en un bucket de s3:

## Escenario: Eres un Administrador de sistemas en una empresa que utiliza AWS para sus servicios en la nube. Te han asignado la tarea de configurar un rol de IAM que permita a los usuarios asumirlo desde la CLI para escribir archivos en un bucket de s3 especifico.


1. **Instalación de aws cli con el comando sudo apt-get install aws cli:**



 https://i.postimg.cc/4N3mkdvy/1.png


- Con el comando aws --version podemos verificar que la instalación de aws cli se haya instalado correctamente y la versión a la que esta se instalo 



**Con el comando aws --version podemos verificar que la instalación de aws cli se haya instalado correctamente y la versión a la que esta se instalo**

 
 
  https://i.postimg.cc/k4fqfQpc/2.png

  

**Creamos un usuario IAM con acceso programático:** 


**Para realizar este paso necesitamos acceder con nuestro usuario y credenciales a la plataforma de aws**
**- En el panel de servicios colocamos “IAM”**
**- Luego vamos a “user” en el panel izquierdo**


https://i.postimg.cc/MZ3zBYRZ/3.png



**- luego vamos a la derecha a “crear usuario”**



https://i.postimg.cc/Pq6dMbcM/4.png



**- En user name le colocamos un nombre al usuario en este caso “admin-root”**



https://i.postimg.cc/TYrGsvF1/5.png



**- Creamos una contraseña para el usuario y le damos a next**



https://i.postimg.cc/SxS0t2c1/6.png



**- Seleccionamos los permisos para el usuario en este caso “AdministratorAccess” y le damos a next**


https://i.postimg.cc/nc1g7FN4/7.png




**- Seleccionamos crear usuario**



https://i.postimg.cc/MpK4Yk8h/8.png



**- ingresamos el usuario y la credencial y accedemos a la cuenta de usuario generada**




https://i.postimg.cc/bwC5C6yd/9.png




**- Una vez ingresado a la plataforma podemos visualizar en la esquina superior derecha el nombre de usuario que nos identifica el usuario al que estamos haciendo uso.**



https://i.postimg.cc/QtL0wwRN/10.png




**-Creamos una clave programática**


**Para eso ingresamos al usuario, luego vamos a la pestaña de “security credencials"**



https://i.postimg.cc/tCRDKhm6/11.png



**En el siguiente paso vamos a “Access keys”**




https://i.postimg.cc/4xmPdXGN/12.png



**Colocamos command line interface**



https://i.postimg.cc/gJPHNRZn/13.png



**- luego descargamos el Access key y el Secret key:, estas dos claves nos van a proveer el acceso  a los servicios aws cli**


https://i.postimg.cc/8k4mm7Pz/14.png


**- Configuramos la consola con el comando “configure”:**


**Colocamos el Access key, el secret acces key, la región y el formato**


https://i.postimg.cc/LXRjzpcP/Captura.png


**Creamos el bucket s3 atravez de la consola con el comando**

**1-	BUCKET_NAME= ”les3desafio4”**
**2-	aws s3 mb s3://$BUCKET_NAME**
**3-	luego abajo Podemos verificar los buckets que hay creados**



https://i.postimg.cc/BbnDVCQQ/16.png



**En el siguiente paso creamos las políticas JSON necesarias que nos van a permitir la escritura en nuestra bucket s3 creado, utilizamos el editor de texto “nano”**



**Creamos dos políticas:**


**1-	“s3-permisos.json” que es la política destinada al bucket s3**
**2-	- En effect colocamos “Allow” permite la acción especificada**
**3-	- En Action especifica la acción que esta permitida. En este caso. “s3.PutObject” permite la acción de colocar un objeto en el buckets3**
**4-	En Resource especificamos los recursos a los que se le aplica la política en este caso el arn "arn:aws:s3:::les3desafio4/*” indica que la acción “s3:PutObject”  está **permitida en todos los objetos (/*) dentro del bucket s3 “les3desafio4”**


https://i.postimg.cc/KvVL0BXx/17.png




**5-	“Este archivo “policyrole.json”  define una política de IAM en AWS que permite a la  cuenta específica (arn:aws:iam::119295402406) asumir un rol (sts:AssumeRole).**

- **En effect colocamos “Allow” permite la acción especificada**
- **En Principal especificamos que la cuenta con el arn  tiene permiso para realizar una acción**
- **En Action sts:AssumeRole especificamos la acción que esta permitida, en este caso permite a la cuenta de aws (arn:aws:iam::119295402406) asumir el rol en aws**



https://i.postimg.cc/G3gspGmG/18.png



**Para crear el Rol, debes empezar por establecer una política de confianza que determine quién tiene permiso para utilizar ese rol. Aquí tienes un ejemplo sencillo de una política de confianza para un rol que permite a un servicio de AWS asumir ese rol.**



https://i.postimg.cc/QMqFZWzB/19.png



**Luego creamos el Rol y adjuntamos la política usando “S3-WriteRoleLean” con el siguiente comando**




https://i.postimg.cc/jS02WX0w/20.png



https://i.postimg.cc/k4pX7Nv5/21.png



**Creamos un usuario Iam con credenciales programáticas**



https://i.postimg.cc/zG8Ltjtm/1.png



https://i.postimg.cc/0NNzxN1c/2.png



**Con este comando creamos el Access key para el usuario**



https://i.postimg.cc/7LQfLyxD/safasf.png



**Modificamos el archivo trust policy y vamos a incluirlo dentro del json apuntando al user s3-support1**




https://i.postimg.cc/MH061k8n/4.png




**Actualizar el rol**



https://i.postimg.cc/wTHTgBhL/5.png




**Configurar las credenciales del nuevo rol**


https://i.postimg.cc/jS3sHQB4/6.png



**Asumimos el rol**



https://i.postimg.cc/L85S8ghY/7.png



**Subimos un archivo de prueba al bucket s3://les3desafio4 desde el CLi**



https://i.postimg.cc/P57jpf86/8.png



https://i.postimg.cc/yYQqt6nV/9.png




**En la primera línea dentro de los “Objetos” del Bucket S3 podemos visualizar el archivo previamente enviado desde el CLI de aws**




https://i.postimg.cc/d3sXNgyk/10.png





**Material Adicional:**


https://i.postimg.cc/tCmfDSCJ/11.png



https://i.postimg.cc/P5p77WP4/12.png



https://i.postimg.cc/VkxhPJtc/13.png



**- Se crea un bucket S3, se configura un rol con la política necesaria, se genera un usuario IAM con credenciales programáticas, se actualiza la política del rol para permitir la asunción por parte del usuario “s3-support-1”, y se conecta la CLI con las credenciales del usuario s3-support-1**
**- El usuario s3-support-1 utiliza las credenciales configuradas en la CLI para asumir el rol IAM creadas anteriormente. Este rol tiene una política que permite escribir en el bucket S3 creado anteriormente**


**Diagrama de Asunción de Rol:**

**IAM User (s3-support-1): Este es el usuario IAM que está intentando acceder a recursos protegidos por el rol.**

**IAM Role: Representa el rol IAM con la política adjunta que permite la escritura en el bucket S3.**

**S3 Bucket: Es el recurso al que el rol IAM tiene acceso para escribir datos.**

**El proceso de asumir el rol implica que el usuario s3-support-1 obtiene temporalmente permisos y credenciales asociadas al rol IAM, permitiéndole realizar acciones específicas como escribir en el bucket S3. Una vez que la tarea se completa, el usuario puede regresar a sus permisos IAM originales.**
**Este diagrama refleja cómo los roles IAM facilitan el acceso temporal y controlado a recursos específicos en AWS, cumpliendo con los principios de seguridad y gestión de acceso de manera eficaz**