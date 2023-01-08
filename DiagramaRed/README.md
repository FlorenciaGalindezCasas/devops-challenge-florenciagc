## **RED, MAQUINAS VIRTUALES, ALTA DISPONIBILIDAD Y CARGAS VARIABLES**

  Inicialmente, se crea el recurso VPC (Nubes virtuales privadas) que es la base sobre la que crearemos los demas recursos para que estos tengan red o conectividad.

  Para albergar el backend y el frontend, se utilizan los recursos EC2 que son maquinas virtuales en la nube, compatibles con docker para los despliegues.

  Luego, para activar la alta disponiblidad, segun la documentacion de AWS, debemos disponer los servicios EC2 en diferentes zonas de disponibilidad mediante un autoscaling group (permite que decidamos que cantidad de maquinas iguales hay y a su vez ubicarlas en distintas zonas) y para acceder a ellos, usaremos un balanceador de carga. 

  Dicho esto, en resumen tenemos:
  - Una **VPC** que tendra todos los recursos de AWS.
  - Un **balanceador de carga** que recibira las solicitudes de los usuarios que quieran acceder al frontend y las distribuya entre las maquinas EC2 creadas.
  - **Dos redes publicas (subnet)**, una para cada zona de disponibilidad ya que son fisicamente lugares diferentes. Las maquinas EC2 necesitan estar en una red
    para que se les asigne una IP y debe ser publica para que el FRONTEND pueda ser accesible para los usuarios.
  - Dos maquinas virtuales **EC2** para el FRONTEND y dos para el BACKEND, cada una en un grupo de autoscaling para ser compatible con cargas variables, pero a
    su vez con alta disponibilidad debido a que cada una de estas maquinas esta en una zona de disponibilidad diferente. El grupo de autoscaling puede configurarse para que haya mas de una maquina EC2 por cada zona de disponibilidad tambien.  


## **BASES DE DATOS Y BACKEND**

  Para la seccion de bases de datos y su conexion con el BACKEND, elegi:

  **DYNAMODB:** para las bases de datos no relacionales, super-rápida y auto-escalable.
  **AURORA:** para las bases relacionales, porque es hasta cinco veces más rápida que las bases de datos de MySQL estándar y tres veces más rápida que las bases de datos de PostgreSQL estándar. 

  Los servicios de AURORA y DYNAMODB permiten tener "replicas", segun la documentacion de AWS, que servirian para configurar la alta disponibilidad, ya que la base de datos principal, supongamos las que nombre con una letra "A" al final, estan en una zona de disponibilidad A, y las replicas estaran en la zona B.
  No esta de mas mencionar que las bases de datos se encuentran en otras redes SUBNET diferentes a las del BACKEND y FRONTEND, ya que es una buena practica   separar en otras redes a las bases de datos, debido a que suelen tener informacion confidencial o sensible.

  BACKEND en zona de disponibilidad A se conectara a las bases de datos en la zona A, mientras que el backend en B, en las bases de B respectivamente.  


  ## **CONEXION A SERVICIOS EXTERNOS**

  El BACKEND debe consumir dos servicios externos cuya arquitectura desconocemos. Por externo entendemos que esta fuera de la nube, por lo que el backend deberia conectarse a internet para conectarse a estos servicios.

  Segun la documentacion de AWS sobre redes y conectividad con internet, hay un recurso llamado INTERNET GATEWAY que permite configurar que las maquinas EC2 en dicha red publica puedan navegar por internet y conectarse con recursos externos.  

 **_______________________________________________________________________________________________________________________________________________________________________________________________________________**
  ### **FUENTES**

  - [Estabilidad estática con zonas de disponibilidad](https://aws.amazon.com/es/builders-library/static-stability-using-availability-zones/)
  - [VPC](https://docs.aws.amazon.com/es_es/vpc/latest/userguide/what-is-amazon-vpc.html)
  - [Internet Gateway](https://docs.aws.amazon.com/es_es/vpc/latest/userguide/VPC_Internet_Gateway.html)
  - [VPC-EC2](https://www.youtube.com/watch?v=I0nL0NX4qZc)
  - [Servicios AWS](https://www.linkedin.com/pulse/listado-de-todos-los-servicios-amazon-web-services-daniel-pe%C3%B1a-silva/)
