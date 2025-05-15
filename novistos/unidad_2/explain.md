---
marp: true
paginate: true
theme: default
class: invert
---

# Comprendiendo `EXPLAIN ANALYZE` en PostgreSQL  

### Guía para leer y entender un plan de ejecución

---

## ¿Qué es `EXPLAIN ANALYZE`?

`EXPLAIN ANALYZE` es un comando de PostgreSQL que ejecuta una consulta y devuelve información detallada sobre cómo el motor de la base de datos la ejecuta.

**Ejemplo:**
```sql
EXPLAIN ANALYZE SELECT * FROM usuarios WHERE edad > 30;
```

Este comando proporciona un "plan de ejecución", que describe los pasos que PostgreSQL sigue para obtener los datos.

---

## Concepto de Árbol de Ejecución

El resultado de `EXPLAIN ANALYZE` se representa como un árbol. Cada nodo representa una operación ejecutada en la consulta. La ejecución empieza en los nodos más internos y progresa hacia arriba.

---

**Ejemplo de estructura de árbol:**
```
Seq Scan on usuarios (cost=0.00..12.34 rows=5 width=64)
  -> Filter: (edad > 30)
```

Cada nodo muestra:
- **Tipo de escaneo (Seq Scan, Index Scan, etc.)**
- **Costo estimado**
- **Número de filas estimadas y reales**
- **Tiempo de ejecución**

---

## Explicación de los Tiempos de Ejecución

Los tiempos de ejecución en `EXPLAIN ANALYZE` están expresados en **milisegundos (ms)**.

### **Ejemplo de salida con tiempos:**
```
Seq Scan on usuarios  (cost=0.00..12.34 rows=5 width=64) (actual time=0.021..0.035 rows=5 loops=1)
```

**Desglose:**
- **`actual time=0.021..0.035`**:
  - `0.021 ms`: Tiempo en que el nodo comenzó a ejecutarse.
  - `0.035 ms`: Tiempo total hasta que el nodo finalizó.
- **Diferencia (`0.035 - 0.021`)**: Indica el tiempo total de ejecución en milisegundos.

Si el valor es muy alto, se puede convertir a segundos dividiendo entre **1000**.

---

Ejemplo:
```
(actual time=1245.678..1299.345)
```
Tiempo total: **1299.345 - 1245.678 = 53.667 ms** → **0.053 segundos**.

---

## Tipos de Operaciones en `EXPLAIN ANALYZE`

### 1. Sequential Scan (`Seq Scan`)
Recorre todas las filas de una tabla.

```sql
EXPLAIN ANALYZE SELECT * FROM usuarios;
```

**Ejemplo de salida:**
```
Seq Scan on usuarios (cost=0.00..12.34 rows=5 width=64)
```

---


### 2. Index Scan (`Index Scan`)
Usa un índice para buscar datos más rápido.

```sql
EXPLAIN ANALYZE SELECT * FROM usuarios WHERE id = 5;
```

Salida:
```
Index Scan using idx_usuarios_id on usuarios (cost=0.15..8.20 rows=1 width=64)
```

---

## Ejemplo 1: Escaneo Secuencial vs Índice

```sql
EXPLAIN ANALYZE SELECT * FROM empleados WHERE salario > 50000;
```

Si la tabla no tiene un índice, veremos un **Seq Scan**. Si hay un índice, PostgreSQL usará un **Index Scan**.

```sql
CREATE INDEX idx_salario ON empleados(salario);
```

---

## Ejemplo 2: Uso de Hash Join

Los Hash Joins se usan para combinar grandes volúmenes de datos eficientemente.

```sql
EXPLAIN ANALYZE 
SELECT * 
FROM pedidos p 
JOIN clientes c ON p.cliente_id = c.id;
```

Salida típica:
```
Hash Join  (cost=45.00..110.00 rows=1000 width=128)
  -> Seq Scan on pedidos p
  -> Hash
      -> Seq Scan on clientes c
```

---

## Ejemplo 3: Uso de Sort

El operador **Sort** se usa cuando PostgreSQL necesita ordenar los datos antes de devolverlos.

```sql
EXPLAIN ANALYZE SELECT * FROM productos ORDER BY precio DESC;
```

Salida típica:
```
Sort (cost=20.00..30.00 rows=500 width=64)
  -> Seq Scan on productos
```

Si `productos.precio` tiene un índice, PostgreSQL puede usar **Index Scan** en lugar de **Sort**, mejorando el rendimiento.

```sql
CREATE INDEX idx_precio ON productos(precio);
```

---

## Comandos Equivalentes en Otros Motores de BD

| Motor de BD     | Comando equivalente a `EXPLAIN ANALYZE` |
|----------------|-----------------------------------------|
| **MySQL**      | `EXPLAIN ANALYZE SELECT ...;` *(Desde MySQL 8.0.18+)* |
| **MariaDB**    | `EXPLAIN FORMAT=JSON SELECT ...;` |
| **SQL Server** | `SET STATISTICS IO, TIME ON;` seguido de la consulta |

---

| Motor de BD     | Comando equivalente a `EXPLAIN ANALYZE` |
|----------------|-----------------------------------------|
| **Oracle**     | `EXPLAIN PLAN FOR SELECT ...;` y luego `SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY);` |
| **SQLite**     | `EXPLAIN QUERY PLAN SELECT ...;` |
| **IBM Db2**    | `EXPLAIN PLAN FOR SELECT ...;` y luego consultar `EXPLAIN_STATEMENT` |
| **Informix**   | `SET EXPLAIN ON;` antes de ejecutar la consulta |

---

## Resumen

- `EXPLAIN ANALYZE` permite analizar el rendimiento de las consultas.
- Los **árboles de ejecución** muestran cómo PostgreSQL obtiene los datos.
- **Seq Scan** y **Index Scan** son estrategias de búsqueda.
- **Hash Join** optimiza combinaciones grandes de datos.
- **Sort** se usa cuando se requiere ordenar resultados.
- **Los tiempos de ejecución están en milisegundos (ms).**
- **Si el tiempo es alto, se puede convertir a segundos dividiendo entre 1000.**
- **Otros motores de BD tienen comandos similares para analizar consultas.**

### ¡Optimiza tus consultas con `EXPLAIN ANALYZE`!
