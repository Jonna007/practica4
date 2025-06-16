
# 📄 Práctica No 4 - Contenedores PostgreSQL y pgAdmin conectados mediante red personalizada en Docker

## 1. Título

**Práctica No 4**: Creación de contenedores PostgreSQL y pgAdmin, conectados a través de red Docker personalizada

## 2. Tiempo de duración

Aproximadamente 2 hora

## 3. Fundamentos

En esta práctica se abordó la implementación de dos contenedores Docker: uno ejecutando el motor de base de datos PostgreSQL y otro con la herramienta gráfica pgAdmin para la gestión de dicha base de datos. A través de Docker, los contenedores fueron conectados mediante una red personalizada para permitir la comunicación entre ellos.

Se trabajaron los siguientes conceptos clave:

- **Contenedores Docker**: Entornos aislados donde se ejecutan servicios con todas sus dependencias.
- **Red personalizada en Docker**: Medio que permite a los contenedores comunicarse de forma segura y eficiente.
- **pgAdmin**: Interfaz web para administrar bases de datos PostgreSQL.

Comandos importantes usados:

- `docker network create`: para crear la red `redleo`.
- `docker run -d`: para lanzar los contenedores PostgreSQL y pgAdmin.
- `docker network connect`: para unir los contenedores a la red.
- `docker inspect`: para revisar configuración de red y conectividad.

## 4. Conocimientos previos

- Uso básico de Docker y terminal.
- Fundamentos de bases de datos PostgreSQL.
- Gestión de redes de contenedores.
- Navegación en interfaces como pgAdmin.

## 5. Objetivos a alcanzar

- Crear un contenedor PostgreSQL.
- Crear un contenedor pgAdmin.
- Conectar ambos contenedores mediante una red personalizada en Docker.
- Administrar PostgreSQL desde pgAdmin creando una base de datos de prueba.

## 6. Equipo necesario

- Sistema operativo: Windows 11 Home
- Procesador: AMD Ryzen 5 3500U with Radeon Vega Mobile Gfx 2.10 GHz
- Memoria RAM: 8 GB
- Docker Desktop instalado y funcionando
- Navegador para acceder a pgAdmin

## 7. Material de apoyo

- Documentación oficial de Docker
- Manual oficial de PostgreSQL
- Sitio web oficial de pgAdmin
- Videos de apoyo docente (EVA)
- Cheatsheets de redes Docker

## 8. Procedimiento

**Paso 1:** Verificar versión de Docker y descargar imagen PostgreSQL  
`docker -v`  
`docker pull postgres`

**Paso 2:** Crear contenedor PostgreSQL  
```bash
docker run -d --name dbsql -e POSTGRES_PASSWORD=1611 -p 5432:5432 postgres
```

**Paso 3:** Crear contenedor pgAdmin  
```bash
docker run -d --name pgadmin -p 8090:80 \
-e PGADMIN_DEFAULT_EMAIL=jjcadme@sudamericano.edu.ec \
-e PGADMIN_DEFAULT_PASSWORD=1611 \
dpage/pgadmin4
```

**Paso 4:** Crear red personalizada  
```bash
docker network create --attachable redleo
```

**Paso 5:** Conectar contenedores a la red  
```bash
docker network connect redleo dbsql
docker network connect redleo pgadmin
```

**Paso 6:** Verificar conectividad  
```bash
docker inspect redleo
```

**Paso 7:** Acceder a pgAdmin en navegador  
URL: `http://localhost:8090`  
Login:  
- Email: `jjcadme@sudamericano.edu.ec`  
- Contraseña: `1611`

**Paso 8:** Crear base de datos desde pgAdmin  
- Agregar nuevo servidor.
- Nombre: `postgresql-local`
- Host: `dbsql`
- Usuario: `postgres`
- Contraseña: `1611`
- Crear base de datos `appweb` desde la interfaz.

## 9. Resultados esperados

Esta práctica permitió crear y gestionar servicios de base de datos en contenedores con PostgreSQL y pgAdmin. Se utilizó una red personalizada para permitir la conexión directa entre ambos contenedores.

Se logró:
- Crear dos contenedores funcionales.
- Acceder y gestionar PostgreSQL mediante pgAdmin desde el navegador.
- Comprobar la comunicación efectiva mediante red Docker.

## 10. Bibliografía

- pgAdmin Development Team. (2025). *pgAdmin – PostgreSQL Tools*. https://www.pgadmin.org/
- PostgreSQL Global Development Group. (2025). *PostgreSQL: A powerful, open-source object-relational database system*. https://www.postgresql.org/
