---
marp: true
paginate: true
theme: uncover
class: invert
---
# Base de Datos de Prueba en PostgreSQL

Presentación paso a paso para:

1. Crear base de datos
2. Definir tablas relacionadas
3. Realizar respaldos de esquema y datos

---

## 1. Crear la Base de Datos

```sql
-- Crear la base de datos de prueba
CREATE DATABASE prueba_db;
```

- **CREATE DATABASE**: genera una nueva base de datos
- Asegúrate de tener permisos de creación

---

## 2. Conectar a la Base de Datos

```sql
\c prueba_db;
```

- **\c**: comando de 
  -psql para cambiar de conexión
- Opera dentro del cliente psql

---

## 3. Crear Tabla de Clientes

```sql
CREATE TABLE clientes (
  id SERIAL PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  email VARCHAR(100) UNIQUE NOT NULL
);
```

- **SERIAL**: entero autoincremental
- **PRIMARY KEY**: clave primaria única
- **UNIQUE NOT NULL**: el email debe existir y ser único

---

## 4. Crear Tabla de Productos

```sql
CREATE TABLE productos (
  id SERIAL PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  precio NUMERIC(10,2) NOT NULL
);
```

- **NUMERIC(10,2)**: números decimales con 2 dígitos de precisión

---

## 5. Crear Tabla de Pedidos con Relaciones

```sql
CREATE TABLE pedidos (
  id SERIAL PRIMARY KEY,
  cliente_id INTEGER NOT NULL REFERENCES clientes(id),
  producto_id INTEGER NOT NULL REFERENCES productos(id),
  cantidad INTEGER NOT NULL CHECK (cantidad > 0),
  fecha TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

- **FOREIGN KEY**: relaciona `cliente_id` con `clientes(id)` y `producto_id` con `productos(id)`
- **CHECK**: validación de `cantidad > 0`
- **DEFAULT CURRENT_TIMESTAMP**: registra fecha/hora automáticamente

---

## 6. Respaldo de Esquema

Para exportar solo la **estructura** (tablas, índices, restricciones):

```bash
pg_dump -U <usuario> -h <host> -s \
  -f respaldo_esquema.sql prueba_db
```

- `-s` / `--schema-only`: esquema
- `-f`: archivo de salida

---

## 7. Respaldo de Datos

Para exportar solo los **datos** (población de tablas):

```bash
pg_dump -U <usuario> -h <host> -a \
  -f respaldo_datos.sql prueba_db
```

- `-a` / `--data-only`: datos
- `-f`: archivo de salida

---

## 8. Restauración Rápida

- Restaurar esquema:
  ```bash
  psql -U <usuario> -h <host> -d prueba_db \
    -f respaldo_esquema.sql
  ```

- Restaurar datos:
  ```bash
  psql -U <usuario> -h <host> -d prueba_db \
    -f respaldo_datos.sql
  ```

---

# ¡Listo!

Tu entorno de prueba está configurado y protegido con respaldos separados para esquemas y datos.
