---
marp: true
paginate: true
theme: dafault
class: invert
script: mermaid
_paginate: &:page
---

# Creación de Diagramas de Modelo Relacional

## ¿Qué es un Diagrama Entidad-Relación (ERD)?

- Representa visualmente la estructura de una base de datos.
- Define entidades, atributos y relaciones.
- Ayuda a diseñar bases de datos normalizadas.

---

# Elementos Claves de un ERD

- **Entidades**: Representan objetos del mundo real (Ej: Clientes, Órdenes).
- **Atributos**: Propiedades de cada entidad (Ej: Nombre, Precio).
- **Relaciones**: Conectan entidades (Ej: Un Cliente realiza Órdenes).
- **Clave Primaria (PK)**: Identificador único de una entidad.
- **Clave Foránea (FK)**: Referencia a otra entidad.

---

# Tipos de Tablas en un Modelo Relacional

## Tablas Principales o Maestras

Almacenan entidades centrales del sistema, como usuarios o productos.

Ejemplo: `usuarios`, `productos`, `ordenes`.

---

## Tablas de Detalle

- Guardan información adicional sobre una entidad principal.
- Se usan en relaciones **uno a muchos (1:N)**.
- Contienen una clave foránea (`FK`) que referencia a la tabla principal.

Ejemplo: `detalle_orden`, que almacena productos dentro de una orden.

```sql
CREATE TABLE detalle_orden (
    id BIGSERIAL PRIMARY KEY,
    orden_id BIGINT NOT NULL REFERENCES ordenes(id) ON DELETE CASCADE,
    producto_id BIGINT NOT NULL REFERENCES productos(id) ON DELETE CASCADE,
    cantidad INT CHECK (cantidad > 0),
    precio_unitario NUMERIC(10,2) NOT NULL
);
```

---

## Tablas Pivote o Intermedias

- Se usan en relaciones **muchos a muchos (M:N)**.
- No contienen información adicional más allá de las claves foráneas.
- Actúan como un puente entre dos tablas principales.

Ejemplo: `usuario_rol`, que conecta usuarios con roles.

```sql
CREATE TABLE usuario_rol (
    usuario_id BIGINT NOT NULL REFERENCES usuarios(id) ON DELETE CASCADE,
    rol_id BIGINT NOT NULL REFERENCES roles(id) ON DELETE CASCADE,
    PRIMARY KEY (usuario_id, rol_id)
);
```

---

# Ejemplo de Diagrama ERD

```mermaid
erDiagram
    USUARIOS {
        BIGINT ID_Usuario PK
        VARCHAR Nombre
        VARCHAR Email UK
        VARCHAR Contrasena
    }
    
    ORDENES {
        BIGINT ID_Orden PK
        BIGINT ID_Usuario FK
        TIMESTAMP Fecha DEFAULT now()
        VARCHAR Estado
    }
    
    PRODUCTOS {
        BIGINT ID_Producto PK
        VARCHAR Nombre
        NUMERIC Precio
    }
    
    DETALLE_ORDEN {
        BIGINT ID_Detalle PK
        BIGINT ID_Orden FK
        BIGINT ID_Producto FK
        INT Cantidad CHECK (Cantidad > 0)
        NUMERIC Precio_Unitario
    }
    
    USUARIOS ||--o{ ORDENES : genera
    ORDENES ||--o{ DETALLE_ORDEN : contiene
    PRODUCTOS ||--o{ DETALLE_ORDEN : incluye
```

---

# Caso Real: Gestión de Órdenes de Compra

## Tablas Principales

### Usuarios

Guarda información de los usuarios que interactúan con el sistema.

```sql
CREATE TABLE usuarios (
    id BIGSERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    contrasena TEXT NOT NULL
);
```

### Órdenes de Compra

Registra las órdenes de compra generadas por los usuarios.

```sql
CREATE TABLE ordenes (
    id BIGSERIAL PRIMARY KEY,
    usuario_id BIGINT NOT NULL REFERENCES usuarios(id) ON DELETE CASCADE,
    fecha TIMESTAMP DEFAULT now(),
    estado VARCHAR(50) NOT NULL
);
```

---

# Tablas de Detalle y Pivote

### Productos

Almacena los productos disponibles para la compra.

```sql
CREATE TABLE productos (
    id BIGSERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    precio NUMERIC(10,2) NOT NULL CHECK (precio >= 0)
);
```

---

### Detalles de Órdenes (Tabla Detalle)

Relaciona las órdenes con los productos y sus cantidades.

```sql
CREATE TABLE detalle_orden (
    id BIGSERIAL PRIMARY KEY,
    orden_id BIGINT NOT NULL REFERENCES ordenes(id) ON DELETE CASCADE,
    producto_id BIGINT NOT NULL REFERENCES productos(id) ON DELETE CASCADE,
    cantidad INT CHECK (cantidad > 0),
    precio_unitario NUMERIC(10,2) NOT NULL
);
```

---

# Beneficios de un ERD

✅ Facilita la comprensión de la base de datos.
✅ Ayuda a evitar redundancia y errores.
✅ Permite una implementación más eficiente en SQL.

---

# Conclusión

- Los diagramas ERD son esenciales para modelar bases de datos.
- Siguiendo buenas prácticas se logra un diseño optimizado y escalable.
- Este modelo permite gestionar órdenes de compra relacionando usuarios, productos y detalles de las órdenes.
- Herramientas como Mermaid permiten una representación clara y efectiva.
