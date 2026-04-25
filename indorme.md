# TAS1 - Estructura
## 1. Título
Creación y personalizacion de dos servidores web con Nginx
## 2. Tiempo de duración
40 min
## 3. Fundamentos

Docker es una plataforma que nos permite crear, implementar y ejecutar aplicaciones dentro de contenedores. Un contenedor que es una unidad ligera y portátil que incluye todo lo necesario para que una aplicación funcione: el código, las dependencias, las librerías y la configuración. A diferencia de las máquinas virtuales, los contenedores no requieren un sistema operativo completo para cada instancia, sino que comparten el kernel del sistema anfitrión, lo que los hace mucho más rápidos y eficientes.

Nginx es un servidor web de alto rendimiento que también puede funcionar como proxy inverso, balanceador de carga y servidor de contenido estático. Es ampliamente utilizado en entornos de producción por su velocidad, estabilidad y bajo consumo de recursos.

En esta práctica se utiliza Docker para desplegar dos instancias separadas del servidor web Nginx, cada una corriendo en un contenedor independiente. Este enfoque permite tener múltiples servidores web  asignando puertos distintos a cada uno.

La personalización de los servidores se logra modificando el archivo index.html ubicado en la ruta /usr/share/nginx/html/, que es donde Nginx busca el contenido web por defecto. De esta manera, se puede adaptar el contenido que se muestra en el navegador según las necesidades: información institucional en un servidor y datos personales del estudiante en el otro.

## 4. Conocimientos previos
   
- Manejo básico de la terminal o línea de comandos.
- Conocimiento elemental de HTML.
- noción general sobre virtualización o entornos aislados.

## 5. Objetivos a alcanzar
   
Los objetivos alcanzados con la realización de esta práctica fueron:

- Implementar dos servidores web independientes utilizando contenedores Docker.
- Comprender el uso de la imagen oficial de Nginx para desplegar aplicaciones web.
- Personalizar el contenido de los servidores mediante la edición del archivo index.html.
- Familiarizarse con los comandos básicos de Docker para la gestión de contenedores.
- Comprobar el funcionamiento simultáneo de ambos servidores web en diferentes puertos.
- Analizar las ventajas del uso de contenedores en comparación con otros entornos virtualizados.
  
## 6. Equipo necesario
  
- Docker Desktop instalado y funcionando correctamente.
- Editor de texto (Cursor, VS Code o similar).
- Navegador web (Chrome, Firefox o Edge).

## 7. Material de apoyo
   
- Documentación oficial de Docker: https://docs.docker.com
- Documentación oficial de Nginx: https://nginx.org
- Guías y manuales sobre comandos básicos de Docker.
- Recursos del aula virtual.
  
## 8. Procedimiento

**Paso 1: Crear el primer contenedor Nginx**
Se ejecuta este comando para crear el contenedor nginx1 y exponerlo en el puerto 8089:

```bash
docker run -d --name nginx1 -p 8089:80 nginx
```

![Figura 8-1. Creación de primer contenedor.](./img/Screenshot%202025-10-18%20185431.png)

Abrir en el navegador:
 http://localhost:8089

![Figura 8-1. Localhost del 2do contenedor.](./img/Screenshot%202025-10-18%20185606.png)

**Paso 2: Crear el primer contenedor Nginx**
Se ejecuta este comando para crear el contenedor nginx1 y exponerlo en el puerto 8089:

```bash
docker run -d --name nginx2 -p 8090:80 nginx
```

![Figura 8-1. Creación de segundo contenedor.](./img/Screenshot%202025-10-18%20185704.png)

Abrir en el navegador:
 http://localhost:8090

![Figura 8-1. Localhost del 2do contenedor.](./img/Screenshot%202025-10-18%20185745.png)

**Paso 3: Copiar el archivo index.html del contenedor nginx1 al anfitrión**
Copiar el archivo original para poder editarlo:

```bash
docker cp nginx1:/usr/share/nginx/html/index.html ./index1.html
```
Abrir el archivo con un editor de texto e editar

![Figura 8-3. Uso de cp para copiar el archivo html.](./img/Screenshot%202025-10-18%20190902.png)

**Paso 4: Copiar el archivo editado al contenedor nginx**
Ejecutamos el comando para copiar el archivo editado e subir a los contenedores creados

```bash
docker cp index1.html nginx1:/usr/share/nginx/html/index.html
```

Y actualiza el navegador en http://localhost:8089 y http://localhost:8090

![Figura 8-4. Redirección de contenido de notas.txt a resumen.txt.](./img/Screenshot%202025-10-18%20203027.png)

## 9. Resultados esperados
    
- Dos contenedores Nginx activos y ejecutándose en paralelo (nginx1 y nginx2).
- El primer servidor (puerto 8089) muestra información institucional personalizada.
- El segundo servidor (puerto 8090) muestra información personal del estudiante.
- El estudiante comprende el proceso completo de creación, modificación y despliegue de contenedores.
- Se evidencia el funcionamiento independiente de ambos servicios web al ingresar a:

    http://localhost:8089
 → Información institucional

    http://localhost:8090
 → Información personal

- Comprensión práctica del aislamiento de servicios y la reutilización de imágenes Docker.

## 10. Bibliografía
    
Docker Inc. (2024). Docker Documentation. Recuperado de: https://docs.docker.com

Nginx, Inc. (2024). NGINX Documentation. Recuperado de: https://nginx.org/en/docs/


Merkel, D. (2014). Docker: Lightweight Linux Containers for Consistent Development and Deployment. Linux Journal, (239), 2–10.

Red Hat. (2023). Understanding containers and Docker. Recuperado de: https://www.redhat.com/en/topics/containers/what-is-docker