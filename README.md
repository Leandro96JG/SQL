# SQL
![SQL](mysql.svg "SQL")

## Comandos Principales

### 
````sql
SHOW DATABASE
````
- Mostrar todas las bases de datos

### 
````sql
CREATE DATABASE nombredb
````
- Crear base de datos

### 
````sql
DROP DATABASE nombredb
````
- borra una base de datos


## Operadores De Sentencias

### ``IF EXISTS``
- Sí existe ejecutar script

### ``IF NOT EXISTS``
- Sí no existe ejecutar script

## Crear Usuario Para Una BD

- Normalmente esto lo hace quien está administrando la base de datos, para otorgar permisos a quienes quieran trabajar con nuestra db 

````sql
CREATE USER 'usuario@dominiodb.com' IDENTIFIED BY '(contraseña)'
````

- Para ingresar a la base de datos con el nombre de usuario creado desde la terminal:
````sql
'mysql -u (usuario) -p'
````
e ingresar la contraseña asignada

- Esto no significa que nuestro usuario vaya a tener acceso a nuestras base de datos, para esto es necesario asignarles permisos

### Algunos comandos para dar privilegios

- Otorgar todos los privilegios al usuario asignado.
````sql
GRANT ALL PRIVILEGES ON (Nombre DB) TO 'usuario@dominioDB.com'
```` 

- Unas vez asignado cualquier privilegio, por buena practica, es necesario actualizar nuestra base de datos. Para esto existe el siguiente comando:
````sql
FLUSH PRIVILEGES;
````

- Ver los privilegios que tiene un usuario: 
````sql
SHOW GRANTS FOR 'usuario@dominioDB.com';
````

- Para quitar privilegios 
````sql
REVOKE ALL GRANT OPTION FROM 'usuario@dominiodb.com';
````

- Eliminar usuario 
````sql
DROP USER 'usuario@dominiodb.com'
````

## Tablas

- Crear tabla: 
````sql
CREATE TABLE (nombre)
````

- Elegir nuestra db que vamos a trabajar: 
````sql
USE nombre db
````

- Ver tablas de la db: 
````sql
SHOW TABLES
````

- Crear una tabla: **CREATE nombreTabla (atributos con sus tipos de datos)**. Ej: 
````sql
CREATE usuarios(nombre VARCHAR, correo VARCHAR)
````

- Describir una tabla:
 ````sql
 DESCRIBE (nombre de la tabla)
 ````


### Agregar, Modificar o Eliminar Atributos De Una Tabla

- Agregar atributos:
 ````sql
 ALTER TABLE (tabla) ADD COLUMN (atributo + tipo de datos)
 ````

- Modificar un tipo de datos:
 ````sql
 ALTER TABLE (tabla) MODIFY (atributo existente + tipo de dato nuevo)
 ````

- Renombrar un atributo de una tabla. 
````sql
ALTER TABLE (tabla) RENAME COLUMN (atributo) TO (nuevo nombre)
````

- Eliminar un atributo de una tabla. 
````sql
ALTER TABLE (tabla) DROP COLUMN (atributo)
````

### CRUD de datos en una tabla

- Agregar datos a una tabla:
 ````sql
 INSERT INTO (tabla) VALUES (valores separados por comas)
 ````

**NOTA:**
 _Usar este metodo puede ser una mala practica ya que hay que saber el orden que estan los datos, como buena practica se usa:_ 

````sql
INSERT INTO (nombre de los atributos a ingresar datos)
VALUES (datos a ingresar)
````
- Recordar que los datos autoincrementables no es necesario asignarles valor.

- Leer todos los datos de una tabla: 
````sql
SELECT * FROM (tabla)
````

## Funciones, Operadores Y Clausulas en DB

### ``COUNT()``
- Contador segun una condición. Ej: Todos los usuarios de una db: 
````sql
SELECT COUNT(*) FROM usuarios
````

### ``AS``
- Para darle un _Alias_ a cada operacion hecha por una funcion de db podemos usar el operador **AS** ej: 
````sql
SELECT COUNT(*) AS total_usuarios FROM usuarios
````

### ``WHERE``
- Hacer algo cuando se cumpla una condicion Ej:
 ````sql
 SELECT * FROM usuarios WHERE nombre="Leandro";
 ````

### ``IN``
- Para buscar segun varios datos. Ej: 
```sql
SELECT * FROM usuarios
WHERE nombre
IN (nombres de personas a buscar el registro)
```
 Esto devuelve las comunas que cumplan con los datos agregados.

### ``LIKE``
- Para buscar un patron especifico dentro de una columna en una consulta. Se definen usando dos comodines principales.
1. ``%``: Coincide con cualquier secuencia de caracteres. Puede ser usado al inicio o al final de una cadena.

- ``'A%'`` cualquier valor que comience con 'A'. Ej:
 ````sql
SELECT * FROM usuarios WHERE nombre LIKE 'A%'
````
- ``'%A'`` cualquier valor que termine con 'A'.
- ``'%A%'`` cualquier valor que contenga con 'A'.

2. ``_``:(Guion Bajo) Coicide con un **solo caracter**.
- ``'A_n_'`` Coincidirá con cualquier cadena que tenga cuatro caracteres, donde el primero sea 'A', el segundo sea cualquier carácter, el tercero sea 'n' y el cuarto sea cualquier carácter (como 'Ana', 'Aní').

- Operador ``NOT LIKE`` hace lo inverso.

### Operadores Relacionales

- **Los operadores relacionales** en SQL son utilizados para realizar comparaciones entre valores y son fundamentales en las consultas para filtrar o evaluar datos.

- **Principales Operadores Relacionales**
1. ``=`` (Igual a):
- Compara si dos valores son iguales.
2. ``<> o !=`` (diferente de):
- Compara si dos valores son diferentes.
3. ``< o >`` (Mayo que o Menor que):
- Compara si el valor de la izq es menor o mayor que el de la derecha
4. ``BEETWEEN`` (Entre un rango de valores):
- Verifica si un valor está entre dos valores, inclusivo. Ej: 
````sql
SELECT * FROM usuarios WHERE edad BETWEEN 20 AND 29
````
5. ``IS NULL`` y ``IS NOT NULL`` (Comparación de valores nulos):
- Verifica si un valor es **NULL** o NO es **NULL**. Ej: 
````sql
SELECT * FROM usuarios WHERE direccion IS NULL
````

### Operadores Logicos

- Se usan para combinar multiples condiciones en una consulta. Permiten aplicar lógica condicional (como "y","o","no") para filtrar resultados basados en múltiples criterios.

- **Principales Operadores Lógicos en SQL:**

1. ``AND`` (Y lógico):
- Devuelve **TRUE** si ambas condiciones son verdaderas.
- Cobinar múltiples condiciones en una consulta. Ej:
 ````sql
 SELECT * FROM usuarios 
 WHERE edad > 26 
 AND nombre LIKE 'LE%'
 ````
  Devuelve todos los valores mayores a 26 y que el nombre empiece con 'LE'.

2. ``OR`` (O Lógico):
- Devuelve **TRUE** si alguna de las condiciones es verdadera.

3. ``NOT`` (Negación Lógica):
- Invierte el resultado de una condición, devolviendo **TRUE** cuando la condición es **FALSE** y viceversa.

- **NOTA**: _En consultas más complejas, es recomendable usar parentisis_:
```` sql
SELECT * FROM empleados
WHERE (salario > 2000 OR departamento_id = 3)
AND NOT nombre = 'Carlos';
````

## Sentencia ``UPDATE``

- Se utiliza para modificar los datos existentes en una o más filas de una tabla. Puedes actualizar valores de una o más columnas y aplicar condiciones para determinar qué filas se van a modificar.

````sql
UPDATE usuarios
SET correo = "leandro96@gmail.com", direccion = "Solo existo"
WHERE usuario_id = 1;
````

### _NOTAS IMPORTANTES_:
* **Cláusula** ``WHERE``: Es muy importante usar la cláusula ``WHERE`` para evitar modificar todas las filas de la tabla por accidente.

* **Restricciones y llaves foráneas:** Asegurarse de que cualqier modificación NO viole las restricciones de la DB, como llaves foráneas, únicas o cualquier otra restricción.

* **Reversibilidad**: Una vez realizada la sentencia ``UPDATE``, no se puede deshacer directamente. Por eso es recomendable realizar **BACKUPS** antes de hacer cambios masivos.

## ``DELETE``
- Borrar datos en una o mas filas
- Tambien hay que tener en cuenta usar la cláusula ``WHERE`` si nó te podes mandar el moco de tu vida :).
````sql
DELETE FROM usuarios WHERE usuario_id = 2;
````

## ``TRUNCATE``
- Para reiniciar toda la tabla desde cero (teniendo en cuenta lo id auto incrementables)
````sql
TRUNCATE TABLE usuarios;
````