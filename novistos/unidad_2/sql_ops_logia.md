---
marp: true
paginate: true
theme: default
class: invert
---

# **Sentencias Lógicas en SQL**

Las **sentencias lógicas en SQL** permiten construir condiciones en consultas para filtrar, combinar y evaluar datos.

---

## **1. Operadores Lógicos**

| Operador | Descripción | Ejemplo |
|:----------|:-------------|:---------|
| `AND` | TRUE si ambas condiciones son verdaderas. | `WHERE edad > 18 AND ciudad = 'Bogotá'` |
| `OR` | TRUE si al menos una condición es verdadera. | `WHERE edad > 18 OR ciudad = 'Bogotá'` |
| `NOT` | Niega una condición. | `WHERE NOT estado = 'Inactivo'` |

---

## **2. Operadores de Comparación**

| Operador | Descripción | Ejemplo |
|:----------|:-------------|:---------|
| `=` | Igual a | `WHERE nombre = 'Juan'` |
| `!=` o `<>` | Diferente de | `WHERE edad != 30` |
| `>` | Mayor que | `WHERE salario > 5000` |
| `<` | Menor que | `WHERE puntuacion < 100` |
| `>=` | Mayor o igual que | `WHERE experiencia >= 5` |
| `<=` | Menor o igual que | `WHERE edad <= 40` |

---

## **3. Operadores Especiales**

| Operador | Descripción | Ejemplo |
|:----------|:-------------|:---------|
| `IN` | Coincide con valores en una lista. | `WHERE ciudad IN ('Bogotá', 'Medellín')` |
| `NOT IN` | Excluye los valores de la lista. | `WHERE ciudad NOT IN ('Cali', 'Cartagena')` |
| `BETWEEN` | Evalúa si un valor está dentro de un rango. | `WHERE edad BETWEEN 20 AND 30` |

---

| Operador | Descripción | Ejemplo |
|:----------|:-------------|:---------|
| `LIKE` | Busca coincidencias según un patrón. | `WHERE nombre LIKE 'J%'` |
| `IS NULL` | Evalúa si un valor es `NULL`. | `WHERE fecha_baja IS NULL` |
| `IS NOT NULL` | Evalúa si un valor **no** es `NULL`. | `WHERE telefono IS NOT NULL` |

---

## **4. Uso de `CASE` para Lógica Condicional**

```sql
SELECT nombre,
       CASE
           WHEN edad < 18 THEN 'Menor de edad'
           WHEN edad BETWEEN 18 AND 60 THEN 'Adulto'
           ELSE 'Adulto mayor'
       END AS categoria
FROM personas;
```

---

## **5. Combinación de Operadores**

Puedes combinar operadores para crear condiciones avanzadas:

```sql
SELECT *
FROM empleados
WHERE (salario > 3000 AND edad < 40)
   OR (cargo = 'Gerente' AND departamento = 'Ventas')
   AND estado IS NOT NULL;
```
