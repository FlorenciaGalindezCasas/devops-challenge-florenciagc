## **Despliegue en PC local**
Se agrego un archivo Dockerfile tanto en la carpeta de backend como en la de frontend, estos archivos contienen un conjunto de instrucciones que se ejecutan sucesivamente para realizar acciones en la imagen.

### _**Dockerfile backend:**_  
Modifiqué el archivo _requierements.txt_ ya que se generaban errores con algunos requerimentos. Para eso debí agregar estos al dockerfile con el comando _**RUN pip install nombre_requieriment**_.

Con el comando _**EXPOSE 8000**_ indico el puerto donde correra la app de Django.

Luego en la terminal se ejecuta el comando _**docker build -t nombre_imagen**_, el cual me crea una imagen en docker.

Se ejecuta el comando _**docker run -dp 8000:8000 nombre_imagen**_ para correr la imagen en el puerto 8000.

Con el comando _**python manage.py runserver**_ se abre una ventana en el navegador donde se despliega la imagen de docker correspondiente al backend. Especificamente en el puerto 8000.

Para resolver errores por los cuales no me renderizaba la aplicacion tuve que instalar las Third apps con el comando _**pip install thirdapp**_. Ej: pip install djangorestframework.

### _**Dockerfile frontend:**_  
Se ejecuta el comando _**docker build -t nombre_imagen**_, el cual me crea una imagen en docker.

Se ejecuta el comando _**docker run -dp 3000:3000 nombre_imagen**_ para correr la imagen en el puerto 3000.

Luego se abre una ventana en el navegador con el comando _**npm start**_. Esto se hace en el puerto: 3000. Donde se renderiza un frontend creado con Reactjs.

### _**Dockerfile-compose:**_  
Docker Compose es una herramienta que se desarrolló para ayudar a definir y compartir aplicaciones de varios contenedores.  
Con Compose, se puede crear un archivo YAML para definir los servicios y, con un solo comando, podemos activar o desactivar todo.  
Solo se necesitaría clonar su repositorio e iniciar la aplicación de redacción.  
El archivo Docker-compose.yml se crea en la raíz de la aplicación. En éste se define la lista de servicios o contenedores que queremos ejecutar.  

Se ejecuta el comando _**docker-compose up**_ y Compose iniciará y ejecutará toda la aplicación.
 ______________________________________________________________________________________________________________________________________________________________

 ## FUENTES:
 - [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
 - [Docker Compose](https://hub.docker.com/r/docker/compose/#!)

**___________________________________________________________________________________________________________________________________________________________**

## **Despliegue en AWS**

**1.** Ingresar a EC2 en AWS.  
**2.** Crear una key pairs.  
**3.** Insertar el archivo descargado keypairs.pem dentro de la carpeta .ssh.  
**4.** Crear una instancia en EC2, escogi Amazon Linux AMI.   
**5.** Ejecuto comando _**chmod 600 keypair.pem**_ para otorgar permiso de lectura.  
**6.** Ejecuto comando _**ssh -i "keypair.pem" ec2-user@IP publica**_ para acceder al servidor.  
**7.** Ejecuto _**yum update**_ para actualizar todos los paquetes de Linux.  
**8.** Instalo docker en AWS:  
   1. Ejecuto _**sudo yum install docker -y**_.
   2. Incio el servicio con _**sudo service docker start**_.
   3. Ejecuto _**sudo usermod -a -G docker ec2-user**_ que crea automáticamente un grupo 'docker' que tiene privilegios de root por defecto.  

**9.** Agrego imagenes de docker a un repositorio ECR (servicio de registro de imágenes de contenedor):
   1. Recuperar un token de autenticación y autenticar su cliente de Docker en el registro. _**aws configure**_   
      Utilice AWS CLI:  
      _**aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 728221614068.dkr.ecr.us-east-1.amazonaws.com**_
   2. Previamente debo subir las imagenes que tengo en el docker local a dockerhub. Y luego hacer _**docker pull florenciagc/image-backend:latest**_   
   3. Etiquetar la imagen para poder enviarla a este repositorio:  
      _**docker tag IDimage 728221614068.dkr.ecr.us-east-1.amazonaws.com/florenciagc/web-page-docker:latest**_
   4. Ejecutar el siguiente comando para enviar esta imagen al repositorio de AWS recién creado:  
      _**docker push 728221614068.dkr.ecr.us-east-1.amazonaws.com/florenciagc/web-page-docker:latest**_  

**10.** Ejecuto _**docker run -d -p port:port repository:tag**_   
**11.** Abro la IP publica de la instancia en EC2. Deberia renderizar la aplicacion.  

 ______________________________________________________________________________________________________________________________________________________________

 ### FUENTES:
 - [Desplegar aplicaciones en AWS](https://www.youtube.com/watch?v=xrBgkxByRQg)
 - [Cómo usar contenedores Docker con AWS EC2](https://hostadvice.com/how-to/how-to-use-docker-containers-with-aws-ec2-2/)
 - [Dockerhub](https://hub.docker.com/)





