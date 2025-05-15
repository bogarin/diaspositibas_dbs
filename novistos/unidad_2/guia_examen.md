---
marp: true
paginate: true
theme: dafault
class: invert
script: mermaid
_paginate: &:page
---

# Ejemplo Completo de Diseño e Implementación de Base de Datos Relacional

---
## 1. Análisis de Requisitos
### Enunciado del problema
Una librería desea llevar el control de sus ventas, productos y clientes. Se requiere almacenar la siguiente información:
- **Clientes** con sus datos personales (nombre, teléfono, email).
- **Productos** con su información (nombre, precio, categoría).
- **Ventas** que relacione clientes con los productos comprados, incluyendo la fecha de la venta y la cantidad adquirida.

---
crear las tablas pertienestes con sus atributos y relaciones.

insertar los valores de cada tabla.

dame select de las tablas involucradas.

dame una consulta agrupada por el nombre del cliente y los productos comprados.

dame  la infromacion de el producto mas vendido.

el producto mas comprado por un cliente


---
## 2. Diseño del Modelo Conceptual
### Diagrama Entidad-Relación (E-R)
- **Entidades:** Cliente, Producto, Venta
- **Relaciones:**
  - Un cliente puede realizar muchas ventas (1:N)
  - Un producto puede estar en muchas ventas (N:M)

**Atributos:**
- Cliente (ID, Nombre, Teléfono, Email)
- Producto (ID, Nombre, Precio, Categoría)
- Venta (ID, Fecha, Cantidad, ClienteID, ProductoID)

---
## 3. Conversión a Esquema Relacional
- **Cliente(ID, Nombre, Teléfono, Email)**
- **Producto(ID, Nombre, Precio, Categoría)**
- **Venta(ID, Fecha, Cantidad, ClienteID [FK], ProductoID [FK])**



---
## 6. Normalización y Cardinalidad
- **1FN:** Cada celda tiene un solo valor. Ejemplo: Cada cliente tiene un solo teléfono por registro.
- **2FN:** Todas las columnas dependen totalmente de la clave primaria. Ejemplo: En la tabla `Venta`, `ClienteID` y `ProductoID` están en claves foráneas que se relacionan adecuadamente.
- **3FN:** No hay dependencias transitivas. Ejemplo: Datos como el teléfono del cliente no dependen de otro atributo distinto del `ID` del cliente.
- **4FN:** Las relaciones multivaloradas están separadas en tablas distintas. Ejemplo: Las ventas se gestionan por separado para cada cliente y producto.
- **5FN:** Se descompone la relación de ventas en tablas que evitan ambigüedades. Ejemplo: La tabla `Venta` gestiona la relación N:M entre clientes y productos.

