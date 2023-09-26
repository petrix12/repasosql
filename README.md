# REPASO SQL

## Curso 1: Consultas en SQL para principiantes
+ URL: https://www.udemy.com/course/sql-desde-cero-curso-practico

1. Crear base de datos:
    ```sql
    CREATE DATABASE midb;
    ```
    + **Nota**: para este curso crearemos las bases de datos **world** y **employees**.
2. Mostrat bases de datos:
    ```sql
    SHOW DATABASES;
    ```
3. Crear usuario de base de datos:
    ```sql
    CREATE USER 'nuevo_usuario'@'localhost' IDENTIFIED BY 'password_del_usuario';
    ```
4. Establecer permisos a un usuario:
    ```sql
    -- Permisos al usuario nuevo_usuario sobre todas las bases de datos y todas las tablas
    GRANT ALL PRIVILEGES ON *.* TO 'nuevo_usuario'@'localhost';
    -- Permisos al usuario nuevo_usuario sobre todas las tablas de la base de datos midb
    GRANT ALL PRIVILEGES ON midb.* TO 'nuevo_usuario'@'localhost';
    ```
5. Actualizar los privilegios de los usuarios:
    ```sql
    FLUSH PRIVILEGES;
    ```
6. Ingresar a MySQL por consola:
    + $ mysql -uroot -p
    + **Nota**: La **u** en **uroot** significa **user** y **root** el **usuario**. El -p debe colocarse si el usuario fue creado con password.
7. Ingresar a una base de datos por consola:
    + mysql> use midb;
8. Importar una base de datos por consola que se encuentre en la carpeta **downloads** de **Windows**:
    + mysql> SOURCE Downloads\\midb.sql;
    + **Nota**: para este curso importaremos la base de datos **world.sql**, **employees** y **numpidb** ubicada en **soportes\curso1\world.sql**, **soportes\curso1\employees.sql** y **soportes\curso1\employees.sqlnumpidb.sql** respectivamente.
9. Salir de MySQL por consola:
    + mysql> exit
10. Seleccionar base de datos:
    ```sql
    USE midb
    ```
11. Mostrar tablas de la base de datos seleccionada:
    ```sql
    SHOW TABLES;
    ```
12. Ver la estructura de una tabla:
    ```sql
    DESCRIBE tabla_x;
    ```
13. Comentario de una lína:
    ```sql
    -- Este es un comentario de una línea en SQL
    ```
14. Comentario de varias líneas:
    ```sql
    /*
        Este es
        un comentario
        de varias
        líneas
    */
    ```
14. Seleccionar todos los campos de una tabla:
    ```sql
    SELECT * FROM tabla_x;
    ```
15. Seleccionar un campo de una tabla:
    ```sql
    SELECT campo_x FROM tabla_x;
    ```
16. Seleccionar varios campos de una tabla:
    ```sql
    SELECT campo_a, campo_b, campo_c FROM tabla_X;
    ```
17. Seleccionar campos de una tabla con alias:
    ```sql
    SELECT campo_a AS otro_nombre, campo_b AS "Nombre con espacios" FROM tabla_x;
    ```
18. Seleccionar valores unicos de un determinado campo en una tabla:
    ```sql
    SELECT DISTINCT campo_x FROM tabla_x;
    ```
    + **Nota**: si se colocan varios campos, estos deberán ser iguales respectivamentes a otros para que sean filtrados.
19. Ejemplos de operadores aritméticos (+, -, *, /, DIV, MOD):
    ```sql
    -- OPERADORES ARITMÉTICOS
    -- Suma
    SELECT 3 + 4;
    -- Resta
    SELECT 5 - 8;
    -- Multiplicación
    SELECT 2 * 6;
    -- División
    SELECT 1 / 7;
    -- División entera
    SELECT 9 DIV 4;
    -- Resto de una división
    SELECT mod(41, 5);
    -- Calculos sobre una consulta
    SELECT campo_a, (campo_b / campo_c) AS "Relacion de B/C" FROM tabla_X;
    ```
20. Ejemplos de operadores de comparación (<, <=, >, >=, =, !=):
    ```sql
    -- OPERADORES DE COMPARACIÓN (Resulatos: 1: true, 0: false)
    -- Menor
    SELECT 4 < 5;
    -- Menor o igual
    SELECT 7 <= 3;
    -- Mayor
    SELECT 1 > 9;
    -- Mayor o igual
    SELECT 8 >= 2;
    -- Igual
    SELECT 12 = 11;
    -- Distinto
    SELECT 6 != 10;
    SELECT FALSE != TRUE;
    SELECT 'HOLA' != 'BYE';
    ```
21. Ejemplos de operadores lógicos (AND, OR, NOT):
    ```sql
    SELECT TRUE AND FALSE;
    SELECT FALSE OR TRUE;
    SELECT NOT TRUE;
    SELECT 1 AND 0;
    SELECT 0 OR 1;
    SELECT NOT 1;
    ```
22. Ejemplos de filtros con WHERE en las consultas:
    ```sql
    SELECT * FROM tabla_x WHERE campo_a = 12;
    SELECT * FROM tabla_x WHERE campo_a > 3 AND campo_b = "valor_x";

    SELECT * FROM tabla_x WHERE campo_a != 'M';
    /*
        La siguiente consulta arroja el mismo resultado que la anterior pero es un poco menos eficiente
        porque tiene que hacer un paso más: primero calcula el valor booleano de campo_a = 'M' y
        luego niega su valor, en cambio la otra es un paso más directa.
    */
    SELECT * FROM tabla_x WHERE NOT campo_a = 'M';

    -- Uso de comodines % (varios caracteres) y _ (un solo caracter)
    SELECT * FROM tabla_x WHERE campo_y LIKE "G%";
    SELECT * FROM tabla_x WHERE campo_y LIKE "_e%";

    -- Uso de comodines con fecha
    SELECT * FROM tabla_x WHERE campo_fecha LIKE "1972-__-12";
    ```
23. Obtener registros en donde unos de sus campos se encuentren dentro de un rango (Operador BETWEEN):
    ```sql
    -- El rango a usar BETWEEN debe ir de menor a mayor (Se usa para rangos numéricos y de fecha)
    SELECT * FROM tabla_x WHERE campo_x BETWEEN 112 AND 217;
    -- La cosulta anterior arrojará el mismo resultado que la siguiente
    SELECT * FROM tabla_z WHERE campo_x >= 112 AND campo_x <= 217;
    
    SELECT * FROM tabla_x WHERE campo_x NOT BETWEEN 112 AND 217;
    -- La cosulta anterior arrojará el mismo resultado que la siguiente
    SELECT * FROM tabla_x WHERE campo_x < 112 OR campo_x > 217;

    SELECT * FROM tabla_x WHERE campo_fecha_x BETWEEN "1972-01-01" AND "1972-12-31";
    ```
24. Ejemplo de uso del operador IN:
    ```sql
    SELECT * FROM tabla_x WHERE campo_z IN ("Valor_1", "Valor_2");
    -- La siguiente consulta arroja el mismo resultado que la anterior
    SELECT * FROM tabla_x WHERE campo_z LIKE "Valor_1" OR campo_z LIKE "Valor_2";
    ```
25. Ejemplo de uso de **DATEDIFF**:
    + Encontrar las personas que tengan una edad mayor a 60 años
    ```sql
    SELECT 
        campo_nombre AS nombre, 
        campo_apellido AS apellido, 
        DATEDIFF(CURRENT_TIMESTAMP, campo_fecha_nacimiento) / 365 AS edad
    FROM tabla_personas 
    WHERE 
        DATEDIFF(CURRENT_TIMESTAMP, campo_fecha_nacimiento) >= 60 AND
        DATEDIFF(CURRENT_TIMESTAMP, campo_fecha_nacimiento) < 61;
    -- Nota: existen formas más eficientes de llegar a este mismo resultado
    ```
26. Ordenar tabla por campos:
    ```sql
    SELECT * FROM tabla_x ORDER BY campo_2;
    -- La siguiente consulta es equivalente a la anterior, ya que por defecto se ordena de forma ascendente
    SELECT * FROM tabla_x ORDER BY campo_2 ASC;
    -- La siguiente consulta ordena de manera descendente, contraria a la anterior
    SELECT * FROM tabla_x ORDER BY campo_2 DESC;
    -- La siguiente consulta desordena los resultados
    SELECT * FROM tabla_x ORDER BY RAND();

    SELECT * FROM tabla_x WHERE campo_3 LIKE "Pe%" ORDER BY campo_2;
    ```
27. Ignorar o buscar los registros NULL:
    ```sql
    SELECT * FROM tabla_x WHERE campo_4 IS NULL;
    -- La siguiente expresión es equivalente a la anterior
    SELECT * FROM tabla_x WHERE NOT campo_4 IS NOT NULL;

    SELECT * FROM tabla_x WHERE campo_4 IS NOT NULL;
    -- La siguiente expresión es equivalente a la anterior
    SELECT * FROM tabla_x WHERE NOT campo_4 IS NULL;
    ```
28. Limitar las busquedas de registros:
    ```sql
    -- Muestra los primeros 10 registros
    SELECT * FROM tabla_x ORDER BY campo_2 DESC LIMIT 10;
    -- Muestra igualmente los primeros 10 registros
    SELECT * FROM tabla_x ORDER BY campo_2 DESC LIMIT 0, 10;
    -- Muestra los primeros 10 registros a partir del registro 11
    SELECT * FROM tabla_x ORDER BY campo_2 DESC LIMIT 10, 10;
    -- Muestra los primeros 10 registros a partir del registro 21
    SELECT * FROM tabla_x ORDER BY campo_2 DESC LIMIT 20, 10;
    ```
29. Obtener los 5 departamentos con los nombres más largos de la tabla_x:
    ```sql
    SELECT * FROM tabla_x ORDER BY LENGTH(campo_departamento) LIMIT 5;
    ```
30. Ejemplo de funciones de agregación (SUM, AVG, MIN, MAX, STDDEV):
    ```sql
    -- Sumar los valores de un determinado campo de todos los registros de una tabla
    SELECT SUM(campo_numerico) AS 'Total' FROM tabla_x;

    -- Obtener el promedio, el menor valor y el mayor valor de una tabla de notas
    SELECT 
        AVG(nota) AS 'promedio de notas',
        MIN(nota) AS 'nota más baja',
        MAX(nota) AS 'nota más alta'
    FROM tabla_de_notas;

    -- Obtener la desviación estandar
    SELECT STDDEV(nota) AS 'Desviación Estandar' FROM tabla_de_notas;

    -- Un ejemplo de funciones de agregación un poco más elaborado
    SELECT 
        ROUND(AVG(nota) - STDDEV(nota)) AS 'Límite inferior',
        ROUND(AVG(nota) + STDDEV(nota)) AS 'Límite superior'
    FROM tabla_de_notas;

    -- Obtener el total de registros de una tabla
    SELECT COUNT(*) AS 'total de registros' FROM tabla_x;
    ```
31. Ejemplo de uso de la clausula **GROUP BY**:
    ```sql
    -- Encontrar la superficie total de cada continente
    SELECT continente, SUM(superficie) AS 'área total' FROM paises GROUP BY continente;
    ```
32. Ejemplo de uso de la clausula **HAVING**:
    ```sql
    -- Mostrar los continentes con esperanza de vida media mayor a 70 años
    SELECT 
        continente, AVG(EsperanzaVida) AS 'esperanza de vida' 
    FROM paises GROUP BY continente HAVING AVG(EsperanzaVida) > 70;
    ```
    + **Nota**: **HAVING** va despues de un **GROUP BY**.
33. Estructura básica de un **JOIN**:
    ```sql
    -- INNER JOIN: combinación de ambas tablas por igual (se toman los elementos de ambas tablas)
    SELECT * FROM tabla_x x JOIN tabla_y y ON x.campo_tabla_x = y.campo_tabla_y;

    -- LEFT JOIN: predomina la tabla izquierda (se toman lo elementos de la tabla_x)
    SELECT * FROM tabla_x x LEFT JOIN tabla_y y ON x.campo_tabla_x = y.campo_tabla_y;

    -- RIGHT JOIN: predomina la tabla derecha (se toman lo elementos de la tabla_y)
    SELECT * FROM tabla_x x RIGHT JOIN tabla_y y ON x.campo_tabla_x = y.campo_tabla_y;
    ```
    + **Nota**: por defecto al aplicar un **JOIN** se esta aplicando un **INNER JOIN**.
34. Ejemplo de uso de **INNER JOIN**:
    ```sql
    /*
        Campos de la tabla estudiantes:
            id
            nombre
            apellido
            documento
            edad
            seccion_id
        Campos de la tabla secciones:
            id
            nombre
            descriptor
    */

    -- 1) Relacionar la tabla estudiantes con la tabla secciones
    SELECT * FROM estudiantes e
    JOIN secciones s
    ON e.seccion_id = s.id

    -- 2) Obtener los nombres de los estudiantes con su sección
    SELECT CONCAT(e.nombre, ' ', e.apellido) AS "Nombre", s.id AS "Sección"
    FROM estudiantes e INNER JOIN secciones s
    ON e.seccion_id = s.id
    ```
35. **JOIN** con multiples tablas:
    ```sql
    /*
        Campos de la tabla employees:
            emp_no
            birth_date
            first_name
            last_name
            gender
            hire_date
        Campos de la tabla dept_emp:
            emp_no
            dept_no
            from_date
            to_date
        Campos de la tabla departments:
            dept_no
            dept_name
        Campos de la tabla salaries
            emp_no
            salary
            from_date
            to_date
    */

    -- 1) Obtener una lista de los empleados con el departamento al cual pertenece
    SELECT e.first_name AS 'Nombre', e.last_name AS 'Apellido', d.dept_name AS 'Departamento'  
    FROM employees e 
    JOIN dept_emp de ON e.emp_no = de.emp_no
    JOIN departments d ON de.dept_no = d.dept_no;

    -- 2) Obtener una lista de los empleados con el departamento al cual pertenece y también el salario
    SELECT 
        e.first_name AS 'Nombre', 
        e.last_name AS 'Apellido', 
        d.dept_name AS 'Departamento',
        s.salary AS 'Salario'
    FROM employees e 
    JOIN dept_emp de ON e.emp_no = de.emp_no
    JOIN departments d ON de.dept_no = d.dept_no
    JOIN salaries s ON e.emp_no = s.emp_no;

    -- 3) Determinar el salario promedio de cada departamento y ordenar los resultados de mayor a menor
    SELECT
        d.dept_name AS 'Departamento',
        AVG(s.salary) AS 'Salario promedio'
    FROM departments d
    JOIN dept_emp de ON d.dept_no = de.dept_no
    JOIN salaries s ON de.emp_no = s.emp_no
    GROUP BY d.dept_name ORDER BY AVG(s.salary) DESC;
    ```
36. Unión de consultas:
    ```sql
    /*
        Campos de la tabla country:
            Code            Name        Continent       Region
            SurfaceArea     IndepYear   Population      LifeExpectancy
	        GNP             GNPOld      LocalName       GovernmentForm
	        HeadOfState	    Capital     Code2
    */
    
    -- Consulta 1:
    SELECT Name, Continent FROM country WHERE Population > 150000000;
    
    -- Consulta 2:
    SELECT Name, Continent FROM country WHERE SurfaceArea > 9000000;

    -- Unión de la consulta 1 con la consulta 2:
    SELECT Name, Continent FROM country WHERE Population > 150000000
    UNION ALL
    SELECT Name, Continent FROM country WHERE SurfaceArea > 9000000;

    -- Unión de la consulta 1 con la consulta 2 sin la repetición de registros:
    SELECT Name, Continent FROM country WHERE Population > 150000000
    UNION
    SELECT Name, Continent FROM country WHERE SurfaceArea > 9000000;
    ```
37. Ejemplos de subconsultas (subquery):
    ```sql
    -- Ejemplos de estructura de consultas con subconsultas:
    -- Ejemplo 1 (Subconsulta en SELECT):
    SELECT columna, (SELECT subconsulta) AS alias FROM tabla;
    -- Ejemplo 2 (Subconsulta en WHERE):
    SELECT columna FROM tabla WHERE columna IN (SELECT subconsulta);
    -- Ejemplo 3 (Subconsulta en HAVING):
    SELECT columna FROM tabla GROUP BY columna HAVING columna IN (SELECT subconsulta);
    -- Ejemplo 4 (Subconsulta en FROM):
    SELECT columna FROM (subconsulta);
    -- Ejemplo 5 (Subconsulta con EXISTS):
    SELECT columna FROM tabla WHERE EXISTS (SELECT subconsulta);

    /*
        BD: world:
        Campos de la tabla country:
            Code            Name            Continent       Region
            SurfaceArea     IndepYear       Population      LifeExpectancy
	        GNP             GNPOld          LocalName       GovernmentForm
	        HeadOfState	    Capital         Code2
        Campos de la tabla city:
            Name            CountryCode     District        Population
        Campos de la tabla countrylanguage:
            CountryCode     Language        IsOfficial      Percentage

        BD: employees:
        Campos de la tabla salaries:
            emp_no          salary          from_date       to_date
        Campos de la tabla employees:
            emp_no          birth_date      first_name      last_name
            gender          hire_date

    */

    -- Subconsulta con la clausula EXISTS:
    SELECT Name FROM country WHERE EXISTS (
        SELECT * FROM city 
        WHERE city.CountryCode = country.Code AND city.Population > 8000000
    );
    /* 
        Nota: el EXISTS transforma la subconsulta en un booleano, es decir si esta condición no se cumple 
        entonces se filtra el campo Name
    */

    -- Subconsulta en clausula SELECT:
    -- Obtener el lenguaje más hablado por país y su porcentaje:
    SELECT
        Name AS "País",
        (
            SELECT Language 
            FROM countrylanguage
            WHERE CountryCode = country.Code ORDER BY Percentage DESC LIMIT 1
        ) AS "Lenguaje",
        (
            SELECT Percentage 
            FROM countrylanguage
            WHERE CountryCode = country.Code ORDER BY Percentage DESC LIMIT 1
        ) AS "Porcentaje"
    FROM country;
    /*
        Nota 1: existen formas más eficientes de realizar estas consultas.
        Nota 2: las subconsultas en la clausula SELECT deben arrojar un solo campo de un solo registro
    */

    -- Subconsulta en clausula FROM:
    SELECT * FROM (SELECT Name, Region, LifeExpectancy FROM country) AS tabla_virtual WHERE LifeExpectancy > 80;
    
    -- Subconsulta en clausula WHERE:
    -- Obtener todos los paises de habla español
    SELECT Name FROM country WHERE Code IN (
        SELECT CountryCode FROM countrylanguage WHERE Language = 'Spanish'
    );

    -- Subconsulta en clausula HAVING:
    -- Obtener los paises que tengan más de tres idiomas
    SELECT Name FROM country c HAVING (
        SELECT COUNT(*) 
        FROM countrylanguage cl
        WHERE cl.CountryCode = c.Code
    ) > 3;

    -- Ejemplos varios:
    -- 1) Obtener los empleados con salarios superiores al promedio:
    SELECT 
        emp_no AS "ID empleado", 
        (
            SELECT CONCAT(first_name, ' ', last_name) 
            FROM employees e
            WHERE s.emp_no = e.emp_no
        ) AS "Empleado",
        salary AS "Salario" 
    FROM salaries s WHERE salary > (
        SELECT AVG(salary) FROM salaries
    );

    -- 2) Obtener los paises con población mayor a la promedio:
    SELECT Name, Population FROM country WHERE Population > (
        SELECT AVG(Population) FROM country
    );

    -- 3) Obtener los paises que tienen un área superior al promedio de su continente
    SELECT 
        Name, 
        SurfaceArea 
    FROM country c1 
    WHERE SurfaceArea > (
        SELECT AVG(SurfaceArea) 
        FROM country c2 
        WHERE c1.Continent = c2.Continent
    );
    ```
38. mmm




    ```sql

    ```