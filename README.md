
# 📚 Ayuda Memoria SQL con Explicaciones

Guía rápida con sintaxis y para qué sirve cada comando o concepto.

---

## Bases de Datos

```sql
CREATE DATABASE nombre_db;
```
*Crear una base de datos nueva llamada `nombre_db`.*

```sql
USE nombre_db;
```
*Seleccionar la base de datos `nombre_db` para trabajar con ella.*

```sql
SHOW DATABASES;
```
*Listar todas las bases de datos existentes en el servidor.*

```sql
DROP DATABASE nombre_db;
```
*Eliminar la base de datos llamada `nombre_db` y todo su contenido.*

---

## Tablas

```sql
CREATE TABLE nombre_tabla (
  campo1 TIPO,
  campo2 TIPO
);
```
*Crear una tabla nueva con los campos y tipos especificados.*

```sql
SHOW TABLES;
```
*Mostrar todas las tablas existentes en la base de datos seleccionada.*

```sql
DESCRIBE nombre_tabla;
```
*Mostrar la estructura (campos, tipos, claves) de la tabla.*

```sql
DROP TABLE nombre_tabla;
```
*Eliminar la tabla `nombre_tabla` y todos sus datos.*

```sql
ALTER TABLE nombre_tabla ADD nueva_columna TIPO;
```
*Agregar una nueva columna a la tabla existente.*

```sql
ALTER TABLE nombre_tabla MODIFY columna_existente TIPO;
```
*Modificar el tipo o características de una columna existente.*

```sql
ALTER TABLE nombre_tabla DROP columna_a_eliminar;
```
*Eliminar una columna de la tabla.*

```sql
RENAME TABLE tabla1 TO tabla2;
```
*Renombrar la tabla `tabla1` a `tabla2`.*

---

## Tipos de Datos Comunes

| Tipo de Dato   | Descripción                       |
| -------------- | ---------------------------------|
| INT            | Número entero                    |
| DECIMAL(x,y)   | Número decimal con precisión    |
| VARCHAR(n)     | Texto variable hasta n caracteres|
| TEXT           | Texto largo                     |
| DATE           | Fecha (AAAA-MM-DD)               |
| DATETIME       | Fecha y hora                   |
| TIME           | Hora (HH:MM:SS)                |
| BOOLEAN        | Valor verdadero/falso (1 o 0)   |

---

## Restricciones (Constraints)

```sql
PRIMARY KEY
```
*Define un campo o conjunto de campos que identifican un registro de forma única.*

```sql
AUTO_INCREMENT
```
*Hace que un campo numérico se incremente automáticamente al insertar registros nuevos.*

```sql
UNIQUE
```
*Indica que los valores de una columna deben ser únicos en la tabla.*

```sql
NOT NULL
```
*Impide que un campo quede vacío (no acepta valores NULL).*

```sql
DEFAULT valor
```
*Establece un valor por defecto si no se especifica otro al insertar.*

```sql
CHECK (condición)
```
*Valida que los datos cumplan una condición lógica.*

```sql
FOREIGN KEY (...) REFERENCES otra_tabla(campo)
```
*Establece una relación de integridad referencial entre tablas.*

---

## Insertar / Actualizar / Eliminar

```sql
INSERT INTO nombre_tabla (campo1, campo2) VALUES (valor1, valor2);
```
*Insertar un nuevo registro con los valores indicados.*

```sql
INSERT INTO nombre_tabla VALUES (v1, v2), (v3, v4);
```
*Insertar varios registros a la vez.*

```sql
UPDATE nombre_tabla SET campo = nuevo_valor WHERE condicion;
```
*Modificar los valores de uno o varios registros que cumplan la condición.*

```sql
DELETE FROM nombre_tabla WHERE condicion;
```
*Eliminar uno o varios registros según la condición.*

---

## Consultas (SELECT)

```sql
SELECT * FROM nombre_tabla;
```
*Obtener todos los registros y campos de la tabla.*

```sql
SELECT campo1, campo2 FROM nombre_tabla;
```
*Obtener sólo los campos especificados de todos los registros.*

```sql
SELECT * FROM nombre_tabla WHERE campo = valor;
```
*Obtener registros que cumplan una condición.*

```sql
SELECT * FROM nombre_tabla WHERE campo LIKE 'A%';
```
*Buscar registros donde el campo comienza con 'A' (comodín).*

```sql
SELECT * FROM nombre_tabla WHERE campo BETWEEN 10 AND 100;
```
*Buscar registros cuyo campo está en un rango.*

```sql
SELECT * FROM nombre_tabla ORDER BY campo ASC;
```
*Ordenar los resultados por un campo en forma ascendente.*

```sql
SELECT * FROM nombre_tabla LIMIT 10;
```
*Limitar el número de resultados a 10.*

---

## JOINs (Uniones)

```sql
SELECT * FROM A INNER JOIN B ON A.campo = B.campo;
```
*Devuelve registros que tienen coincidencias en ambas tablas.*

```sql
SELECT * FROM A LEFT JOIN B ON A.campo = B.campo;
```
*Devuelve todos los registros de A y los coincidentes de B (si no hay, muestra NULL).*

```sql
SELECT * FROM A RIGHT JOIN B ON A.campo = B.campo;
```
*Devuelve todos los registros de B y los coincidentes de A.*

---

## Funciones Agregadas

```sql
SELECT COUNT(*) FROM nombre_tabla;
```
*Cuenta la cantidad de registros.*

```sql
SELECT SUM(campo) FROM nombre_tabla;
```
*Calcula la suma de los valores de un campo numérico.*

```sql
SELECT AVG(campo) FROM nombre_tabla;
```
*Calcula el promedio de los valores de un campo.*

```sql
SELECT MAX(campo), MIN(campo) FROM nombre_tabla;
```
*Obtiene el valor máximo y mínimo de un campo.*

```sql
SELECT campo, COUNT(*) FROM nombre_tabla GROUP BY campo;
```
*Agrupa registros por un campo y cuenta registros por grupo.*

---

## Vistas (Views)

```sql
CREATE VIEW nombre_vista AS
SELECT campo1, campo2 FROM nombre_tabla WHERE condicion;
```
*Crea una vista (consulta guardada) con un nombre para usarla fácilmente.*

```sql
SELECT * FROM nombre_vista;
```
*Consulta datos desde la vista.*

```sql
DROP VIEW nombre_vista;
```
*Elimina la vista.*

---

## Triggers

```sql
CREATE TRIGGER nombre_trigger
AFTER INSERT ON nombre_tabla
FOR EACH ROW
BEGIN
  -- código SQL que se ejecuta tras insertar un registro
END;
```
*Define una acción automática que se ejecuta tras un evento (insert, update, delete).*

```sql
SHOW TRIGGERS;
```
*Lista todos los triggers existentes.*

```sql
DROP TRIGGER nombre_trigger;
```
*Elimina un trigger.*

---

## Ejemplo Completo

```sql
-- Crear tabla clientes
CREATE TABLE clientes (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nombre VARCHAR(100) NOT NULL,
  correo VARCHAR(100) UNIQUE NOT NULL,
  fecha_registro DATE DEFAULT CURRENT_DATE,
  activo BOOLEAN DEFAULT 1
);

-- Crear tabla pedidos
CREATE TABLE pedidos (
  id INT PRIMARY KEY AUTO_INCREMENT,
  id_cliente INT NOT NULL,
  fecha_pedido DATETIME DEFAULT CURRENT_TIMESTAMP,
  total DECIMAL(10,2),
  estado VARCHAR(20) DEFAULT 'pendiente',
  FOREIGN KEY (id_cliente) REFERENCES clientes(id)
);

-- Insertar datos en clientes
INSERT INTO clientes (nombre, correo) VALUES
('Juan Perez', 'juan@example.com'),
('Ana Gómez', 'ana@example.com');

-- Insertar datos en pedidos
INSERT INTO pedidos (id_cliente, total) VALUES
(1, 150.00),
(1, 300.50),
(2, 120.75);

-- Consultar todos los clientes activos
SELECT * FROM clientes WHERE activo = 1;

-- Consultar pedidos con datos del cliente (JOIN)
SELECT p.id, c.nombre, p.fecha_pedido, p.total, p.estado
FROM pedidos p
INNER JOIN clientes c ON p.id_cliente = c.id;

-- Actualizar estado de un pedido
UPDATE pedidos SET estado = 'completado' WHERE id = 2;

-- Borrar cliente y sus pedidos (asegúrate que se manejen las FK o usar transacción)
DELETE FROM pedidos WHERE id_cliente = 2;
DELETE FROM clientes WHERE id = 2;

-- Crear una vista con pedidos pendientes
CREATE VIEW pedidos_pendientes AS
SELECT p.id, c.nombre, p.fecha_pedido, p.total
FROM pedidos p
JOIN clientes c ON p.id_cliente = c.id
WHERE p.estado = 'pendiente';

-- Consultar la vista
SELECT * FROM pedidos_pendientes;

-- Crear trigger para actualizar fecha de registro al modificar cliente
CREATE TRIGGER actualiza_fecha_registro
BEFORE UPDATE ON clientes
FOR EACH ROW
BEGIN
  SET NEW.fecha_registro = CURRENT_DATE;
END;
```

