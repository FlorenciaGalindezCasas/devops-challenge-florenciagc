Para la creacion del CI/CD utilicé [GitHub Actions](https://docs.github.com/en/actions).  

## **GitHub Actions**  
GitHub Actions es una plataforma de integración continua y entrega continua (CI/CD) que le permite automatizar su canalización de compilación, prueba e implementación.  

### Crear un flujo de trabajo  
GitHub Actions usa la sintaxis YAML para definir el flujo de trabajo. Cada flujo de trabajo se almacena como un archivo YAML independiente en su repositorio de código, en un directorio llamado .github/workflows.  

Puede crear un flujo de trabajo en su repositorio que activa automáticamente una serie de comandos cada vez que se envía código.  

**1.** Cree un nuevo nombre secreto DOCKERHUB_USERNAMEy su ID de Docker como valor.Cree un nuevo token de acceso personal (PAT) para Docker Hub.  

**2.** En su repositorio, cree el .github/workflows/directorio para almacenar sus archivos de flujo de trabajo.  

**3.** En el .github/workflows/directorio, cree un nuevo archivo .yml  

### Ejecutar:

- docker-compose build
- docker-compose up
- docker run -p 8001:80 florenciagc/devops-nginx:tagname
- Abrir localhost:8001

 ______________________________________________________________________________________________________________________________________________________________

 ### FUENTES:
 - [Introduction to GitHub Actions](https://docs.docker.com/build/ci/github-actions/)
 - [About continuous integration](https://docs.github.com/en/actions/automating-builds-and-tests/about-continuous-integration)
 - [Guía de inicio rápido para GitHub Actions](https://docs.github.com/es/actions/quickstart)

