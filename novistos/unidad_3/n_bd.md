---
marp: true
paginate: true
theme: dafault
class: invert
script: mermaid
_paginate: &:page
---

# Normalización de Bases de Datos

## 4.1 Conceptos Básicos

La normalización es el proceso de organizar los datos en una base de datos para reducir la redundancia y mejorar la integridad de los datos.

### Objetivos de la Normalización:

- Eliminar redundancias.
- Minimizar anomalías en la manipulación de datos.
- Garantizar la integridad de los datos.

---

## 4.2 Primera Forma Normal (1FN)

Una tabla está en 1FN si:
- Todos los atributos contienen valores atómicos (no multivaluados ni compuestos).
- Tiene una clave primaria definida.
- No hay duplicación de filas.

Ejemplo de violación de 1FN:

```sql
CREATE TABLE Contactos (
    ID SERIAL PRIMARY KEY,
    Nombre VARCHAR(100),
    Telefonos TEXT -- No atómico
);
```
---

**Estructura incorrecta:**

```
+----+--------+------------+
| ID | Nombre | Telefonos  |
+----+--------+------------+
|  1 | Juan   | 123, 456   |
|  2 | Pedro  | 789        |
+----+--------+------------+
```

---

Solución en 1FN:

```sql
CREATE TABLE Contactos (
    ID SERIAL,
    Nombre VARCHAR(100),
    Telefono VARCHAR(20),
    PRIMARY KEY (ID, Telefono)
);
```

**Estructura correcta:**

```
+----+--------+----------+
| ID | Nombre | Telefono |
+----+--------+----------+
|  1 | Juan   | 123      |
|  1 | Juan   | 456      |
|  2 | Pedro  | 789      |
+----+--------+----------+
```

---

## 4.3 Dependencias Funcionales y Transitivas

Ejemplo:

```sql
CREATE TABLE Empleados (
    ID SERIAL PRIMARY KEY,
    Nombre VARCHAR(100),
    Departamento VARCHAR(100),
    Ubicacion VARCHAR(100) -- Dependencia transitiva
);
```

---

**Estructura incorrecta:**

```
+----+--------+-------------+-----------+
| ID | Nombre | Departamento| Ubicación |
+----+--------+-------------+-----------+
|  1 | Juan   | Ventas      | Edificio A|
|  2 | Ana    | Finanzas    | Edificio B|
+----+--------+-------------+-----------+
```

---


Solución:

```sql
CREATE TABLE Departamentos (
    ID SERIAL PRIMARY KEY,
    Nombre VARCHAR(100),
    Ubicacion VARCHAR(100)
);

CREATE TABLE Empleados (
    ID SERIAL PRIMARY KEY,
    Nombre VARCHAR(100),
    ID_Departamento INT,
    FOREIGN KEY (ID_Departamento) REFERENCES Departamentos(ID)
);
```

---

**Estructura correcta:**

```
Tabla Empleados:
+----+--------+----------------+
| ID | Nombre | ID_Departamento|
+----+--------+----------------+
|  1 | Juan   | 10             |
|  2 | Ana    | 20             |
+----+--------+----------------+

Tabla Departamentos:
+----+-------------+-----------+
| ID | Nombre     | Ubicación |
+----+-------------+-----------+
| 10 | Ventas     | Edificio A|
| 20 | Finanzas   | Edificio B|
+----+-------------+-----------+
```

---

## 4.4 Segunda Forma Normal (2FN)

Ejemplo:

```sql
CREATE TABLE Productos (
    ID_Producto SERIAL,
    ID_Proveedor VARCHAR(10),
    Nombre_Producto VARCHAR(100),
    Nombre_Proveedor VARCHAR(100),
    PRIMARY KEY (ID_Producto, ID_Proveedor)
);
```
---

Solución:

```sql
CREATE TABLE Productos (
    ID SERIAL PRIMARY KEY,
    Nombre VARCHAR(100)
);

CREATE TABLE Proveedores (
    ID SERIAL PRIMARY KEY,
    Nombre VARCHAR(100)
);

CREATE TABLE Producto_Proveedor (
    ID_Producto INT,
    ID_Proveedor INT,
    PRIMARY KEY (ID_Producto, ID_Proveedor),
    FOREIGN KEY (ID_Producto) REFERENCES Productos(ID),
    FOREIGN KEY (ID_Proveedor) REFERENCES Proveedores(ID)
);
```

---

## 4.5 Tercera Forma Normal (3FN)

Ejemplo antes de 3FN:

```sql
CREATE TABLE Empleados (
    ID SERIAL PRIMARY KEY,
    Nombre VARCHAR(100),
    ID_Departamento INT,
    Departamento VARCHAR(100),
    Ubicacion VARCHAR(100)
);
```
---

Solución:

```sql
CREATE TABLE Departamentos (
    ID SERIAL PRIMARY KEY,
    Nombre VARCHAR(100),
    Ubicacion VARCHAR(100)
);

CREATE TABLE Empleados (
    ID SERIAL PRIMARY KEY,
    Nombre VARCHAR(100),
    ID_Departamento INT,
    FOREIGN KEY (ID_Departamento) REFERENCES Departamentos(ID)
);
```

---

## 4.6 Forma Normal de Boyce-Codd (BCNF)

Ejemplo de problema en 3FN:

```sql
CREATE TABLE Cursos (
    Curso VARCHAR(100),
    Profesor VARCHAR(100),
    Aula VARCHAR(10),
    PRIMARY KEY (Curso, Profesor)
);
```
---

Solución:

```sql
CREATE TABLE Profesores (
    ID SERIAL PRIMARY KEY,
    Nombre VARCHAR(100)
);

CREATE TABLE Cursos (
    ID SERIAL PRIMARY KEY,
    Nombre VARCHAR(100)
);

CREATE TABLE Aula_Curso (
    ID_Curso INT,
    Aula VARCHAR(10),
    PRIMARY KEY (ID_Curso, Aula),
    FOREIGN KEY (ID_Curso) REFERENCES Cursos(ID)
);

CREATE TABLE Curso_Profesor (
    ID_Curso INT,
    ID_Profesor INT,
    PRIMARY KEY (ID_Curso, ID_Profesor),
    FOREIGN KEY (ID_Curso) REFERENCES Cursos(ID),
    FOREIGN KEY (ID_Profesor) REFERENCES Profesores(ID)
);
```

