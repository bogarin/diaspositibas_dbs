---
marp: true
theme: default
class: invert
paginate: true
---

# Creación de Diagramas de Modelo Relacional

## ¿Qué es un Diagrama Entidad-Relación (ERD)?

- Representa visualmente la estructura de una base de datos.
- Define entidades, atributos y relaciones.
- Ayuda a diseñar bases de datos normalizadas.

---

## Elementos Claves de un ERD

- **Entidades**: Representan objetos del mundo real (Ej: Clientes, Reservas).
- **Atributos**: Propiedades de cada entidad (Ej: Nombre, Correo Electrónico).
- **Relaciones**: Conectan entidades (Ej: Un Cliente realiza Reservas).
- **Clave Primaria (PK)**: Identificador único de una entidad.
- **Clave Foránea (FK)**: Referencia a otra entidad.

---

## Ejemplo de Diagrama ERD

---

```mermaid
erDiagram
    CLIENTES {
        INT ID_Cliente PK
        VARCHAR Nombre
        VARCHAR Correo_Electronico UK
        VARCHAR Telefono
        TEXT Direccion
    }
    
    HABITACIONES {
        INT ID_Habitacion PK
        VARCHAR Tipo_Habitacion
        DECIMAL Precio_Noche
        STRING Estado
    }
    
    RESERVAS {
        INT ID_Reserva PK
        INT ID_Cliente FK
        INT ID_Habitacion FK
        DATE Fecha_Checkin
        DATE Fecha_Checkout
        STRING Estado_Reserva
    }
    
    PAGOS {
        INT ID_Pago PK
        INT ID_Reserva FK
        STRING Metodo_Pago
        DECIMAL Monto_Pagado
        DATE Fecha_Pago
        STRING Estado_Pago
    }
    
    CLIENTES ||--o{ RESERVAS : realiza
    HABITACIONES ||--o{ RESERVAS : asignada
    RESERVAS ||--o{ PAGOS : asociado
```
---

![width:35% bg](../imagenes/m_db1.png)

---

## Explicación del Ejemplo

1. **Clientes** pueden realizar múltiples **Reservas**.
2. Cada **Reserva** está asociada a una **Habitación**.
3. Cada **Reserva** tiene un **Pago** asociado.
4. Las claves primarias (PK) identifican registros únicos.
5. Las claves foráneas (FK) mantienen la integridad referencial.

---

## Beneficios de un ERD

✅ Facilita la comprensión de la base de datos.
✅ Ayuda a evitar redundancia y errores.
✅ Permite una implementación más eficiente en SQL.

---

## Conclusión

- Los diagramas ERD son esenciales para modelar bases de datos.
- Siguiendo buenas prácticas se logra un diseño optimizado y escalable.
- Herramientas como Mermaid permiten una representación clara y efectiva.

