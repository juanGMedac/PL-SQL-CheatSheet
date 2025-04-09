![PLSQL Cheat Sheet Banner](https://github.com/juanGMedac/PL-SQL-CheatSheet/blob/main/banner.png)

# 📘 PL/SQL Cheat Sheet

Este repositorio contiene una guía rápida de PL/SQL. Ideal para quienes trabajan con Oracle y necesitan una referencia ágil de sintaxis, estructuras y buenas prácticas.

---

## 📦 Índice

- [Bloques](#-bloques)
- [Variables](#-variables)
- [Constantes](#-constantes)
- [SELECT INTO](#-select-into)
- [%TYPE](#-type)
- [Condiciones (IF/CASE)](#-condiciones-ifcase)
- [Loops](#-loops)
- [Triggers](#-triggers)
- [Cursores](#-cursores)
- [Registros (Records)](#-records)
- [Funciones](#-funciones)
- [Procedimientos Almacenados](#-procedimientos)
- [Paquetes](#-paquetes)
- [Excepciones](#-excepciones)
- [Colecciones](#-colecciones)
- [Programación Orientada a Objetos](#-programación-orientada-a-objetos)

---

## 🔹 Bloques

```sql
DECLARE
   -- Declaraciones
BEGIN
   -- Código principal
EXCEPTION
   -- Manejo de errores
END;
```

---

## 🔹 Variables

```sql
v_nombre VARCHAR2(50);
v_edad NUMBER := 30;
```

---

## 🔹 Constantes

```sql
c_tax CONSTANT NUMBER := 0.18;
```

---

## 🔹 SELECT INTO

```sql
DECLARE
   v_salario employees.salary%TYPE;
BEGIN
   SELECT salary INTO v_salario
   FROM employees
   WHERE employee_id = 100;
END;
```

---

## 🔹 %TYPE

```sql
v_nombre employees.first_name%TYPE;
```

---

## 🔹 Condiciones

### IF / ELSIF / ELSE

```sql
IF salario > 5000 THEN
   DBMS_OUTPUT.PUT_LINE('Alto salario');
ELSIF salario > 3000 THEN
   DBMS_OUTPUT.PUT_LINE('Salario medio');
ELSE
   DBMS_OUTPUT.PUT_LINE('Salario bajo');
END IF;
```

### CASE

```sql
CASE departamento_id
   WHEN 10 THEN DBMS_OUTPUT.PUT_LINE('Administración');
   WHEN 20 THEN DBMS_OUTPUT.PUT_LINE('Ventas');
   ELSE DBMS_OUTPUT.PUT_LINE('Otro');
END CASE;
```

---

## 🔹 Loops

### FOR

```sql
FOR i IN 1..5 LOOP
   DBMS_OUTPUT.PUT_LINE(i);
END LOOP;
```

### WHILE

```sql
WHILE i <= 5 LOOP
   DBMS_OUTPUT.PUT_LINE(i);
   i := i + 1;
END LOOP;
```

### LOOP / EXIT

```sql
LOOP
   EXIT WHEN contador > 10;
   contador := contador + 1;
END LOOP;
```

---

## 🔹 Triggers

```sql
CREATE OR REPLACE TRIGGER trg_audit
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
   INSERT INTO audit_table (user_action) VALUES ('Insertado empleado');
END;
```

---

## 🔹 Cursores

### Explícito

```sql
DECLARE
   CURSOR c_emp IS SELECT first_name FROM employees;
   v_nombre employees.first_name%TYPE;
BEGIN
   OPEN c_emp;
   LOOP
      FETCH c_emp INTO v_nombre;
      EXIT WHEN c_emp%NOTFOUND;
      DBMS_OUTPUT.PUT_LINE(v_nombre);
   END LOOP;
   CLOSE c_emp;
END;
```

---

## 🔹 Records

```sql
DECLARE
   emp_rec employees%ROWTYPE;
BEGIN
   SELECT * INTO emp_rec FROM employees WHERE employee_id = 100;
   DBMS_OUTPUT.PUT_LINE(emp_rec.first_name || ' ' || emp_rec.last_name);
END;
```

---

## 🔹 Funciones

```sql
CREATE OR REPLACE FUNCTION obtener_saludo(nombre IN VARCHAR2)
RETURN VARCHAR2 IS
BEGIN
   RETURN 'Hola, ' || nombre;
END;
```

---

## 🔹 Procedimientos

```sql
CREATE OR REPLACE PROCEDURE saludar(nombre IN VARCHAR2) IS
BEGIN
   DBMS_OUTPUT.PUT_LINE('Hola, ' || nombre);
END;
```

---

## 🔹 Paquetes

```sql
-- Especificación
CREATE OR REPLACE PACKAGE mi_paquete AS
   PROCEDURE saludar(nombre IN VARCHAR2);
   FUNCTION obtener_saludo(nombre IN VARCHAR2) RETURN VARCHAR2;
END;

-- Cuerpo
CREATE OR REPLACE PACKAGE BODY mi_paquete AS
   PROCEDURE saludar(nombre IN VARCHAR2) IS
   BEGIN
      DBMS_OUTPUT.PUT_LINE('Hola, ' || nombre);
   END;

   FUNCTION obtener_saludo(nombre IN VARCHAR2) RETURN VARCHAR2 IS
   BEGIN
      RETURN 'Saludos, ' || nombre;
   END;
END;
```

---

## 🔹 Excepciones

```sql
BEGIN
   -- Código
EXCEPTION
   WHEN NO_DATA_FOUND THEN
      DBMS_OUTPUT.PUT_LINE('No se encontraron datos');
   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
```

---

## 🔹 Colecciones

### VARRAY

```sql
TYPE numeros_array IS VARRAY(5) OF NUMBER;
v_numeros numeros_array := numeros_array(1, 2, 3, 4, 5);
```

### Nested Table

```sql
TYPE lista_nombres IS TABLE OF VARCHAR2(50);
v_nombres lista_nombres := lista_nombres('Ana', 'Luis');
```

### Associative Array

```sql
TYPE empleados_tab IS TABLE OF VARCHAR2(100) INDEX BY PLS_INTEGER;
v_empleados empleados_tab;
v_empleados(1) := 'Juan';
```

---

## 🔹 Programación Orientada a Objetos

### Definición de Tipo Objeto

```sql
CREATE OR REPLACE TYPE persona_t AS OBJECT (
   nombre VARCHAR2(100),
   edad NUMBER,
   MEMBER PROCEDURE mostrar
);
```

### Cuerpo del Tipo

```sql
CREATE OR REPLACE TYPE BODY persona_t AS
   MEMBER PROCEDURE mostrar IS
   BEGIN
      DBMS_OUTPUT.PUT_LINE('Nombre: ' || nombre || ', Edad: ' || edad);
   END;
END;
```

### Uso

```sql
DECLARE
   p persona_t := persona_t('Carlos', 30);
BEGIN
   p.mostrar;
END;
```

---

## 📚 Recursos útiles

- [Oracle Documentation](https://docs.oracle.com/en/database/oracle/oracle-database/)
- [W3Schools PL/SQL](https://www.w3schools.com/sql/sql_plsql.asp)
- [Oracle Live SQL](https://livesql.oracle.com/)

---

> 🙌 ¿Te fue útil? ¡Haz una estrella ⭐️ al repo y contribuye con ejemplos o correcciones!
