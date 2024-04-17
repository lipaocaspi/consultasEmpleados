#### Consultas SQL

##### **Creación de tablas**

```sql
CREATE TABLE departamento(
    codigo INT(10) NOT NULL AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    presupuesto DOUBLE NOT NULL,
    gastos DOUBLE NOT NULL
);

CREATE TABLE empleado (
    codigo INT(10) NOT NULL AUTO_INCREMENT PRIMARY KEY,
    nif VARCHAR(9) NOT NULL,
    nombre VARCHAR(100) NOT NULL,
    apellido1 VARCHAR(100) NOT NULL,
    apellido2 VARCHAR(100),
    codigo_departamento INT(10),
    FOREIGN KEY (codigo_departamento) REFERENCES departamento(codigo)
);
```

##### **Inserción de datos**

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

##### **Consultas sobre una tabla**

1. Lista el primer apellido de todos los empleados.

   ```sql
   SELECT apellido1
   FROM empleado;
   
   +-----------+
   | apellido1 |
   +-----------+
   | Rivero    |
   | Salas     |
   | Rubio     |
   | Suárez    |
   | Loyola    |
   | Santana   |
   | Ruiz      |
   | Ruiz      |
   | Gómez     |
   | Flores    |
   | Herrera   |
   | Salas     |
   | Sáez      |
   +-----------+
   ```

   

2. Lista el primer apellido de los empleados eliminando los apellidos que estén repetidos.

   ```sql
   SELECT DISTINCT apellido1
   FROM empleado;
   
   +-----------+
   | apellido1 |
   +-----------+
   | Rivero    |
   | Salas     |
   | Rubio     |
   | Suárez    |
   | Loyola    |
   | Santana   |
   | Ruiz      |
   | Gómez     |
   | Flores    |
   | Herrera   |
   | Sáez      |
   +-----------+
   ```

   

3. Lista todas las columnas de la tabla *empleado*.

   ```sql
   SELECT codigo, nif, nombre, apellido1, apellido2, codigo_departamento
   FROM empleado;
   
   +--------+-----------+--------------+-----------+-----------+---------------------+
   | codigo | nif       | nombre       | apellido1 | apellido2 | codigo_departamento |
   +--------+-----------+--------------+-----------+-----------+---------------------+
   |      1 | 32481596F | Aarón        | Rivero    | Gómez     |                   1 |
   |      2 | Y5575632D | Adela        | Salas     | Díaz      |                   2 |
   |      3 | R6970642B | Adolfo       | Rubio     | Flores    |                   3 |
   |      4 | 77705545E | Adrián       | Suárez    | NULL      |                   4 |
   |      5 | 17087203C | Marcos       | Loyola    | Méndez    |                   5 |
   |      6 | 38382980M | María        | Santana   | Moreno    |                   1 |
   |      7 | 80576669X | Pilar        | Ruiz      | NULL      |                   2 |
   |      8 | 71651431Z | Pepe         | Ruiz      | Santana   |                   3 |
   |      9 | 56399183D | Juan         | Gómez     | López     |                   2 |
   |     10 | 46384486H | Diego        | Flores    | Salas     |                   5 |
   |     11 | 67389283A | Marta        | Herrera   | Gil       |                   1 |
   |     12 | 41234836R | Irene        | Salas     | Flores    |                NULL |
   |     13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |                NULL |
   +--------+-----------+--------------+-----------+-----------+---------------------+
   ```

   

4. Lista el nombre y los apellidos de todos los empleados.

   ```sql
   SELECT nombre, apellido1, apellido2
   FROM empleado;
   
   +--------------+-----------+-----------+
   | nombre       | apellido1 | apellido2 |
   +--------------+-----------+-----------+
   | Aarón        | Rivero    | Gómez     |
   | Adela        | Salas     | Díaz      |
   | Adolfo       | Rubio     | Flores    |
   | Adrián       | Suárez    | NULL      |
   | Marcos       | Loyola    | Méndez    |
   | María        | Santana   | Moreno    |
   | Pilar        | Ruiz      | NULL      |
   | Pepe         | Ruiz      | Santana   |
   | Juan         | Gómez     | López     |
   | Diego        | Flores    | Salas     |
   | Marta        | Herrera   | Gil       |
   | Irene        | Salas     | Flores    |
   | Juan Antonio | Sáez      | Guerrero  |
   +--------------+-----------+-----------+
   ```

   

5. Lista el identificador de los departamentos de los empleados que aparecen en la tabla *empleado*.

   ```sql
   SELECT codigo_departamento
   FROM empleado;
   
   +---------------------+
   | codigo_departamento |
   +---------------------+
   |                NULL |
   |                NULL |
   |                   1 |
   |                   1 |
   |                   1 |
   |                   2 |
   |                   2 |
   |                   2 |
   |                   3 |
   |                   3 |
   |                   4 |
   |                   5 |
   |                   5 |
   +---------------------+
   ```

   

6. Lista el identificador de los departamentos de los empleados que aparecen en la tabla *empleado*, eliminando los identificadores que aparecen repetidos.

   ```sql
   SELECT DISTINCT codigo_departamento
   FROM empleado;
   
   +---------------------+
   | codigo_departamento |
   +---------------------+
   |                NULL |
   |                   1 |
   |                   2 |
   |                   3 |
   |                   4 |
   |                   5 |
   +---------------------+
   ```

   

7. Lista el nombre y apellidos de los empleados en una única columna.

   ```sql
   SELECT CONCAT(nombre, ' ', apellido1, ' ', COALESCE(apellido2, '')) AS nombre_completo
   FROM empleado;
   
   +-----------------------------+
   | nombre_completo             |
   +-----------------------------+
   | Aarón Rivero Gómez          |
   | Adela Salas Díaz            |
   | Adolfo Rubio Flores         |
   | Adrián Suárez               |
   | Marcos Loyola Méndez        |
   | María Santana Moreno        |
   | Pilar Ruiz                  |
   | Pepe Ruiz Santana           |
   | Juan Gómez López            |
   | Diego Flores Salas          |
   | Marta Herrera Gil           |
   | Irene Salas Flores          |
   | Juan Antonio Sáez Guerrero  |
   +-----------------------------+
   ```

   

8. Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en mayúscula.

   ```sql
   SELECT CONCAT(UPPER(nombre), ' ', UPPER(apellido1), ' ', UPPER(COALESCE(apellido2, ''))) AS nombre_completo
   FROM empleado;
   
   +-----------------------------+
   | nombre_completo             |
   +-----------------------------+
   | AARÓN RIVERO GÓMEZ          |
   | ADELA SALAS DÍAZ            |
   | ADOLFO RUBIO FLORES         |
   | ADRIÁN SUÁREZ               |
   | MARCOS LOYOLA MÉNDEZ        |
   | MARÍA SANTANA MORENO        |
   | PILAR RUIZ                  |
   | PEPE RUIZ SANTANA           |
   | JUAN GÓMEZ LÓPEZ            |
   | DIEGO FLORES SALAS          |
   | MARTA HERRERA GIL           |
   | IRENE SALAS FLORES          |
   | JUAN ANTONIO SÁEZ GUERRERO  |
   +-----------------------------+
   ```

   

9. Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en minúscula.

   ```sql
   SELECT CONCAT(LOWER(nombre), ' ', LOWER(apellido1), ' ', LOWER(COALESCE(apellido2, ''))) AS nombre_completo
   FROM empleado;
   
   +-----------------------------+
   | nombre_completo             |
   +-----------------------------+
   | aarón rivero gómez          |
   | adela salas díaz            |
   | adolfo rubio flores         |
   | adrián suárez               |
   | marcos loyola méndez        |
   | maría santana moreno        |
   | pilar ruiz                  |
   | pepe ruiz santana           |
   | juan gómez lópez            |
   | diego flores salas          |
   | marta herrera gil           |
   | irene salas flores          |
   | juan antonio sáez guerrero  |
   +-----------------------------+
   ```

   

10. Lista el identificador de los empleados junto al nif, pero el nif deberá aparecer en dos columnas, una mostrará únicamente los dígitos del nif y la otra la letra.

    ```sql
    
    ```

    

11. Lista el nombre de cada departamento y el valor del presupuesto actual del que dispone. Para calcular este dato tendrá que restar al valor del presupuesto inicial (columna presupuesto) los gastos que se han generado (columna gastos). Tenga en cuenta que en algunos casos pueden existir valores negativos. Utilice un alias apropiado para la nueva columna columna que está calculando.

    ```sql
    SELECT nombre, (presupuesto - gastos) AS presupuesto_actual
    FROM departamento;
    
    +------------------+--------------------+
    | nombre           | presupuesto_actual |
    +------------------+--------------------+
    | Desarrollo       |             114000 |
    | Sistemas         |             129000 |
    | Recursos Humanos |             255000 |
    | Contabilidad     |             107000 |
    | I+D              |              -5000 |
    | Proyectos        |                  0 |
    | Publicidad       |              -1000 |
    +------------------+--------------------+
    ```

    

12. Lista el nombre de los departamentos y el valor del presupuesto actual ordenado de forma ascendente.

    ```sql
    SELECT nombre, (presupuesto - gastos) AS presupuesto_actual
    FROM departamento
    ORDER BY nombre ASC, presupuesto ASC;
    
    +------------------+--------------------+
    | nombre           | presupuesto_actual |
    +------------------+--------------------+
    | Contabilidad     |             107000 |
    | Desarrollo       |             114000 |
    | I+D              |              -5000 |
    | Proyectos        |                  0 |
    | Publicidad       |              -1000 |
    | Recursos Humanos |             255000 |
    | Sistemas         |             129000 |
    +------------------+--------------------+
    ```

    

13. Lista el nombre de todos los departamentos ordenados de forma ascendente.

    ```sql
    SELECT nombre
    FROM departamento
    ORDER BY nombre ASC;
    
    +------------------+
    | nombre           |
    +------------------+
    | Contabilidad     |
    | Desarrollo       |
    | I+D              |
    | Proyectos        |
    | Publicidad       |
    | Recursos Humanos |
    | Sistemas         |
    +------------------+
    ```

    

14. Lista el nombre de todos los departamentos ordenados de forma descendente.

    ```sql
    SELECT nombre
    FROM departamento
    ORDER BY nombre DESC;
    
    +------------------+
    | nombre           |
    +------------------+
    | Sistemas         |
    | Recursos Humanos |
    | Publicidad       |
    | Proyectos        |
    | I+D              |
    | Desarrollo       |
    | Contabilidad     |
    +------------------+
    ```

    

15. Lista los apellidos y el nombre de todos los empleados, ordenados de forma alfabética tendiendo en cuenta en primer lugar sus apellidos y luego su nombre.

    ```sql
    SELECT apellido1, apellido2, nombre
    FROM empleado
    ORDER BY apellido1 ASC, apellido2 ASC, nombre ASC;
    
    +-----------+-----------+--------------+
    | apellido1 | apellido2 | nombre       |
    +-----------+-----------+--------------+
    | Flores    | Salas     | Diego        |
    | Gómez     | López     | Juan         |
    | Herrera   | Gil       | Marta        |
    | Loyola    | Méndez    | Marcos       |
    | Rivero    | Gómez     | Aarón        |
    | Rubio     | Flores    | Adolfo       |
    | Ruiz      | NULL      | Pilar        |
    | Ruiz      | Santana   | Pepe         |
    | Sáez      | Guerrero  | Juan Antonio |
    | Salas     | Díaz      | Adela        |
    | Salas     | Flores    | Irene        |
    | Santana   | Moreno    | María        |
    | Suárez    | NULL      | Adrián       |
    +-----------+-----------+--------------+
    ```

    

16. Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen mayor presupuesto.

    ```sql
    SELECT nombre, presupuesto
    FROM departamento
    ORDER BY presupuesto DESC
    LIMIT 3;
    
    +------------------+-------------+
    | nombre           | presupuesto |
    +------------------+-------------+
    | I+D              |      375000 |
    | Recursos Humanos |      280000 |
    | Sistemas         |      150000 |
    +------------------+-------------+
    ```

    

17. Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen menor presupuesto.

    ```sql
    SELECT nombre, presupuesto
    FROM departamento
    ORDER BY presupuesto ASC
    LIMIT 3;
    
    +--------------+-------------+
    | nombre       | presupuesto |
    +--------------+-------------+
    | Proyectos    |           0 |
    | Publicidad   |           0 |
    | Contabilidad |      110000 |
    +--------------+-------------+
    ```

    

18. Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen mayor gasto.

    ```sql
    SELECT nombre, gastos
    FROM departamento
    ORDER BY gastos DESC
    LIMIT 2;
    
    +------------------+--------+
    | nombre           | gastos |
    +------------------+--------+
    | I+D              | 380000 |
    | Recursos Humanos |  25000 |
    +------------------+--------+
    ```

    

19. Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen menor gasto.

    ```sql
    SELECT nombre, gastos
    FROM departamento
    ORDER BY gastos ASC
    LIMIT 2;
    
    +------------+--------+
    | nombre     | gastos |
    +------------+--------+
    | Proyectos  |      0 |
    | Publicidad |   1000 |
    +------------+--------+
    ```

    

20. Devuelve una lista con 5 filas a partir de la tercera fila de la tabla empleado. La tercera fila se debe incluir en la respuesta. La respuesta debe incluir todas las columnas de la tabla *empleado*.

    ```sql
    
    ```

    

21. Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen un presupuesto mayor o igual a 150000 euros.

    ```sql
    SELECT nombre, presupuesto
    FROM departamento
    WHERE presupuesto >= 150000;
    
    +------------------+-------------+
    | nombre           | presupuesto |
    +------------------+-------------+
    | Sistemas         |      150000 |
    | Recursos Humanos |      280000 |
    | I+D              |      375000 |
    +------------------+-------------+
    ```

    

22. Devuelve una lista con el nombre de los departamentos y el gasto, de aquellos que tienen menos de 5000 euros de gastos.

    ```sql
    SELECT nombre, gastos
    FROM departamento
    WHERE gastos < 5000;
    
    +--------------+--------+
    | nombre       | gastos |
    +--------------+--------+
    | Contabilidad |   3000 |
    | Proyectos    |      0 |
    | Publicidad   |   1000 |
    +--------------+--------+
    ```

    

23. Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen  un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.

    ```sql
    SELECT nombre, presupuesto
    FROM departamento
    WHERE presupuesto >= 100000 AND presupuesto <= 200000;
    
    +--------------+-------------+
    | nombre       | presupuesto |
    +--------------+-------------+
    | Desarrollo   |      120000 |
    | Sistemas     |      150000 |
    | Contabilidad |      110000 |
    +--------------+-------------+
    ```

    

24. Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.

    ```sql
    SELECT nombre
    FROM departamento
    WHERE presupuesto < 100000 OR presupuesto > 200000;
    
    +------------------+
    | nombre           |
    +------------------+
    | Recursos Humanos |
    | I+D              |
    | Proyectos        |
    | Publicidad       |
    +------------------+
    ```

    

25. Devuelve una lista con el nombre de los departamentos que tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.

    ```sql
    SELECT nombre
    FROM departamento
    WHERE presupuesto BETWEEN 100000 AND 200000;
    
    +--------------+
    | nombre       |
    +--------------+
    | Desarrollo   |
    | Sistemas     |
    | Contabilidad |
    +--------------+
    ```

    

26. Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.

    ```sql
    SELECT nombre
    FROM departamento
    WHERE presupuesto NOT BETWEEN 100000 AND 200000;
    
    +------------------+
    | nombre           |
    +------------------+
    | Recursos Humanos |
    | I+D              |
    | Proyectos        |
    | Publicidad       |
    +------------------+
    ```

    

27. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean mayores que el presupuesto del que disponen.

    ```sql
    SELECT nombre, gastos, presupuesto
    FROM departamento
    WHERE gastos > presupuesto;
    
    +------------+--------+-------------+
    | nombre     | gastos | presupuesto |
    +------------+--------+-------------+
    | I+D        | 380000 |      375000 |
    | Publicidad |   1000 |           0 |
    +------------+--------+-------------+
    ```

    

28. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean menores que el presupuesto del que disponen.

    ```sql
    SELECT nombre, gastos, presupuesto
    FROM departamento
    WHERE gastos < presupuesto;
    
    +------------------+--------+-------------+
    | nombre           | gastos | presupuesto |
    +------------------+--------+-------------+
    | Desarrollo       |   6000 |      120000 |
    | Sistemas         |  21000 |      150000 |
    | Recursos Humanos |  25000 |      280000 |
    | Contabilidad     |   3000 |      110000 |
    +------------------+--------+-------------+
    ```

    

29. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean iguales al presupuesto del que disponen.

    ```sql
    SELECT nombre, gastos, presupuesto
    FROM departamento
    WHERE gastos = presupuesto;
    
    +-----------+--------+-------------+
    | nombre    | gastos | presupuesto |
    +-----------+--------+-------------+
    | Proyectos |      0 |           0 |
    +-----------+--------+-------------+
    ```

    

30. Lista todos los datos de los empleados cuyo segundo apellido sea NULL.

    ```sql
    SELECT codigo, nif, nombre, apellido1, apellido2, codigo_departamento
    FROM empleado
    WHERE apellido2 IS NULL;
    
    +--------+-----------+---------+-----------+-----------+---------------------+
    | codigo | nif       | nombre  | apellido1 | apellido2 | codigo_departamento |
    +--------+-----------+---------+-----------+-----------+---------------------+
    |      4 | 77705545E | Adrián  | Suárez    | NULL      |                   4 |
    |      7 | 80576669X | Pilar   | Ruiz      | NULL      |                   2 |
    +--------+-----------+---------+-----------+-----------+---------------------+
    ```

    

31. Lista todos los datos de los empleados cuyo segundo apellido no sea NULL.

    ```sql
    SELECT codigo, nif, nombre, apellido1, apellido2, codigo_departamento
    FROM empleado
    WHERE apellido2 IS NOT NULL;
    
    +--------+-----------+--------------+-----------+-----------+---------------------+
    | codigo | nif       | nombre       | apellido1 | apellido2 | codigo_departamento |
    +--------+-----------+--------------+-----------+-----------+---------------------+
    |      1 | 32481596F | Aarón        | Rivero    | Gómez     |                   1 |
    |      2 | Y5575632D | Adela        | Salas     | Díaz      |                   2 |
    |      3 | R6970642B | Adolfo       | Rubio     | Flores    |                   3 |
    |      5 | 17087203C | Marcos       | Loyola    | Méndez    |                   5 |
    |      6 | 38382980M | María        | Santana   | Moreno    |                   1 |
    |      8 | 71651431Z | Pepe         | Ruiz      | Santana   |                   3 |
    |      9 | 56399183D | Juan         | Gómez     | López     |                   2 |
    |     10 | 46384486H | Diego        | Flores    | Salas     |                   5 |
    |     11 | 67389283A | Marta        | Herrera   | Gil       |                   1 |
    |     12 | 41234836R | Irene        | Salas     | Flores    |                NULL |
    |     13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |                NULL |
    +--------+-----------+--------------+-----------+-----------+---------------------+
    ```

    

32. Lista todos los datos de los empleados cuyo segundo apellido sea López.

    ```sql
    SELECT codigo, nif, nombre, apellido1, apellido2, codigo_departamento
    FROM empleado
    WHERE apellido2 = 'López';
    
    +--------+-----------+--------+-----------+-----------+---------------------+
    | codigo | nif       | nombre | apellido1 | apellido2 | codigo_departamento |
    +--------+-----------+--------+-----------+-----------+---------------------+
    |      9 | 56399183D | Juan   | Gómez     | López     |                   2 |
    +--------+-----------+--------+-----------+-----------+---------------------+
    ```

    

33. Lista todos los datos de los empleados cuyo segundo apellido sea Díaz o Moreno. Sin utilizar el operador IN.

    ```sql
    SELECT codigo, nif, nombre, apellido1, apellido2, codigo_departamento
    FROM empleado
    WHERE apellido2 = 'Díaz' OR apellido2 = 'Moreno';
    
    +--------+-----------+--------+-----------+-----------+---------------------+
    | codigo | nif       | nombre | apellido1 | apellido2 | codigo_departamento |
    +--------+-----------+--------+-----------+-----------+---------------------+
    |      2 | Y5575632D | Adela  | Salas     | Díaz      |                   2 |
    |      6 | 38382980M | María  | Santana   | Moreno    |                   1 |
    +--------+-----------+--------+-----------+-----------+---------------------+
    ```

    

34. Lista todos los datos de los empleados cuyo segundo apellido sea Díaz o Moreno. Utilizando el operador IN.

    ```sql
    SELECT codigo, nif, nombre, apellido1, apellido2, codigo_departamento
    FROM empleado
    WHERE apellido2 IN ('Díaz', 'Moreno');
    
    +--------+-----------+--------+-----------+-----------+---------------------+
    | codigo | nif       | nombre | apellido1 | apellido2 | codigo_departamento |
    +--------+-----------+--------+-----------+-----------+---------------------+
    |      2 | Y5575632D | Adela  | Salas     | Díaz      |                   2 |
    |      6 | 38382980M | María  | Santana   | Moreno    |                   1 |
    +--------+-----------+--------+-----------+-----------+---------------------+
    ```

    

35. Lista los nombres, apellidos y nif de los empleados que trabajan en el departamento 3.

    ```sql
    SELECT nombre, apellido1, apellido2, nif
    FROM empleado
    WHERE codigo_departamento = 3;
    
    +--------+-----------+-----------+-----------+
    | nombre | apellido1 | apellido2 | nif       |
    +--------+-----------+-----------+-----------+
    | Adolfo | Rubio     | Flores    | R6970642B |
    | Pepe   | Ruiz      | Santana   | 71651431Z |
    +--------+-----------+-----------+-----------+
    ```

    

36. Lista los nombres, apellidos y nif de los empleados que trabajan en los departamentos 2, 4 o 5.

    ```sql
    SELECT nombre, apellido1, apellido2, nif
    FROM empleado
    WHERE codigo_departamento IN (2, 4, 5);
    
    +---------+-----------+-----------+-----------+
    | nombre  | apellido1 | apellido2 | nif       |
    +---------+-----------+-----------+-----------+
    | Adela   | Salas     | Díaz      | Y5575632D |
    | Pilar   | Ruiz      | NULL      | 80576669X |
    | Juan    | Gómez     | López     | 56399183D |
    | Adrián  | Suárez    | NULL      | 77705545E |
    | Marcos  | Loyola    | Méndez    | 17087203C |
    | Diego   | Flores    | Salas     | 46384486H |
    +---------+-----------+-----------+-----------+
    ```
    
    

##### **Consultas multitabla** (Composición interna)

1. Devuelve un listado con los empleados y los datos de los departamentos donde trabaja cada uno.

   ```sql
   SELECT e.nombre, e.apellido1, e.apellido2, d.codigo AS codigo_departamento, d.nombre AS nombre_departamento, d.presupuesto, d.gastos
   FROM empleado AS e, departamento AS d
   WHERE e.codigo_departamento = d.codigo;
   
   +---------+-----------+-----------+---------------------+---------------------+-------------+--------+
   | nombre  | apellido1 | apellido2 | codigo_departamento | nombre_departamento | presupuesto | gastos |
   +---------+-----------+-----------+---------------------+---------------------+-------------+--------+
   | Aarón   | Rivero    | Gómez     |                   1 | Desarrollo          |      120000 |   6000 |
   | María   | Santana   | Moreno    |                   1 | Desarrollo          |      120000 |   6000 |
   | Marta   | Herrera   | Gil       |                   1 | Desarrollo          |      120000 |   6000 |
   | Adela   | Salas     | Díaz      |                   2 | Sistemas            |      150000 |  21000 |
   | Pilar   | Ruiz      | NULL      |                   2 | Sistemas            |      150000 |  21000 |
   | Juan    | Gómez     | López     |                   2 | Sistemas            |      150000 |  21000 |
   | Adolfo  | Rubio     | Flores    |                   3 | Recursos Humanos    |      280000 |  25000 |
   | Pepe    | Ruiz      | Santana   |                   3 | Recursos Humanos    |      280000 |  25000 |
   | Adrián  | Suárez    | NULL      |                   4 | Contabilidad        |      110000 |   3000 |
   | Marcos  | Loyola    | Méndez    |                   5 | I+D                 |      375000 | 380000 |
   | Diego   | Flores    | Salas     |                   5 | I+D                 |      375000 | 380000 |
   +---------+-----------+-----------+---------------------+---------------------+-------------+--------+
   ```

   

2. Devuelve un listado con los empleados y los datos de los departamentos donde trabaja cada uno. Ordena el resultado, en primer lugar por el nombre del departamento (en orden alfabético) y en segundo lugar por los apellidos y el nombre de los empleados.

   ```sql
   SELECT e.nombre, e.apellido1, e.apellido2, d.codigo AS codigo_departamento, d.nombre AS nombre_departamento, d.presupuesto, d.gastos
   FROM empleado AS e, departamento AS d
   WHERE e.codigo_departamento = d.codigo
   ORDER BY d.nombre ASC, e.apellido1 ASC, e.apellido2 ASC, e.nombre ASC;
   
   +---------+-----------+-----------+---------------------+---------------------+-------------+--------+
   | nombre  | apellido1 | apellido2 | codigo_departamento | nombre_departamento | presupuesto | gastos |
   +---------+-----------+-----------+---------------------+---------------------+-------------+--------+
   | Adrián  | Suárez    | NULL      |                   4 | Contabilidad        |      110000 |   3000 |
   | Marta   | Herrera   | Gil       |                   1 | Desarrollo          |      120000 |   6000 |
   | Aarón   | Rivero    | Gómez     |                   1 | Desarrollo          |      120000 |   6000 |
   | María   | Santana   | Moreno    |                   1 | Desarrollo          |      120000 |   6000 |
   | Diego   | Flores    | Salas     |                   5 | I+D                 |      375000 | 380000 |
   | Marcos  | Loyola    | Méndez    |                   5 | I+D                 |      375000 | 380000 |
   | Adolfo  | Rubio     | Flores    |                   3 | Recursos Humanos    |      280000 |  25000 |
   | Pepe    | Ruiz      | Santana   |                   3 | Recursos Humanos    |      280000 |  25000 |
   | Juan    | Gómez     | López     |                   2 | Sistemas            |      150000 |  21000 |
   | Pilar   | Ruiz      | NULL      |                   2 | Sistemas            |      150000 |  21000 |
   | Adela   | Salas     | Díaz      |                   2 | Sistemas            |      150000 |  21000 |
   +---------+-----------+-----------+---------------------+---------------------+-------------+--------+
   ```

   

3. Devuelve un listado con el identificador y el nombre del departamento, solamente de aquellos departamentos que tienen empleados.

   ```sql
   SELECT DISTINCT(d.codigo), d.nombre
   FROM departamento AS d, empleado AS e
   WHERE d.codigo = e.codigo_departamento;
   
   +--------+------------------+
   | codigo | nombre           |
   +--------+------------------+
   |      1 | Desarrollo       |
   |      2 | Sistemas         |
   |      3 | Recursos Humanos |
   |      4 | Contabilidad     |
   |      5 | I+D              |
   +--------+------------------+
   ```

   

4. Devuelve un listado con el identificador, el nombre del departamento y el valor del presupuesto actual del que dispone, solamente de aquellos departamentos que tienen empleados. El valor del presupuesto actual lo puede calcular restando al valor del presupuesto inicial (columna presupuesto) el valor de los gastos que ha generado (columna gastos).

   ```sql
   SELECT DISTINCT(d.codigo), d.nombre, (d.presupuesto - d.gastos) AS presupuesto_actual
   FROM departamento AS d, empleado AS e
   WHERE d.codigo = e.codigo_departamento;
   
   +--------+------------------+--------------------+
   | codigo | nombre           | presupuesto_actual |
   +--------+------------------+--------------------+
   |      1 | Desarrollo       |             114000 |
   |      2 | Sistemas         |             129000 |
   |      3 | Recursos Humanos |             255000 |
   |      4 | Contabilidad     |             107000 |
   |      5 | I+D              |              -5000 |
   +--------+------------------+--------------------+
   ```

   

5. Devuelve el nombre del departamento donde trabaja el empleado que tiene el nif 38382980M.

   ```sql
   SELECT d.nombre
   FROM departamento AS d, empleado AS e
   WHERE d.codigo = e.codigo_departamento AND e.nif = '38382980M';
   
   +------------+
   | nombre     |
   +------------+
   | Desarrollo |
   +------------+
   ```

   

6. Devuelve el nombre del departamento donde trabaja el empleado Pepe Ruiz Santana.

   ```sql
   SELECT d.nombre
   FROM departamento AS d, empleado AS e
   WHERE d.codigo = e.codigo_departamento AND e.nombre = 'Pepe' AND e.apellido1 = 'Ruiz' AND e.apellido2 = 'Santana';
   
   +------------------+
   | nombre           |
   +------------------+
   | Recursos Humanos |
   +------------------+
   ```

   

7. Devuelve un listado con los datos de los empleados que trabajan en el departamento de I+D. Ordena el resultado alfabéticamente.

   ```sql
   SELECT e.codigo, e.nif, e.nombre, e.apellido1, e.apellido2, e.codigo_departamento
   FROM empleado AS e, departamento AS d
   WHERE d.codigo = e.codigo_departamento AND d.nombre = 'I+D'
   ORDER BY e.nombre ASC;
   
   +--------+-----------+--------+-----------+-----------+---------------------+
   | codigo | nif       | nombre | apellido1 | apellido2 | codigo_departamento |
   +--------+-----------+--------+-----------+-----------+---------------------+
   |     10 | 46384486H | Diego  | Flores    | Salas     |                   5 |
   |      5 | 17087203C | Marcos | Loyola    | Méndez    |                   5 |
   +--------+-----------+--------+-----------+-----------+---------------------+
   ```

   

8. Devuelve un listado con los datos de los empleados que trabajan en el departamento de Sistemas, Contabilidad o I+D. Ordena el resultado alfabéticamente.

   ```sql
   SELECT e.codigo, e.nif, e.nombre, e.apellido1, e.apellido2, e.codigo_departamento
   FROM empleado AS e, departamento AS d
   WHERE d.codigo = e.codigo_departamento AND d.nombre IN ('Sistemas', 'Contabilidad', 'I+D')
   ORDER BY e.nombre ASC;
   
   +--------+-----------+---------+-----------+-----------+---------------------+
   | codigo | nif       | nombre  | apellido1 | apellido2 | codigo_departamento |
   +--------+-----------+---------+-----------+-----------+---------------------+
   |      2 | Y5575632D | Adela   | Salas     | Díaz      |                   2 |
   |      4 | 77705545E | Adrián  | Suárez    | NULL      |                   4 |
   |     10 | 46384486H | Diego   | Flores    | Salas     |                   5 |
   |      9 | 56399183D | Juan    | Gómez     | López     |                   2 |
   |      5 | 17087203C | Marcos  | Loyola    | Méndez    |                   5 |
   |      7 | 80576669X | Pilar   | Ruiz      | NULL      |                   2 |
   +--------+-----------+---------+-----------+-----------+---------------------+
   ```

   

9. Devuelve una lista con el nombre de los empleados que tienen los departamentos que no tienen un presupuesto entre 100000 y 200000 euros.

   ```sql
   SELECT e.nombre, e.apellido1, e.apellido2
   FROM empleado AS e, departamento AS d
   WHERE d.codigo = e.codigo_departamento AND d.presupuesto NOT BETWEEN 100000 AND 200000;
   
   +--------+-----------+-----------+
   | nombre | apellido1 | apellido2 |
   +--------+-----------+-----------+
   | Adolfo | Rubio     | Flores    |
   | Pepe   | Ruiz      | Santana   |
   | Marcos | Loyola    | Méndez    |
   | Diego  | Flores    | Salas     |
   +--------+-----------+-----------+
   ```

   

10. Devuelve un listado con el nombre de los departamentos donde existe algún empleado cuyo segundo apellido sea NULL. Tenga en cuenta que no debe mostrar nombres de departamentos que estén repetidos.

    ```sql
    SELECT DISTINCT(d.nombre)
    FROM departamento AS d, empleado AS e
    WHERE d.codigo = e.codigo_departamento AND e.apellido2 IS NULL;
    
    +--------------+
    | nombre       |
    +--------------+
    | Contabilidad |
    | Sistemas     |
    +--------------+
    ```
    
    

##### **Consultas multitabla** (Composición externa)

1. Devuelve un listado con todos los empleados junto con los datos de los departamentos donde trabajan. Este listado también debe incluir los empleados que no tienen ningún departamento asociado.

   ```sql
   SELECT e.codigo, e.nif, e.nombre, e.apellido1, e.apellido2, d.codigo AS codigo_departamento, d.nombre AS nombre_departamento, d.presupuesto, d.gastos
   FROM empleado AS e
   LEFT JOIN departamento AS d
   ON d.codigo = e.codigo_departamento;
   
   +--------+-----------+--------------+-----------+-----------+---------------------+---------------------+-------------+--------+
   | codigo | nif       | nombre       | apellido1 | apellido2 | codigo_departamento | nombre_departamento | presupuesto | gastos |
   +--------+-----------+--------------+-----------+-----------+---------------------+---------------------+-------------+--------+
   |      1 | 32481596F | Aarón        | Rivero    | Gómez     |                   1 | Desarrollo          |      120000 |   6000 |
   |      2 | Y5575632D | Adela        | Salas     | Díaz      |                   2 | Sistemas            |      150000 |  21000 |
   |      3 | R6970642B | Adolfo       | Rubio     | Flores    |                   3 | Recursos Humanos    |      280000 |  25000 |
   |      4 | 77705545E | Adrián       | Suárez    | NULL      |                   4 | Contabilidad        |      110000 |   3000 |
   |      5 | 17087203C | Marcos       | Loyola    | Méndez    |                   5 | I+D                 |      375000 | 380000 |
   |      6 | 38382980M | María        | Santana   | Moreno    |                   1 | Desarrollo          |      120000 |   6000 |
   |      7 | 80576669X | Pilar        | Ruiz      | NULL      |                   2 | Sistemas            |      150000 |  21000 |
   |      8 | 71651431Z | Pepe         | Ruiz      | Santana   |                   3 | Recursos Humanos    |      280000 |  25000 |
   |      9 | 56399183D | Juan         | Gómez     | López     |                   2 | Sistemas            |      150000 |  21000 |
   |     10 | 46384486H | Diego        | Flores    | Salas     |                   5 | I+D                 |      375000 | 380000 |
   |     11 | 67389283A | Marta        | Herrera   | Gil       |                   1 | Desarrollo          |      120000 |   6000 |
   |     12 | 41234836R | Irene        | Salas     | Flores    |                NULL | NULL                |        NULL |   NULL |
   |     13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |                NULL | NULL                |        NULL |   NULL |
   +--------+-----------+--------------+-----------+-----------+---------------------+---------------------+-------------+--------+
   ```

   

2. Devuelve un listado donde sólo aparezcan aquellos empleados que no tienen ningún departamento asociado.

   ```sql
   SELECT e.codigo, e.nif, e.nombre, e.apellido1, e.apellido2
   FROM empleado AS e
   LEFT JOIN departamento AS d
   ON e.codigo_departamento = d.codigo
   WHERE e.codigo_departamento IS NULL;
   
   +--------+-----------+--------------+-----------+-----------+
   | codigo | nif       | nombre       | apellido1 | apellido2 |
   +--------+-----------+--------------+-----------+-----------+
   |     12 | 41234836R | Irene        | Salas     | Flores    |
   |     13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |
   +--------+-----------+--------------+-----------+-----------+
   ```

   

3. Devuelve un listado donde sólo aparezcan aquellos departamentos que no tienen ningún empleado asociado.

   ```sql
   SELECT d.nombre
   FROM empleado AS e
   RIGHT JOIN departamento AS d
   ON e.codigo_departamento = d.codigo
   WHERE e.codigo_departamento IS NULL;
   
   +------------+
   | nombre     |
   +------------+
   | Proyectos  |
   | Publicidad |
   +------------+
   ```

   

4. Devuelve un listado con todos los empleados junto con los datos de los departamentos donde trabajan. El listado debe incluir los empleados que no tienen ningún departamento asociado y los departamentos que no tienen ningún empleado asociado. Ordene el listado alfabéticamente por el nombre del departamento.

   ```sql
   SELECT e.codigo, e.nif, e.nombre, e.apellido1, e.apellido2, d.codigo AS codigo_departamento, d.nombre AS nombre_departamento, d.presupuesto, d.gastos
   FROM empleado AS e
   LEFT JOIN departamento AS d
   ON e.codigo_departamento = d.codigo
   UNION
   SELECT e.codigo, e.nif, e.nombre, e.apellido1, e.apellido2, d.codigo AS codigo_departamento, d.nombre AS nombre_departamento, d.presupuesto, d.gastos
   FROM empleado AS e
   RIGHT JOIN departamento AS d
   ON e.codigo_departamento = d.codigo
   ORDER BY nombre_departamento ASC;
   
   +--------+-----------+--------------+-----------+-----------+---------------------+---------------------+-------------+--------+
   | codigo | nif       | nombre       | apellido1 | apellido2 | codigo_departamento | nombre_departamento | presupuesto | gastos |
   +--------+-----------+--------------+-----------+-----------+---------------------+---------------------+-------------+--------+
   |     12 | 41234836R | Irene        | Salas     | Flores    |                NULL | NULL                |        NULL |   NULL |
   |     13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |                NULL | NULL                |        NULL |   NULL |
   |      4 | 77705545E | Adrián       | Suárez    | NULL      |                   4 | Contabilidad        |      110000 |   3000 |
   |      1 | 32481596F | Aarón        | Rivero    | Gómez     |                   1 | Desarrollo          |      120000 |   6000 |
   |      6 | 38382980M | María        | Santana   | Moreno    |                   1 | Desarrollo          |      120000 |   6000 |
   |     11 | 67389283A | Marta        | Herrera   | Gil       |                   1 | Desarrollo          |      120000 |   6000 |
   |      5 | 17087203C | Marcos       | Loyola    | Méndez    |                   5 | I+D                 |      375000 | 380000 |
   |     10 | 46384486H | Diego        | Flores    | Salas     |                   5 | I+D                 |      375000 | 380000 |
   |   NULL | NULL      | NULL         | NULL      | NULL      |                   6 | Proyectos           |           0 |      0 |
   |   NULL | NULL      | NULL         | NULL      | NULL      |                   7 | Publicidad          |           0 |   1000 |
   |      3 | R6970642B | Adolfo       | Rubio     | Flores    |                   3 | Recursos Humanos    |      280000 |  25000 |
   |      8 | 71651431Z | Pepe         | Ruiz      | Santana   |                   3 | Recursos Humanos    |      280000 |  25000 |
   |      2 | Y5575632D | Adela        | Salas     | Díaz      |                   2 | Sistemas            |      150000 |  21000 |
   |      7 | 80576669X | Pilar        | Ruiz      | NULL      |                   2 | Sistemas            |      150000 |  21000 |
   |      9 | 56399183D | Juan         | Gómez     | López     |                   2 | Sistemas            |      150000 |  21000 |
   +--------+-----------+--------------+-----------+-----------+---------------------+---------------------+-------------+--------+
   ```

   

5. Devuelve un listado con los empleados que no tienen ningún departamento asociado y los departamentos que no tienen ningún empleado asociado. Ordene el listado alfabéticamente por el nombre del departamento.

   ```sql
   SELECT e.codigo, e.nif, e.nombre, e.apellido1, e.apellido2, d.codigo AS codigo_departamento, d.nombre AS nombre_departamento, d.presupuesto, d.gastos
   FROM empleado AS e
   LEFT JOIN departamento AS d
   ON e.codigo_departamento = d.codigo
   WHERE e.codigo_departamento IS NULL
   UNION
   SELECT e.codigo, e.nif, e.nombre, e.apellido1, e.apellido2, d.codigo AS codigo_departamento, d.nombre AS nombre_departamento, d.presupuesto, d.gastos
   FROM empleado AS e
   RIGHT JOIN departamento AS d
   ON e.codigo_departamento = d.codigo
   WHERE e.codigo_departamento IS NULL
   ORDER BY nombre_departamento ASC;
   
   +--------+-----------+--------------+-----------+-----------+---------------------+---------------------+-------------+--------+
   | codigo | nif       | nombre       | apellido1 | apellido2 | codigo_departamento | nombre_departamento | presupuesto | gastos |
   +--------+-----------+--------------+-----------+-----------+---------------------+---------------------+-------------+--------+
   |     12 | 41234836R | Irene        | Salas     | Flores    |                NULL | NULL                |        NULL |   NULL |
   |     13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |                NULL | NULL                |        NULL |   NULL |
   |   NULL | NULL      | NULL         | NULL      | NULL      |                   6 | Proyectos           |           0 |      0 |
   |   NULL | NULL      | NULL         | NULL      | NULL      |                   7 | Publicidad          |           0 |   1000 |
   +--------+-----------+--------------+-----------+-----------+---------------------+---------------------+-------------+--------+
   ```

   

**Consultas resumen**

1. Calcula la suma del presupuesto de todos los departamentos.

   ```sql
   SELECT SUM(presupuesto)
   FROM departamento;
   
   +------------------+
   | SUM(presupuesto) |
   +------------------+
   |          1035000 |
   +------------------+
   ```

2. Calcula la media del presupuesto de todos los departamentos.

   ```sql
   SELECT AVG(presupuesto)
   FROM departamento;
   
   +--------------------+
   | AVG(presupuesto)   |
   +--------------------+
   | 147857.14285714287 |
   +--------------------+
   ```

3. Calcula el valor mínimo del presupuesto de todos los departamentos.

   ```sql
   SELECT MIN(presupuesto)
   FROM departamento;
   
   +------------------+
   | MIN(presupuesto) |
   +------------------+
   |                0 |
   +------------------+
   ```

4. Calcula el nombre del departamento y el presupuesto que tiene asignado, del departamento con menor presupuesto.

   ```sql
   SELECT nombre, presupuesto
   FROM departamento
   ORDER BY presupuesto ASC
   LIMIT 1;
   
   +-----------+-------------+
   | nombre    | presupuesto |
   +-----------+-------------+
   | Proyectos |           0 |
   +-----------+-------------+
   ```

5. Calcula el valor máximo del presupuesto de todos los departamentos.

   ```sql
   SELECT MAX(presupuesto)
   FROM departamento;
   
   +------------------+
   | MAX(presupuesto) |
   +------------------+
   |           375000 |
   +------------------+
   ```

6. Calcula el nombre del departamento y el presupuesto que tiene asignado, del departamento con mayor presupuesto.

   ```sql
   SELECT nombre, presupuesto
   FROM departamento
   ORDER BY presupuesto DESC
   LIMIT 1;
   
   +--------+-------------+
   | nombre | presupuesto |
   +--------+-------------+
   | I+D    |      375000 |
   +--------+-------------+
   ```

7. Calcula el número total de empleados que hay en la tabla empleado.

   ```sql
   SELECT COUNT(codigo)
   FROM empleado;
   
   +---------------+
   | COUNT(codigo) |
   +---------------+
   |            13 |
   +---------------+
   ```
   
8. Calcula el número de empleados que no tienen NULL en su segundo apellido.

   ```sql
   SELECT COUNT(codigo)
   FROM empleado
   WHERE apellido2 IS NOT NULL;
   
   +---------------+
   | COUNT(codigo) |
   +---------------+
   |            11 |
   +---------------+
   ```
   
9. Calcula el número de empleados que hay en cada departamento. Tienes que devolver dos columnas, una con el nombre del departamento y otra con el número de empleados que tiene asignados.

   ```sql
   SELECT d.nombre, COUNT(e.codigo_departamento) AS numero_de_empleados
   FROM departamento AS d, empleado AS e
   WHERE d.codigo = e.codigo_departamento
   GROUP BY e.codigo_departamento;
   
   +------------------+---------------------+
   | nombre           | numero_de_empleados |
   +------------------+---------------------+
   | Desarrollo       |                   3 |
   | Sistemas         |                   3 |
   | Recursos Humanos |                   2 |
   | Contabilidad     |                   1 |
   | I+D              |                   2 |
   +------------------+---------------------+
   ```
   
10. Calcula el nombre de los departamentos que tienen más de 2 empleados. El resultado debe tener dos columnas, una con el nombre del departamento y otra con el número de empleados que tiene asignados.

    ```sql
    SELECT d.nombre, COUNT(e.codigo_departamento) AS numero_de_empleados
    FROM departamento AS d
    JOIN empleado AS e
    ON d.codigo = e.codigo_departamento
    GROUP BY e.codigo_departamento
    HAVING COUNT(e.codigo) > 2;
    
    +------------+---------------------+
    | nombre     | numero_de_empleados |
    +------------+---------------------+
    | Desarrollo |                   3 |
    | Sistemas   |                   3 |
    +------------+---------------------+
    ```
    
11. Calcula el número de empleados que trabajan en cada uno de los departamentos. El resultado de esta consulta también tiene que incluir aquellos departamentos que no tienen ningún empleado asociado.

    ```sql
    SELECT d.nombre, COUNT(e.codigo_departamento) AS numero_de_empleados
    FROM departamento AS d
    LEFT JOIN empleado AS e
    ON d.codigo = e.codigo_departamento
    GROUP BY d.codigo, d.nombre;
    
    +------------------+---------------------+
    | nombre           | numero_de_empleados |
    +------------------+---------------------+
    | Desarrollo       |                   3 |
    | Sistemas         |                   3 |
    | Recursos Humanos |                   2 |
    | Contabilidad     |                   1 |
    | I+D              |                   2 |
    | Proyectos        |                   0 |
    | Publicidad       |                   0 |
    +------------------+---------------------+
    ```
    
12. Calcula el número de empleados que trabajan en cada unos de los departamentos que tienen un presupuesto mayor a 200000 euros.

    ```sql
    SELECT d.nombre, COUNT(e.codigo_departamento) AS numero_de_empleados
    FROM departamento AS d, empleado AS e
    WHERE d.codigo = e.codigo_departamento AND d.presupuesto > 200000
    GROUP BY e.codigo_departamento;
    
    +------------------+---------------------+
    | nombre           | numero_de_empleados |
    +------------------+---------------------+
    | Recursos Humanos |                   2 |
    | I+D              |                   2 |
    +------------------+---------------------+
    ```
    
    
