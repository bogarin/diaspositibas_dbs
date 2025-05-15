---
marp: true
paginate: true
theme: dafault
class: invert
script: mermaid
_paginate: &:page
---

# 📊 Introducción al Modelo Relacional

---

## 📌 ¿Qué es el Modelo Relacional?

El modelo relacional es un método para organizar y estructurar datos en una base de datos. Utiliza **tablas** para representar la información y las relaciones entre los datos.

**Ejemplo:**

- Una tabla "Pacientes" puede contener información como Nombre, Edad y Dirección.
- Una tabla "Consultas" puede almacenar la fecha, el médico y el paciente atendido.

Las tablas se relacionan mediante **claves**.

---

## 🔄 Conversión de Modelo E-R a Modelo Relacional

El **Modelo Entidad-Relación (E-R)** es una representación gráfica de los datos antes de convertirlos en tablas.

### Pasos para la conversión

1. **Entidades → Tablas**
2. **Atributos → Columnas**
3. **Identificadores → Claves primarias**
4. **Relaciones → Claves foráneas**

Ejemplo:

- Entidad "Paciente" ➝ Tabla "Pacientes"
- Relación "Tiene" entre "Pacientes" y "Consultas" ➝ Clave foránea en "Consultas"

---

## 📋 Esquema de la Base de Datos

El **esquema** de una base de datos define la estructura de sus tablas y relaciones.

Ejemplo de esquema para un consultorio médico:

| Pacientes | Consultas |
|-----------|----------|
| id_paciente (PK) | id_consulta (PK) |
| nombre | fecha |
| edad | id_paciente (FK) |

**PK = Primary Key (Clave Primaria)**
**FK = Foreign Key (Clave Foránea)**

---

## 🔒 Restricciones en el Modelo Relacional

Las restricciones garantizan que los datos sean consistentes y correctos.

### ✅ Integridad de Entidad

- Cada tabla debe tener una clave primaria única.
- Evita registros duplicados o sin identificador.

### 🔄 Integridad Referencial

- Garantiza que las relaciones entre tablas sean correctas.
- Ejemplo: No se puede registrar una consulta con un paciente que no existe.

### 🏷️ Integridad de Dominio

- Asegura que los datos ingresados sean válidos.
- Ejemplo: Un campo "Edad" solo debe permitir valores numéricos positivos.
