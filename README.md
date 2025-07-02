
# 📚 Ayuda Memoria SQL

Guía rápida y práctica de comandos SQL comunes para bases de datos, tablas, consultas, inserciones, joins, funciones, vistas y triggers.

---

## Bases de Datos

```sql
CREATE DATABASE nombre_db;
USE nombre_db;
SHOW DATABASES;
DROP DATABASE nombre_db;
```

---

## Tablas

```sql
CREATE TABLE nombre_tabla (
  campo1 TIPO,
  campo2 TIPO
);

SHOW TABLES;
DESCRIBE nombre_tabla;
DROP TABLE nombre_tabla;

ALTER TABLE nombre_tabla ADD nueva_columna TIPO;
ALTER TABLE nombre_tabla MODIFY columna_existente TIPO;
ALTER TABLE nombre_tabla DROP columna_a_eliminar;
RENAME TABLE tabla1 TO tabla2;
```

---

## Tipos de Datos Comunes

| Tipo de Dato   | Descripción                       |
| -------------- | ---------------------------------|
| INT            | Número entero                    |
| DECIMAL(x,y)   | Decimal con precisión            |
| VARCHAR(n)     | Texto variable hasta n caracteres|
| TEXT           | Texto largo                     |
| DATE           | Fecha (YYYY-MM-DD)               |
| DATETIME       | Fecha y hora                    |
| TIME           | Hora (HH:MM:SS)                 |
| BOOLEAN        | Verdadero / Falso (1 o 0)       |

---

## Restricciones (Constraints)

```sql
PRIMARY KEY           -- Clave única e identificadora
AUTO_INCREMENT        -- Incremento automático en campos numéricos
UNIQUE                -- Valores únicos
NOT NULL              -- No acepta valores nulos
DEFAULT valor         -- Valor por defecto
CHECK (condición)     -- Condición para validar valores
FOREIGN KEY (...) REFERENCES otra_tabla(campo)
```

---

## Insertar / Actualizar / Eliminar

```sql
INSERT INTO nombre_tabla (campo1, campo2) VALUES (valor1, valor2);
INSERT INTO nombre_tabla VALUES (v1, v2), (v3, v4);

UPDATE nombre_tabla SET campo = nuevo_valor WHERE condicion;

DELETE FROM nombre_tabla WHERE condicion;
```

---

## Consultas (SELECT)

```sql
SELECT * FROM nombre_tabla;
SELECT campo1, campo2 FROM nombre_tabla;

SELECT * FROM nombre_tabla WHERE campo = valor;
SELECT * FROM nombre_tabla WHERE campo LIKE 'A%';
SELECT * FROM nombre_tabla WHERE campo BETWEEN 10 AND 100;

SELECT * FROM nombre_tabla ORDER BY campo ASC;
SELECT * FROM nombre_tabla LIMIT 10;
```

---

## JOINs (Uniones)

```sql
SELECT * FROM A INNER JOIN B ON A.campo = B.campo;
SELECT * FROM A LEFT JOIN B ON A.campo = B.campo;
SELECT * FROM A RIGHT JOIN B ON A.campo = B.campo;
```

---

## Funciones Agregadas

```sql
SELECT COUNT(*) FROM nombre_tabla;
SELECT SUM(campo) FROM nombre_tabla;
SELECT AVG(campo) FROM nombre_tabla;
SELECT MAX(campo), MIN(campo) FROM nombre_tabla;

SELECT campo, COUNT(*) FROM nombre_tabla GROUP BY campo;
```

---

## Vistas (Views)

```sql
CREATE VIEW nombre_vista AS
SELECT campo1, campo2 FROM nombre_tabla WHERE condicion;

SELECT * FROM nombre_vista;

DROP VIEW nombre_vista;
```

---

## Triggers

```sql
CREATE TRIGGER nombre_trigger
AFTER INSERT ON nombre_tabla
FOR EACH ROW
BEGIN
  -- código SQL aquí
END;

SHOW TRIGGERS;

DROP TRIGGER nombre_trigger;
```

---

## Ejemplo Completo de Tablas Relacionales

```sql
CREATE TABLE clientes (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nombre VARCHAR(100) NOT NULL,
  correo VARCHAR(100) UNIQUE NOT NULL,
  fecha_registro DATE DEFAULT CURRENT_DATE,
  activo BOOLEAN DEFAULT 1
);

CREATE TABLE pedidos (
  id INT PRIMARY KEY AUTO_INCREMENT,
  id_cliente INT NOT NULL,
  fecha_pedido DATETIME DEFAULT CURRENT_TIMESTAMP,
  total DECIMAL(10,2),
  FOREIGN KEY (id_cliente) REFERENCES clientes(id)
);
```
