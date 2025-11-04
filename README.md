# Funciones Personalizadas en PostgreSQL

Las funciones permiten encapsular lógica reutilizable y son fundamentales para el desarrollo de aplicaciones robustas y mantenibles.

---

## 🎯 Objetivo

Aprender a crear, utilizar y aplicar funciones personalizadas en PostgreSQL, comprendiendo su sintaxis, ventajas y diferencias con otros elementos como los procedimientos almacenados.

---

## 📘 Teoría

### ¿Qué son las funciones en PostgreSQL?

Las funciones son bloques de código que realizan tareas específicas y devuelven un valor. Se escriben en lenguajes como SQL o PL/pgSQL y permiten automatizar procesos dentro de la base de datos.

### Diferencias entre funciones y procedimientos

| Característica         | Función (`FUNCTION`)         | Procedimiento (`PROCEDURE`)     |
|------------------------|------------------------------|----------------------------------|
| Retorno de valores     | Sí                           | No necesariamente                |
| Uso en consultas       | Sí                           | No                               |
| Invocación             | `SELECT` o `CALL`            | Solo `CALL`                      |
| Control de transacciones | Limitado                    | Más flexible                     |

### Ventajas de usar funciones

- Reutilización de código
- Modularidad
- Seguridad
- Mantenimiento sencillo

### Sintaxis básica

```sql
CREATE OR REPLACE FUNCTION nombre_funcion(parametros)
RETURNS tipo_retorno AS $$
BEGIN
    -- cuerpo de la función
END;
$$ LANGUAGE plpgsql;
```

### Tipos de funciones

1. **Escalares**: Devuelven un único valor.
2. **De tabla**: Devuelven un conjunto de registros.
3. **Agregadas**: Se usan para operaciones como sumas o conteos personalizados.
4. **Trigger functions**: Se ejecutan automáticamente en respuesta a eventos.

### Buenas prácticas

- Usar nombres descriptivos
- Documentar con comentarios
- Validar entradas
- Manejar excepciones

---

## 🧪 Ejemplos de funciones

```sql
-- Función para calcular el IVA
CREATE OR REPLACE FUNCTION calcular_iva(monto NUMERIC, tasa NUMERIC DEFAULT 0.16)
RETURNS NUMERIC AS $$
BEGIN
    RETURN monto * tasa;
END;
$$ LANGUAGE plpgsql;

-- Función para obtener nombre completo
CREATE OR REPLACE FUNCTION nombre_completo(nombre TEXT, apellido TEXT)
RETURNS TEXT AS $$
BEGIN
    RETURN nombre || ' ' || apellido;
END;
$$ LANGUAGE plpgsql;

-- Función para verificar mayoría de edad
CREATE OR REPLACE FUNCTION es_mayor_de_edad(edad INT)
RETURNS BOOLEAN AS $$
BEGIN
    RETURN edad >= 18;
END;
$$ LANGUAGE plpgsql;

-- Función de tabla: empleados por departamento
CREATE OR REPLACE FUNCTION empleados_por_departamento(dep_id INT)
RETURNS TABLE(id INT, nombre TEXT) AS $$
BEGIN
    RETURN QUERY SELECT id, nombre FROM empleados WHERE departamento_id = dep_id;
END;
$$ LANGUAGE plpgsql;
```

---

## 📚 Ejercicios Propuestos

1. **Crear una función que calcule el descuento aplicado a un producto.**
   - Parámetros: precio original, porcentaje de descuento.
   - Retorno: precio final.

2. **Crear una función que valide si un correo electrónico contiene '@'.**
   - Parámetro: texto.
   - Retorno: booleano.

3. **Crear una función que devuelva los productos con stock menor a un valor dado.**
   - Parámetro: cantidad mínima.
   - Retorno: tabla con productos.

4. **Crear una función que reciba una fecha y devuelva el día de la semana.**
   - Parámetro: fecha.
   - Retorno: texto.

5. **Crear una función que cuente cuántos empleados hay en un departamento.**
   - Parámetro: ID del departamento.
   - Retorno: entero.


