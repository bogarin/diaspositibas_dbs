---
marp: true
paginate: true
theme: dafault
class: invert
script: mermaid
_paginate: &:page
---

# Tarea Unidad 2

## Objetivo

El objetivo de esta tarea es aplicar las fases del diseño de bases de datos para resolver problemas prácticos. Los estudiantes deberán analizar requerimientos, diseñar modelos conceptuales, transformarlos en estructuras lógicas y físicas, e implementar consultas SQL para interactuar con la base de datos.

---

## Instrucciones Generales

- Analizar los requerimientos de cada problema y definir los datos esenciales.
- Diseñar un modelo Entidad-Relación (E-R) para representar los datos de forma visual.
- Convertir el modelo conceptual en un esquema relacional.
- Implementar la base de datos en un DBMS utilizando sentencias SQL.
- Aplicar Lenguaje de Definición de Datos (LDD) y Lenguaje de Manipulación de Datos (LMD) para definir y gestionar la información.
- Asegurar que la solución siga buenas prácticas de diseño y normalización de bases de datos.
- Subir el archivo en el formato especificado a Git antes de la fecha límite.

---

- crear las consultas pertienes con  las instrucciones  vistas en clases generales ( `INSERT INTO`,`SELECT` con `WHERE`, `ORDER BY`, `GROUP BY`,`JOIN`,`LIKE`).
- ada ejemplo tiene una consulta propia que hacer.
- guardar los querys en el documento y captura de pantalla de los resultados obtenidos visualizándose la consulta y el resultado.

---

## Desarrollo

A continuación, se presentan los cinco problemas que el estudiante debe resolver, aplicando todas las fases del diseño de bases de datos:

### **1. Sistema de Gestión de Hospitales**

Un hospital necesita gestionar información de pacientes, médicos y citas médicas.

- Identificar entidades clave: **Paciente, Médico, Cita, Tratamiento**.
- Diseñar el modelo E-R con sus relaciones y atributos principales.
- Transformar el modelo en un esquema relacional con claves primarias y foráneas.
- Implementar la base de datos en SQL mediante sentencias LDD.
- Usar LMD para insertar datos y consultar las citas de un paciente específico.

---

### **2. Tienda en Línea**

Una empresa quiere mejorar la administración de sus pedidos en línea.

- Definir entidades: **Cliente, Producto, Pedido, DetallePedido**.
- Crear el diagrama E-R que refleje las relaciones entre las entidades.
- Convertir el modelo en un esquema de tablas relacionales.
- Implementar la base de datos en SQL con restricciones de integridad.
- Consultar los productos comprados por un cliente específico usando SQL.

---

### **3. Biblioteca Digital**

Se requiere un sistema para administrar préstamos de libros en una biblioteca digital.

- Identificar entidades clave: **Usuario, Libro, Préstamo**.
- Diseñar el modelo E-R que represente los préstamos y relaciones.
- Transformar el modelo en un conjunto de tablas relacionales.
- Implementar la base de datos en un DBMS.
- Realizar consultas SQL para obtener los préstamos activos de un usuario.

---

### **4. Sistema de Recursos Humanos**

Una empresa necesita gestionar sus empleados y departamentos.

- Definir entidades: **Empleado, Departamento, Empresa**.
- Elaborar el diagrama E-R que represente la estructura organizacional.
- Transformar el modelo en un esquema relacional.
- Implementar la base de datos en SQL, asegurando la integridad referencial.
- Consultar empleados por departamento mediante sentencias SQL.

---

### **5. Plataforma de Cursos en Línea**

Se requiere un sistema para gestionar la inscripción de usuarios en cursos en línea.

- Identificar entidades clave: **Usuario, Curso, Inscripción**.
- Diseñar un modelo E-R para representar la relación entre usuarios y cursos.
- Convertir el modelo en un conjunto de tablas con relaciones adecuadas.
- Implementar la base de datos en SQL con restricciones adecuadas.
- Consultar los cursos inscritos por un usuario en la base de datos.

---

## Requisitos de Entrega

- El archivo debe entregarse en formato **PDF**.
- La nomenclatura del archivo debe seguir el siguiente formato:

  ```text
  U2_Tarea#n_num_control.pdf
  ```

  donde `#n` es el número de la tarea y `num_control` es el número de control del estudiante.
- Subir el archivo a Git en el repositorio correspondiente.
- Fecha límite de entrega: **18 de marzo antes de las 19:59 hrs**