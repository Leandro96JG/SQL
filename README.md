![SQL](mysql.svg "SQL")
![SQL](sql-seeklogo.svg)

# SQL

## Comandos Principales

###

```sql
SHOW DATABASE
```

- Mostrar todas las bases de datos

###

```sql
CREATE DATABASE nombredb
```

- Crear base de datos

###

```sql
DROP DATABASE nombredb
```

- borra una base de datos

## Operadores De Sentencias

### `IF EXISTS`

- Sí existe ejecutar script

### `IF NOT EXISTS`

- Sí no existe ejecutar script

## Crear Usuario Para Una BD

- Normalmente esto lo hace quien está administrando la base de datos, para otorgar permisos a quienes quieran trabajar con nuestra db

```sql
CREATE USER 'usuario@dominiodb.com' IDENTIFIED BY '(contraseña)'
```

- Para ingresar a la base de datos con el nombre de usuario creado desde la terminal:

```sql
'mysql -u (usuario) -p'
```

e ingresar la contraseña asignada

- Esto no significa que nuestro usuario vaya a tener acceso a nuestras base de datos, para esto es necesario asignarles permisos

### Algunos comandos para dar privilegios

- Otorgar todos los privilegios al usuario asignado.

```sql
GRANT ALL PRIVILEGES ON (Nombre DB) TO 'usuario@dominioDB.com'
```

- Unas vez asignado cualquier privilegio, por buena practica, es necesario actualizar nuestra base de datos. Para esto existe el siguiente comando:

```sql
FLUSH PRIVILEGES;
```

- Ver los privilegios que tiene un usuario:

```sql
SHOW GRANTS FOR 'usuario@dominioDB.com';
```

- Para quitar privilegios

```sql
REVOKE ALL GRANT OPTION FROM 'usuario@dominiodb.com';
```

- Eliminar usuario

```sql
DROP USER 'usuario@dominiodb.com'
```

## Tablas

- Crear tabla:

```sql
CREATE TABLE (nombre)
```

- Elegir nuestra db que vamos a trabajar:

```sql
USE nombre db
```

- Ver tablas de la db:

```sql
SHOW TABLES
```

- Crear una tabla: **CREATE nombreTabla (atributos con sus tipos de datos)**. Ej:

```sql
CREATE usuarios(nombre VARCHAR, correo VARCHAR)
```

- Describir una tabla:

```sql
DESCRIBE (nombre de la tabla)
```

### Agregar, Modificar o Eliminar Atributos De Una Tabla

- Agregar atributos:

```sql
ALTER TABLE (tabla) ADD COLUMN (atributo + tipo de datos)
```

- Modificar un tipo de datos:

```sql
ALTER TABLE (tabla) MODIFY (atributo existente + tipo de dato nuevo)
```

- Renombrar un atributo de una tabla.

```sql
ALTER TABLE (tabla) RENAME COLUMN (atributo) TO (nuevo nombre)
```

- Eliminar un atributo de una tabla.

```sql
ALTER TABLE (tabla) DROP COLUMN (atributo)
```

### CRUD de datos en una tabla

- Agregar datos a una tabla:

```sql
INSERT INTO (tabla) VALUES (valores separados por comas)
```

**NOTA:**
_Usar este metodo puede ser una mala practica ya que hay que saber el orden que estan los datos, como buena practica se usa:_

```sql
INSERT INTO (nombre de los atributos a ingresar datos)
VALUES (datos a ingresar)
```

- Recordar que los datos autoincrementables no es necesario asignarles valor.

- Leer todos los datos de una tabla:

```sql
SELECT * FROM (tabla)
```

## Funciones, Operadores Y Clausulas en DB

### `COUNT()`

- Contador segun una condición. Ej: Todos los usuarios de una db:

```sql
SELECT COUNT(*) FROM usuarios
```

### `AS`

- Para darle un _Alias_ a cada operacion hecha por una funcion de db podemos usar el operador **AS** ej:

```sql
SELECT COUNT(*) AS total_usuarios FROM usuarios
```

### `WHERE`

- Hacer algo cuando se cumpla una condicion Ej:

```sql
SELECT * FROM usuarios WHERE nombre="Leandro";
```

### `IN`

- Para buscar segun varios datos. Ej:

```sql
SELECT * FROM usuarios
WHERE nombre
IN (nombres de personas a buscar el registro)
```

Esto devuelve las comunas que cumplan con los datos agregados.

### `LIKE`

- Para buscar un patron especifico dentro de una columna en una consulta. Se definen usando dos comodines principales.

1. `%`: Coincide con cualquier secuencia de caracteres. Puede ser usado al inicio o al final de una cadena.

- `'A%'` cualquier valor que comience con 'A'. Ej:

```sql
SELECT * FROM usuarios WHERE nombre LIKE 'A%'
```

- `'%A'` cualquier valor que termine con 'A'.
- `'%A%'` cualquier valor que contenga con 'A'.

2. `_`:(Guion Bajo) Coicide con un **solo caracter**.

- `'A_n_'` Coincidirá con cualquier cadena que tenga cuatro caracteres, donde el primero sea 'A', el segundo sea cualquier carácter, el tercero sea 'n' y el cuarto sea cualquier carácter (como 'Ana', 'Aní').

- Operador `NOT LIKE` hace lo inverso.

### Operadores Relacionales

- **Los operadores relacionales** en SQL son utilizados para realizar comparaciones entre valores y son fundamentales en las consultas para filtrar o evaluar datos.

- **Principales Operadores Relacionales**

1. `=` (Igual a):

- Compara si dos valores son iguales.

2. `<> o !=` (diferente de):

- Compara si dos valores son diferentes.

3. `< o >` (Mayo que o Menor que):

- Compara si el valor de la izq es menor o mayor que el de la derecha

4. `BEETWEEN` (Entre un rango de valores):

- Verifica si un valor está entre dos valores, inclusivo. Ej:

```sql
SELECT * FROM usuarios WHERE edad BETWEEN 20 AND 29
```

5. `IS NULL` y `IS NOT NULL` (Comparación de valores nulos):

- Verifica si un valor es **NULL** o NO es **NULL**. Ej:

```sql
SELECT * FROM usuarios WHERE direccion IS NULL
```

### Operadores Lógicos

- Se usan para combinar multiples condiciones en una consulta. Permiten aplicar lógica condicional (como "y","o","no") para filtrar resultados basados en múltiples criterios.

- **Principales Operadores Lógicos en SQL:**

1. `AND` (Y lógico):

- Devuelve **TRUE** si ambas condiciones son verdaderas.
- Cobinar múltiples condiciones en una consulta. Ej:

```sql
SELECT * FROM usuarios
WHERE edad > 26
AND nombre LIKE 'LE%'
```

Devuelve todos los valores mayores a 26 y que el nombre empiece con 'LE'.

2. `OR` (O Lógico):

- Devuelve **TRUE** si alguna de las condiciones es verdadera.

3. `NOT` (Negación Lógica):

- Invierte el resultado de una condición, devolviendo **TRUE** cuando la condición es **FALSE** y viceversa.

- **NOTA**: _En consultas más complejas, es recomendable usar parentisis_:

```sql
SELECT * FROM empleados
WHERE (salario > 2000 OR departamento_id = 3)
AND NOT nombre = 'Carlos';
```

## Sentencia `UPDATE`

- Se utiliza para modificar los datos existentes en una o más filas de una tabla. Puedes actualizar valores de una o más columnas y aplicar condiciones para determinar qué filas se van a modificar.

```sql
UPDATE usuarios
SET correo = "leandro96@gmail.com", direccion = "Solo existo"
WHERE usuario_id = 1;
```

### _NOTAS IMPORTANTES_:

- **Cláusula** `WHERE`: Es muy importante usar la cláusula `WHERE` para evitar modificar todas las filas de la tabla por accidente.

- **Restricciones y llaves foráneas:** Asegurarse de que cualqier modificación NO viole las restricciones de la DB, como llaves foráneas, únicas o cualquier otra restricción.

- **Reversibilidad**: Una vez realizada la sentencia `UPDATE`, no se puede deshacer directamente. Por eso es recomendable realizar **BACKUPS** antes de hacer cambios masivos.

## `DELETE`

- Borrar datos en una o mas filas
- Tambien hay que tener en cuenta usar la cláusula `WHERE` si nó te podes mandar el moco de tu vida :).

```sql
DELETE FROM usuarios WHERE usuario_id = 2;
```

## `TRUNCATE`

- Para reiniciar toda la tabla desde cero (teniendo en cuenta lo id auto incrementables)

```sql
TRUNCATE TABLE usuarios;
```

## Funciones Matemáticas

### Modulo o Residuo de una División

```sql
SELECT MOD(3,2)
```

### Redondeo a +1

```sql
SELECT CEILING(7.1)
```

- Resultado: 8

### Redondeo a -1

```sql
SELECT FLOOR(7.9)
```

- Resultado: 7

### Redondeo a -0.5 o +0.5

```sql
SELECT ROUND(7.5)
```

- Resultado: 8

```sql
SELECT ROUND(7.4999)
```

- Resultado: 7

### Potencia

```sql
SELECT POWER(2,3)
```

- Resultado: 8

### Raiz

```sql
SELECT SQRT(81)
```

## Por qué es importante saber esto?

> Podemos realizar operaciones entre atributos, siempre que tengan el mismo tipo de datos. Por ejemplo, si una tabla de ventas de productos tenemos por un lado el precio de cada producto y la cantidad que se vendio, podemos ahorrarnos algo de logica de programación de nuestro backend y realizar la operacion en nuestra base de datos para calcular las ganancias totales. Ej:

```sql
SELECT nombre, precio, cantidad, (precio * cantidad) AS ganancia
FROM productos;
```

### Funciones de Agrupamiento

- `MAX()` : EL maximo de algo

```sql
SELECT MAX(precio) AS precio_maximo FROM products;
```

- `MIN()` : EL minimo de algo

```sql
SELECT MIN(precio) AS precio_minimo FROM products;
```

- `SUM()` : Sumatoria de todos los datos de un atributo dentro de una tabla

```sql
SELECT SUM(cantidad) AS cantidad_total FROM products;
```

- `AVG()` : Promedio total

```sql
SELECT AVG(Precio) AS promedio_total FROM products;
```

## ``GROUP BY``

> Se utiliza para agrupar filas que tienen valores idénticos en una o más columnas. Luego, se pueden aplicar funciones de agrupamiento como ``COUNT()``, ``SUM()``, etc. Para realizar cálculos sobre cada grupo de datos.

````sql
SELECT nombre, precio, MAX(precio) AS precio_max 
FROM productos 
GROUP BY nombre, precio
````

## ``HAVING``

> Se utiliza para filtrar los resultados de una consulta después de aplicar las funciones de agrupación o agregación en combinación con la cláusula ``GROUP BY``. A diferencia del ``WHERE``, que se usa para filtrar filas antes de la agregación, ``HAVING`` se aplica después de los grupos han sido formados.

````sql
SELECT nombre, precio, MAX(precio) AS precio_max 
FROM productos 
GROUP BY nombre, precio 
HAVING precio_max >= 10000;
````

## ``DISTINCT``

> Se utiliza para eliminar filas duplicadas de los resultados de una consulta, devolviendo solo valores únicos en las columnas especificadas. Es útil cuando deseas obtener una lista de valores distintos sin repetir entradas.

````sql
SELECT DISTINCT nombre 
FROM productos
````

> **Resultado**: Nombre de productos UNICOS.

## ``ORDER BY``

>  Se utiliza para ordenar los resultados de una consulta en función de una o más columnas. Puedes ordenar los resultados en orden **ascendente** ``ASC`` o **descendente** ``DESC``.

````sql
SELECT nombre, precio 
FROM productos 
ORDER BY nombre ASC;
````
- **Resultado**: Tabla con el nombre y precio, Ordenada de forma ascendente por el nomrbre.

> Tambien se puede ordenar segun una condición usando `WHERE` o `HAVING` pero siempre ``ORDER BY``va al final de la consulta sql.

## ``INDEX``

> Un índice en SQL es una estructura de datos que mejora la velocidad de las operaciones de consulta en una tabla. Funciona como un índice en un libro, permitiendo acceder más rápidamente a las filas de una tabla en función de los valores de una o más columnas. Sin embargo, aunque los índices mejoran la lectura de datos, pueden hacer que las operaciones de escritura (inserciones, actualizaciones y eliminaciones) sean más lentas debido a que los índices también deben mantenerse actualizados.

### Tipos de índices

1. Índice Primario ``(PK)``:
- Se crea automáticamente cuando se define una columna como clave primaria.
- Es único y no permite valores nulos.
````sql
CREATE TABLE empleados (
   empleado_id INT PRIMARY KEY,
   nombre VARCHAR(100)
);
````
2. Índice único ``(UQ)``:
- Garantiza que los valores en una columna o conjunto de columnas sean únicos.
- No permite valores duplicados, pero sí permite valores nulos (con algunas excepciones en diferentes SGBD).
````sql
CREATE UNIQUE INDEX idx_nombre_unico
ON empleados(nombre);
````
3. Índice no único **(normal)**:
- Se usa para mejorar el rendimiento de las consultas, pero permite valores duplicados.
````sql
CREATE INDEX idx_nombre
ON empleados(nombre);
````
4. Índice compuesto:
- Se crea en más de una columna para optimizar consultas que involucran múltiples columnas.
- El orden de las columnas en el índice es importante, ya que se optimiza para consultas que utilizan las columnas en ese orden.
````sql
CREATE INDEX idx_nombre_apellido
ON empleados(nombre, apellido);
````
5. Índice de texto completo (Full-text index):
- Se utiliza para optimizar la búsqueda de texto en columnas que contienen grandes volúmenes de texto, como artículos o descripciones.
- Permite realizar búsquedas eficientes sobre texto extenso.
````sql
CREATE FULLTEXT INDEX idx_descripcion
ON productos(descripcion);
````