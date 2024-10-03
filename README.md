# Curso Sql - Jonmircha

## Comandos Principales

### _Show databases_
- Mostrar todas las bases de datos

### _Create databases (nombre db)_
- Crear base de datos

### _Drop databases (nombre db)_
- borra una base de datos


## Operadores De Sentencias

### _IF EXISTS_
- Sí existe ejecutar script

### _IF NOT EXISTS_
- Sí no existe ejecutar script

## Crear Usuario Para Una BD

- Normalmente esto lo hace quien está administrando la base de datos, para otorgar permisos a quienes quieran trabajar con nuestra db 

- **CREATE USER '(_usuario_)'@'(_dominio_db_)' IDENTIFIED BY '(_contraseña_)'**

- Para ingresar a la base de datos con el nombre de usuario creado desde la terminal:
**_'mysql -u (usuario) -p'_** e ingresar la contraseña asignada

- Esto no significa que nuestro usuario vaya a tener acceso a nuestras base de datos, para esto es necesario asignarles permisos

### Algunos comandos para dar privilegios

- **GRANT ALL PRIVILEGES ON (_Nombre DB_) TO '_(usuario)_@(_dominioDB_)'** Otorga todos los privilegios al usuario asignado.

- Unas vez asignado cualquier privilegio, por buena practica, es necesario actualizar nuestra base de datos. Para esto existe el siguiente comando: **FLUSH PRIVILEGES**

- Ver los privilegios que tiene un usuario: **SHOW GRANTS FOR '(usuario)'@'(dominioDB)'**

- Para quitar privilegios **REVOKE ALL GRANT OPTION FROM '(usuario)@'(dominiodb)'**

- Eliminar usuario **DROP USER '(usuario)@'(dominiodb)'**

## Crear Tablas En Nuestras Bases de Datos

- Elegir nuestra db que vamos a trabajar: **USE (nombre db)**

- Ver tablas de la db: **SHOW TABLES**

- Crear una tabla: *CREATE _nombreTabla_(_atributos con sus tipos de datos_)*. Ej: **CREATE usuarios(_nombre_ VARCHAR, _correo_ VARCHAR)**

- Describir una tabla: **DESCRIBE (nombre de la tabla)**


## Agregar, Modificar o Eliminar Datos De Una Tabla

- Agregar datos: **ALTER TABLE (tabla) ADD COLUMN (dato + tipo de datos)**

- Modificar un tipo de datos: **ALTER TABLE (tabla) MODIFY (dato existente + tipo de dato nuevo)**