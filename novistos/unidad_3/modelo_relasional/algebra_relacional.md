---
marp: true
paginate: true
theme: dafault
class: invert
script: mermaid
_paginate: &:page
---

# 📊 Introducción al Álgebra Relacional

---

## 📌 ¿Qué es el Álgebra Relacional?

El álgebra relacional es un conjunto de **operaciones matemáticas** que se utilizan para manipular y consultar datos en bases de datos relacionales.

Se basa en la teoría de conjuntos y permite obtener información a partir de tablas (relaciones) mediante operaciones específicas.

---

## 🔄 Operaciones Fundamentales del Álgebra Relacional

El álgebra relacional tiene 5 operaciones fundamentales que permiten extraer, combinar y modificar datos.

### 1️⃣ **Selección (σ)**
- Extrae filas que cumplen una condición específica.
- **Ejemplo:** Obtener todos los pacientes mayores de 30 años.

#### **Tabla Pacientes:**
| id_paciente | nombre | edad | ciudad |
|------------|--------|------|---------|
| 1          | Ana    | 28   | Madrid  |
| 2          | Juan   | 35   | Barcelona |
| 3          | Pedro  | 40   | Valencia  |

**Consulta:**
```
σ_{edad > 30} (Pacientes)
```

**Resultado:**
| id_paciente | nombre | edad | ciudad |
|------------|--------|------|---------|
| 2          | Juan   | 35   | Barcelona |
| 3          | Pedro  | 40   | Valencia  |

---

### 2️⃣ **Proyección (π)**
- Extrae columnas específicas de una tabla.
- **Ejemplo:** Obtener solo los nombres de los pacientes.

**Consulta:**
```
π_{nombre} (Pacientes)
```

**Resultado:**
| nombre  |
|--------|
| Ana    |
| Juan   |
| Pedro  |

---

### 3️⃣ **Unión (∪)**
- Combina los datos de dos tablas con la misma estructura.
- **Ejemplo:** Unir listas de pacientes de dos clínicas.

**Tabla Pacientes_Clinica_A:**
| id_paciente | nombre  |
|------------|--------|
| 1          | Ana    |
| 2          | Juan   |

**Tabla Pacientes_Clinica_B:**
| id_paciente | nombre  |
|------------|--------|
| 3          | Pedro  |
| 4          | Lucia  |

**Consulta:**
```
Pacientes_Clinica_A ∪ Pacientes_Clinica_B
```

**Resultado:**
| id_paciente | nombre  |
|------------|--------|
| 1          | Ana    |
| 2          | Juan   |
| 3          | Pedro  |
| 4          | Lucia  |

---

### 4️⃣ **Diferencia (-)**
- Devuelve los elementos de una tabla que no están en otra.
- **Ejemplo:** Pacientes de la Clínica A que no están en la Clínica B.

**Consulta:**
```
Pacientes_Clinica_A - Pacientes_Clinica_B
```

**Resultado:**
| id_paciente | nombre  |
|------------|--------|
| 1          | Ana    |
| 2          | Juan   |

---

### 5️⃣ **Producto Cartesiano (×)**
- Combina todas las filas de dos tablas.
- **Ejemplo:** Lista de todos los médicos con todos los pacientes.

**Tabla Médicos:**
| id_medico | nombre_medico |
|----------|--------------|
| 101      | Dr. López    |
| 102      | Dr. García   |

**Tabla Pacientes:**
| id_paciente | nombre_paciente |
|------------|----------------|
| 1          | Ana            |
| 2          | Juan           |

**Consulta:**
```
Médicos × Pacientes
```

**Resultado:**
| id_medico | nombre_medico | id_paciente | nombre_paciente |
|----------|--------------|------------|----------------|
| 101      | Dr. López    | 1          | Ana            |
| 101      | Dr. López    | 2          | Juan           |
| 102      | Dr. García   | 1          | Ana            |
| 102      | Dr. García   | 2          | Juan           |

---

## 🔍 Álgebra Relacional Extendida

Además de las operaciones fundamentales, existen algunas extendidas que facilitan consultas más avanzadas.

### 🔗 **Join (⨝) - Combinación de Tablas**
- Une dos tablas relacionadas por un atributo común.
- Ejemplo: Obtener la información del paciente y su consulta médica.

### 🔄 **Intersección (∩)**
- Devuelve los registros que existen en ambas tablas.
- Ejemplo: Pacientes atendidos en dos clínicas diferentes.

### 🔢 **División (÷)**
- Encuentra registros que cumplen una condición en todos los casos.
- Ejemplo: Médicos que han atendido a todos los pacientes de una lista.

### 📊 **Agregación**
- Permite calcular valores como SUMA, PROMEDIO, MÁXIMO, MÍNIMO, etc.
- Ejemplo: Promedio de edad de los pacientes.

---

## 🎯 Conclusión

El álgebra relacional es clave para entender cómo funcionan las bases de datos y cómo recuperar información de manera eficiente.

💡 **Es la base para SQL y los sistemas de bases de datos modernos.**
