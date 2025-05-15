---
marp: true
paginate: true
theme: dafault
class: invert
script: mermaid
_paginate: &:page
---

# Tarea 3 Unidad 2 

## Objetivo

El objetivo de esta tarea es aplicar las fases del diseño de bases de datos para resolver problemas prácticos. Los estudiantes deberán analizar requerimientos, diseñar modelos conceptuales, transformarlos en estructuras lógicas y físicas, e implementar consultas SQL para interactuar con la base de datos.

---

## Instrucciones Generales

A continuación, se detallan los pasos para abordar cada uno de los ejercicios:

1. **Análisis de Requisitos:**

   - Lee con atención el enunciado del problema.
   - Identifica qué información se debe almacenar y gestionar.
   - Define las entidades principales (objetos o conceptos clave) y sus relaciones.

2. **Diseño del Modelo Conceptual:**

   - Dibuja un diagrama Entidad-Relación (E-R) utilizando herramientas como Draw\.io, Lucidchart o papel y lápiz, etc.
   - Asegúrate de incluir las entidades, atributos y su tipo de cardinalidad.

---

3. **Conversión a Esquema Relacional:**

   - Convierte el modelo E-R a un conjunto de tablas.
   - Define las claves primarias y foráneas para relacionar las tablas.

4. **Implementación en SQL:**

   - Utiliza un sistema de gestión de bases de datos (DBMS) como MySQL, PostgreSQL o SQL Server.
   - Crea las tablas utilizando **Lenguaje de Definición de Datos (LDD)** con sentencias como `CREATE TABLE`.
   - Inserta datos de ejemplo usando `INSERT INTO`.

---

5. **Consultas SQL:**

   - Realiza consultas para obtener información útil utilizando **Lenguaje de Manipulación de Datos (LMD)**.
   - Aplica las instrucciones SQL como `SELECT`, `WHERE`, `ORDER BY`, `GROUP BY`, `JOIN` y `LIKE`.

6. **Validación:**

   - Verifica que las consultas devuelvan los resultados esperados.
   - Captura una pantalla del resultado obtenido.

---

7. **Entrega:**

   - Guarda el archivo en formato PDF.
   - Incluye las capturas de pantalla junto con los querys utilizados.
   - Sube el archivo a Git en el repositorio asignado antes de la fecha límite.

---

## Desarrollo

A continuación, se presentan cinco problemas nuevos que el estudiante debe resolver, aplicando todas las fases del diseño de bases de datos:

### **1. Sistema de Gestión de Inventarios**

Una empresa desea controlar su inventario de productos y proveedores.

- Identificar entidades clave: **Producto, Proveedor, Categoría, Inventario**.
- Diseñar el modelo E-R.
- Convertir el modelo a un esquema relacional.
- Implementar la base de datos en SQL.
- **Consulta requerida:** Obtener la lista de productos con sus respectivas categorías y proveedores, ordenados alfabéticamente por nombre de producto.

---

### **2. Sistema de Gestión de Eventos**

Una empresa de organización de eventos necesita administrar sus eventos y participantes.

- Definir entidades clave: **Evento, Participante, Ubicación, Organizador**.
- Diseñar el diagrama E-R.
- Crear el esquema relacional.
- Implementar la base de datos.
- **Consulta requerida:** Obtener la lista de eventos programados junto con la cantidad de participantes registrados por evento.

---

### **3. Plataforma de Streaming de Música**

Se desea un sistema para administrar usuarios, artistas y sus canciones.

- Identificar entidades clave: **Usuario, Artista, Álbum, Canción**.
- Diseñar un modelo E-R.
- Transformarlo en un esquema relacional.
- Implementar la base de datos.
- **Consulta requerida:** Listar las canciones reproducidas por un usuario específico, incluyendo el nombre del artista y del álbum.

---

### **4. Sistema de Control de Proyectos**

Una empresa desea hacer seguimiento de sus proyectos y tareas.

- Definir entidades clave: **Proyecto, Empleado, Tarea**.
- Diseñar el diagrama E-R.
- Transformarlo en tablas relacionales.
- Implementar la base de datos.
- **Consulta requerida:** Mostrar todas las tareas pendientes de un proyecto específico, ordenadas por fecha de vencimiento.

---

### **5. Sistema de Evaluación Académica**

Una institución educativa necesita administrar las calificaciones de los estudiantes.

- Identificar entidades clave: **Estudiante, Curso, Profesor, Calificación**.
- Elaborar el modelo E-R.
- Convertirlo a un esquema relacional.
- Implementar la base de datos.
- **Consulta requerida:** Obtener el promedio de calificaciones de un estudiante en todos sus cursos.

---

## Requisitos de Entrega

- El archivo debe entregarse en formato **PDF**.
- La nomenclatura del archivo debe seguir el siguiente formato:

  donde `#n` es el número de la tarea y `num_control` es el número de control del estudiante.
- Subir el archivo a Git en el repositorio correspondiente.
- Fecha límite de entrega: **24 de marzo antes de las 19:59 hrs**.