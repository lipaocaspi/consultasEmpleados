#### Consultas SQL

1. **Creación de tablas**

   ```sql
   CREATE TABLE departamento(
       codigo INT(10) NOT NULL AUTO_INCREMENT,
       nombre VARCHAR(100) NOT NULL,
       presupuesto DOUBLE NOT NULL,
       gastos DOUBLE NOT NULL
   );
   
   CREATE TABLE empleado (
       codigo INT(10) NOT NULL AUTO_INCREMENT,
       nif VARCHAR(9) NOT NULL,
       nombre VARCHAR(100) NOT NULL,
       apellido1 VARCHAR(100) NOT NULL,
       apellido2 VARCHAR(100),
       codigo_departamento INT(10),
       PRIMARY KEY (codigo),
       CONSTRAINT codigoDepartamento FOREIGN KEY (codigo_departamento) REFERENCES departamento(codigo)
   );
   ```

2. **Inserción de datos**

```sql
INSERT INTO departamento
VALUES (1, 'Desarrollo', 120000, 6000),
(2, 'Sistemas', 150000, 21000),
(3, 'Recursos Humanos', 280000, 25000),
(4, 'Contabilidad', 110000, 3000),
(5, 'I+D', 375000, 380000),
(6, 'Proyectos', 0, 0),
(7, 'Publicidad', 0, 1000);
```

```sql
INSERT INTO empleado
VALUES (1, '32481596F', 'Aarón', 'Rivero', 'Gómez', 1),
(2, 'Y5575632D', 'Adela', 'Salas', 'Díaz', 2),
(3, 'R6970642B', 'Adolfo', 'Rubio', 'Flores', 3),
(4, '77705545E', 'Adrián', 'Suárez', NULL, 4),
(5, '17087203C', 'Marcos', 'Loyola', 'Méndez', 5),
(6, '38382980M', 'María', 'Santana', 'Moreno', 1),
(7, '80576669X', 'Pilar', 'Ruiz', NULL, 2),
(8, '71651431Z', 'Pepe', 'Ruiz', 'Santana', 3),
(9, '56399183D', 'Juan', 'Gómez', 'López', 2),
(10, '46384486H', 'Diego', 'Flores', 'Salas', 5),
(11, '67389283A', 'Marta', 'Herrera', 'Gil', 1),
(12, '41234836R', 'Irene', 'Salas', 'Flores', NULL),
(13, '82635162B', 'Juan Antonio', 'Sáez', 'Guerrero', NULL);
```

3. **Consultas sobre una tabla**

   1. Lista el primer apellido de todos los empleados.

      ```sql
      SELECT apellido1
      FROM empleado;
      ```

      

   2. Lista el primer apellido de los empleados eliminando los apellidos que estén repetidos.

      ```sql
      SELECT DISTINCT apellido1
      FROM empleado;
      ```

      

   3. Lista todas las columnas de la tabla *empleado*.

      ```sql
      SELECT codigo, nif, nombre, apellido1, apellido2, codigo_departamento
      FROM empleado;
      ```

      

   4. Lista el nombre y los apellidos de todos los empleados.

      ```sql
      SELECT nombre, apellido1, apellido2
      FROM empleado;
      ```

      

   5. Lista el identificador de los departamentos de los empleados que aparecen en la tabla *empleado*.

      ```sql
      SELECT codigo_departamento
      FROM empleado;
      ```

      

   6. Lista el identificador de los departamentos de los empleados que aparecen en la tabla *empleado*, eliminando los identificadores que aparecen repetidos.

      ```sql
      SELECT DISTINCT codigo_departamento
      FROM empleado;
      ```

      

   7. Lista el nombre y apellidos de los empleados en una única columna.

      ```sql
      SELECT CONCAT(nombre, '', apellido1, '', apellido2) AS nombre_completo
      FROM empleado;
      ```

      

   8. Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en mayúscula.

      ```sql
      SELECT CONCAT(UPPER(nombre), '', UPPER(apellido1), '', UPPER(apellido2)) AS nombre_completo
      FROM empleado;
      ```

      

   9. Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en minúscula.

      ```sql
      SELECT CONCAT(LOWER(nombre), '', LOWER(apellido1), '', LOWER(apellido2)) AS nombre_completo
      FROM empleado;
      ```

      

   10. Lista el identificador de los empleados junto al nif, pero el nif deberá aparecer en dos columnas, una mostrará únicamente los dígitos del nif y la otra la letra.

       ```sql
       
       ```

       

   11. Lista el nombre de cada departamento y el valor del presupuesto actual del que dispone. Para calcular este dato tendrá que restar al valor del presupuesto inicial (columna presupuesto) los gastos que se han generado (columna gastos). Tenga en cuenta que en algunos casos pueden existir valores negativos. Utilice un alias apropiado para la nueva columna columna que está calculando.

       ```sql
       SELECT nombre, (presupuesto - gastos) AS presupuesto_actual
       FROM departamento;
       ```

       

   12. Lista el nombre de los departamentos y el valor del presupuesto actual ordenado de forma ascendente.

       ```sql
       SELECT nombre, presupuesto
       FROM departamento
       ORDER BY nombre ASC, presupuesto ASC;
       ```

       

   13. Lista el nombre de todos los departamentos ordenados de forma ascendente.

       ```sql
       SELECT nombre
       FROM departamento
       ORDER BY nombre ASC;
       ```

       

   14. Lista el nombre de todos los departamentos ordenados de forma descendente.

       ```sql
       SELECT nombre
       FROM departamento
       ORDER BY nombre DESC;
       ```

       

   15. Lista los apellidos y el nombre de todos los empleados, ordenados de forma alfabética tendiendo en cuenta en primer lugar sus apellidos y luego su nombre.

       ```sql
       SELECT apellido1, apellido2, nombre
       FROM empleado
       ORDER BY apellido1 ASC, apellido2 ASC, nombre ASC;
       ```

       

   16. Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen mayor presupuesto.

       ```sql
       SELECT nombre, presupuesto
       FROM departamento
       ORDER BY presupuesto DESC
       LIMIT 3;
       ```

       

   17. Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen menor presupuesto.

       ```sql
       SELECT nombre, presupuesto
       FROM departamento
       ORDER BY presupuesto ASC
       LIMIT 3;
       ```

       

   18. Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen mayor gasto.

       ```sql
       SELECT nombre, gastos
       FROM departamento
       ORDER BY gastos DESC
       LIMIT 2;
       ```

       

   19. Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen menor gasto.

       ```sql
       SELECT nombre, gastos
       FROM departamento
       ORDER BY gastos ASC
       LIMIT 2;
       ```

       

   20. Devuelve una lista con 5 filas a partir de la tercera fila de la tabla empleado. La tercera fila se debe incluir en la respuesta. La respuesta debe incluir todas las columnas de la tabla *empleado*.

       ```sql
       
       ```

       

   21. Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen un presupuesto mayor o igual a 150000 euros.

       ```sql
       SELECT nombre, presupuesto
       FROM departamento
       WHERE presupuesto >= 150000;
       ```

       

   22. Devuelve una lista con el nombre de los departamentos y el gasto, de aquellos que tienen menos de 5000 euros de gastos.

       ```sql
       SELECT nombre, gastos
       FROM departamento
       WHERE gastos < 5000;
       ```

       

   23. Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen  un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.

       ```sql
       SELECT nombre
       FROM departamento
       WHERE presupuesto >= 1000000 AND presupuesto <= 200000;
       ```

       

   24. Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.

       ```sql
       SELECT nombre
       FROM departamento
       WHERE presupuesto < 1000000 AND presupuesto > 200000;
       ```

       

   25. Devuelve una lista con el nombre de los departamentos que tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.

       ```sql
       SELECT nombre
       FROM departamento
       WHERE presupuesto BETWEEN 100000 AND 200000;
       ```

       

   26. Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.

       ```sql
       SELECT nombre
       FROM departamento
       WHERE presupuesto NOT BETWEEN 100000 AND 200000;
       ```

       

   27. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean mayores que el presupuesto del que disponen.

       ```sql
       SELECT nombre, gastos, presupuesto
       FROM departamento
       WHERE gastos > presupuesto;
       ```

       

   28. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean menores que el presupuesto del que disponen.

       ```sql
       SELECT nombre, gastos, presupuesto
       FROM departamento
       WHERE gastos < presupuesto;
       ```

       

   29. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean iguales al presupuesto del que disponen.

       ```sql
       SELECT nombre, gastos, presupuesto
       FROM departamento
       WHERE gastos = presupuesto;
       ```

       

   30. Lista todos los datos de los empleados cuyo segundo apellido sea NULL.

       ```sql
       SELECT codigo, nif, nombre, apellido1, apellido2, codigo_departamento
       FROM empleado
       WHERE apellido2 IS NULL;
       ```

       

   31. Lista todos los datos de los empleados cuyo segundo apellido no sea NULL.

       ```sql
       SELECT codigo, nif, nombre, apellido1, apellido2, codigo_departamento
       FROM empleado
       WHERE apellido2 IS NOT NULL;
       ```

       

   32. Lista todos los datos de los empleados cuyo segundo apellido sea López.

       ```sql
       SELECT codigo, nif, nombre, apellido1, apellido2, codigo_departamento
       FROM empleado
       WHERE apellido2 = 'López';
       ```

       

   33. Lista todos los datos de los empleados cuyo segundo apellido sea Díaz o Moreno. Sin utilizar el operador IN.

       ```sql
       SELECT codigo, nif, nombre, apellido1, apellido2, codigo_departamento
       FROM empleado
       WHERE apellido2 = 'Díaz' OR apellido2 = 'Moreno';
       ```

       

   34. Lista todos los datos de los empleados cuyo segundo apellido sea Díaz o Moreno. Utilizando el operador IN.

       ```sql
       SELECT codigo, nif, nombre, apellido1, apellido2, codigo_departamento
       FROM empleado
       WHERE apellido2 IN ('Díaz', 'Moreno');
       ```

       

   35. Lista los nombres, apellidos y nif de los empleados que trabajan en el departamento 3.

       ```sql
       SELECT nombre, apellido1, apellido2, nif
       FROM empleado
       WHERE codigo_departamento = 3;
       ```

       

   36. Lista los nombres, apellidos y nif de los empleados que trabajan en los departamentos 2, 4 o 5.

       ```sql
       SELECT nombre, apellido1, apellido2, nif
       FROM empleado
       WHERE codigo_departamento IN (2, 4, 5);
       ```

       

4. **Consultas multitabla** (Composición interna)

   1. Devuelve un listado con los empleados y los datos de los departamentos donde trabaja cada uno.

      ```sql
      
      ```

      

   2. Devuelve un listado con los empleados y los datos de los departamentos donde trabaja cada uno. Ordena el resultado, en primer lugar por el nombre del departamento (en orden alfabético) y en segundo lugar por los apellidos y el nombre de los empleados.

      ```sql
      
      ```

      

   3. Devuelve un listado con el identificador y el nombre del departamento, solamente de aquellos departamentos que tienen empleados.

      ```sql
      
      ```

      

   4. Devuelve un listado con el identificador, el nombre del departamento y el valor del presupuesto actual del que dispone, solamente de aquellos departamentos que tienen empleados. El valor del presupuesto actual lo puede calcular restando al valor del presupuesto inicial (columna presupuesto) el valor de los gastos que ha generado (columna gastos).

      ```sql
      
      ```

      

   5. Devuelve el nombre del departamento donde trabaja el empleado que tiene el nif 38382980M.

      ```sql
      
      ```

      

   6. Devuelve el nombre del departamento donde trabaja el empleado Pepe Ruiz Santana.

      ```sql
      
      ```

      

   7. Devuelve un listado con los datos de los empleados que trabajan en el departamento de I+D. Ordena el resultado alfabéticamente.

      ```sql
      
      ```

      

   8. Devuelve un listado con los datos de los empleados que trabajan en el departamento de Sistemas, Contabilidad o I+D. Ordena el resultado alfabéticamente.

      ```sql
      
      ```

      

   9. Devuelve una lista con el nombre de los empleados que tienen los departamentos que no tienen un presupuesto entre 100000 y 200000 euros.

      ```sql
      
      ```

      

   10. Devuelve un listado con el nombre de los departamentos donde existe algún empleado cuyo segundo apellido sea NULL. Tenga en cuenta que no debe mostrar nombres de departamentos que estén repetidos.

       ```sql
       
       ```

       
