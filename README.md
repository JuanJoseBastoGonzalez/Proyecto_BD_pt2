Consultas sobre una tabla
1. Devuelve un listado con el primer apellido, segundo apellido y el nombre de
    todos los alumnos. El listado deberá estar ordenado alfabéticamente de
    menor a mayor por el primer apellido, segundo apellido y nombre.

  ```sql
  SELECT apellido1, apellido2, nombre
  FROM alumno
  ORDER BY apellido1, apellido2, nombre;
  +-----------+------------+--------+
  | apellido1 | apellido2  | nombre |
  +-----------+------------+--------+
  | García    | López      | Juan   |
  | López     | Fernández  | Ana    |
  | Martínez  | Pérez      | María  |
  | Sánchez   | Gómez      | Carlos |
  +-----------+------------+--------+
  
  ```

  

2. Averigua el nombre y los dos apellidos de los alumnos que no han dado de
    alta su número de teléfono en la base de datos.

  ```sql
  SELECT dat.apellido1, dat.apellido2, dat.nombre
  FROM datos dat
  JOIN alumno ON dat.id_datos = alumno.id_datos
  WHERE id_contacto IS NULL;
  Program did not output anything!
  ```

  

3. Devuelve el listado de los alumnos que nacieron en 1999.

   ```sql
   SELECT nombre, apellido1, apellido2
   FROM datos
   JOIN alumno ON datos.id_datos = alumno.id_datos
   WHERE YEAR(fecha_nacimiento) = 1999;
   +--------+-----------+-----------+
   | nombre | apellido1 | apellido2 |
   +--------+-----------+-----------+
   | Juan   | García    | López     |
   +--------+-----------+-----------+
   
   ```

   

4. Devuelve el listado de profesores que no han dado de alta su número de
    teléfono en la base de datos y además su nif termina en K.

  ```sql
  SELECT id_profesor, nif, id_datos, id_contacto, id_ubicacion, fecha_nacimiento, sexo, id_departamento
  FROM profesor
  WHERE id_contacto IS NULL AND RIGHT(nif, 1) = 'K';
  Program did not output anything!
  ```

  

5. Devuelve el listado de las asignaturas que se imparten en el primer
    cuatrimestre, en el tercer curso del grado que tiene el identificador 7.
    Consultas multitabla (Composición interna)

  ```sql
  
  SELECT asignatura.id_asignatura, asignatura.cuatrimestre, detalle_asignatura.nombre
  FROM asignatura
  JOIN detalle_asignatura ON asignatura.id_detalle = detalle_asignatura.id_detalle
  WHERE asignatura.cuatrimestre = 'Primer Cuatrimestre' AND detalle_asignatura.curso = 'Tercer Curso' AND asignatura.id_grado = 7;
  
  Program did not output anything!
  ```

  

6. Devuelve un listado con los datos de todas las alumnas que se han
    matriculado alguna vez en el Grado en Ingeniería Informática (Plan 2015).

  ```sql
  SELECT datos.nombre, datos.apellido1, datos.apellido2, alumno.sexo
  FROM alumno
  JOIN datos ON alumno.id_datos = datos.id_datos
  JOIN detalle_matricula ON alumno.id_alumno = detalle_matricula.id_alumno
  JOIN asignatura ON detalle_matricula.id_asignatura = asignatura.id_asignatura
  JOIN grado ON asignatura.id_grado = grado.id_grado
  JOIN curso ON detalle_matricula.id_curso = curso.id_curso
  WHERE grado.nombre = 'Ingeniería Informática' AND YEAR(curso.año_inicio) = 2015
  GROUP BY alumno.id_alumno
  HAVING alumno.sexo = 'Femenino';
  Program did not output anything!
  ```

Consultas multitabla (Composición interna)
1. Devuelve un listado con los datos de todas las alumnas que se han
    matriculado alguna vez en el Grado en Ingeniería Informática (Plan 2015).

  ```sql
  
  SELECT datos.nombre, datos.apellido1, datos.apellido2
  FROM datos
  JOIN alumno ON datos.id_datos =alumno.id_datos
  JOIN detalle_matricula ON alumno.id_alumno = detalle_matricula.id_alumno
  JOIN asignatura ON detalle_matricula.id_asignatura = asignatura.id_asignatura
  JOIN grado ON asignatura.id_grado = grado.id_grado
  WHERE grado.nombre = 'Ingeniería Informática' AND YEAR(curdate()) = 2015;
  Program did not output anything!
  ```

  

2. Devuelve un listado con todas las asignaturas ofertadas en el Grado en
    Ingeniería Informática (Plan 2015).

  ```sql
  SELECT detalle_asignatura.nombre
  FROM detalle_asignatura
  JOIN asignatura ON detalle_asignatura.id_detalle = asignatura.id_detalle
  JOIN grado ON asignatura.id_grado = grado.id_grado
  WHERE grado.nombre = 'Ingeniería Informática' AND YEAR(curdate()) = 2015;
  Program did not output anything!
  ```

  

3. Devuelve un listado de los profesores junto con el nombre del
    departamento al que están vinculados. El listado debe devolver cuatro
    columnas, primer apellido, segundo apellido, nombre y nombre del
    departamento. El resultado estará ordenado alfabéticamente de menor a
    mayor por los apellidos y el nombre.

  ```sql
  SELECT datos.apellido1, datos.apellido2, datos.nombre, departamento.nombre AS nombre_departamento
  FROM profesor
  JOIN datos ON profesor.id_datos = datos.id_datos
  JOIN departamento ON profesor.id_departamento = departamento.id_departamento
  ORDER BY datos.apellido1, datos.apellido2, datos.nombre;
  +-----------+------------+--------+------------------------------+
  | apellido1 | apellido2  | nombre | nombre_departamento          |
  +-----------+------------+--------+------------------------------+
  | García    | López      | Juan   | Departamento de Informática  |
  | López     | Fernández  | Ana    | Departamento de Historia     |
  | Martínez  | Pérez      | María  | Departamento de Matemáticas  |
  | Sánchez   | Gómez      | Carlos | Departamento de Biología     |
  +-----------+------------+--------+------------------------------+
  ```

  

4. Devuelve un listado con el nombre de las asignaturas, año de inicio y año de
    fin del curso escolar del alumno con nif 26902806M.

  ```sql
  SELECT detalle_asignatura.nombre, YEAR(curso.año_inicio) AS año_inicio, YEAR(curso.año_fin) AS año_fin
  FROM detalle_matricula
  JOIN alumno ON detalle_matricula.id_alumno = alumno.id_alumno
  JOIN asignatura ON detalle_matricula.id_asignatura = asignatura.id_asignatura
  JOIN detalle_asignatura ON asignatura.id_detalle = detalle_asignatura.id_detalle
  JOIN curso ON detalle_matricula.id_curso = curso.id_curso
  WHERE alumno.nif = '26902806M';
  Program did not output anything!
  ```

  

5. Devuelve un listado con el nombre de todos los departamentos que tienen
    profesores que imparten alguna asignatura en el Grado en Ingeniería
    Informática (Plan 2015).

  ```sql
  SELECT DISTINCT departamento.nombre
  FROM profesor
  JOIN departamento ON profesor.id_departamento = departamento.id_departamento
  JOIN asignatura ON profesor.id_profesor = asignatura.id_profesor
  JOIN grado ON asignatura.id_grado = grado.id_grado
  WHERE grado.nombre = 'Ingeniería Informática' AND YEAR(curdate()) = 2015;
  Program did not output anything!
  ```

  

6. Devuelve un listado con todos los alumnos que se han matriculado en
    alguna asignatura durante el curso escolar 2018/2019.  

  ```sql
  SELECT dat.nombre, dat.apellido1, dat.apellido2
  FROM datos dat
  JOIN alumno ON dat.id_datos = alumno.id_datos
  JOIN detalle_matricula ON alumno.id_alumno = detalle_matricula.id_alumno
  JOIN curso ON detalle_matricula.id_curso = curso.id_curso
  WHERE YEAR(curso.año_inicio) = 2018 AND YEAR(curso.año_fin) = 2019;
  +--------+-----------+-----------+
  | nombre | apellido1 | apellido2 |
  +--------+-----------+-----------+
  | Juan   | García    | López     |
  +--------+-----------+-----------+
  ```

  Consultas multitabla (Composición externa)
  Resuelva todas las consultas utilizando las cláusulas LEFT JOIN y RIGHT JOIN.

  1. Devuelve un listado con los nombres de todos los profesores y los

~~~sql
departamentos que tienen vinculados. El listado también debe mostrar
aquellos profesores que no tienen ningún departamento asociado. El listado
debe devolver cuatro columnas, nombre del departamento, primer apellido,
segundo apellido y nombre del profesor. El resultado estará ordenado
alfabéticamente de menor a mayor por el nombre del departamento,
apellidos y el nombre.

```
SELECT departamento.nombre AS nombre_departamento, datos.apellido1, datos.apellido2, datos.nombre
FROM profesor
LEFT JOIN departamento ON profesor.id_departamento = departamento.id_departamento
JOIN datos ON profesor.id_datos = datos.id_datos
ORDER BY nombre_departamento, datos.apellido1, datos.apellido2, datos.nombre;
+------------------------------+-----------+------------+--------+
| nombre_departamento          | apellido1 | apellido2  | nombre |
+------------------------------+-----------+------------+--------+
| Departamento de Biología     | Sánchez   | Gómez      | Carlos |
| Departamento de Historia     | López     | Fernández  | Ana    |
| Departamento de Informática  | García    | López      | Juan   |
| Departamento de Matemáticas  | Martínez  | Pérez      | María  |
+------------------------------+-----------+------------+--------+

```
~~~


​    

  2. Devuelve un listado con los profesores que no están asociados a un

~~~sql
departamento.

```
SELECT datos.apellido1, datos.apellido2, datos.nombre
FROM profesor
LEFT JOIN departamento ON profesor.id_departamento = departamento.id_departamento
JOIN datos ON profesor.id_datos = datos.id_datos
WHERE departamento.id_departamento IS NULL;
Program did not output anything!
```
~~~


​    

  3. Devuelve un listado con los departamentos que no tienen profesores

~~~sql
asociados.

```
SELECT departamento.nombre
FROM departamento
LEFT JOIN profesor ON departamento.id_departamento = profesor.id_departamento
WHERE profesor.id_departamento IS NULL;
Program did not output anything!

```
~~~


​    

  4. Devuelve un listado con los profesores que no imparten ninguna asignatura.

     ```sql
     SELECT datos.apellido1, datos.apellido2, datos.nombre
     FROM profesor
     LEFT JOIN asignatura ON profesor.id_profesor = asignatura.id_profesor
     JOIN datos ON profesor.id_datos = datos.id_datos
     WHERE asignatura.id_asignatura IS NULL;
     Program did not output anything!
     ```

     

  5. Devuelve un listado con las asignaturas que no tienen un profesor asignado.

     ```sql
     SELECT detalle_asignatura.nombre
     FROM detalle_asignatura
     LEFT JOIN asignatura ON detalle_asignatura.id_detalle = asignatura.id_detalle
     WHERE asignatura.id_profesor IS NULL;
     
     Program did not output anything!
     ```

     

  6. Devuelve un listado con todos los departamentos que tienen alguna

    asignatura que no se haya impartido en ningún curso escolar. El resultado
    debe mostrar el nombre del departamento y el nombre de la asignatura que
    no se haya impartido nunca.

```sql
SELECT departamento.nombre AS nombre_departamento, detalle_asignatura.nombre AS nombre_asignatura
FROM departamento
JOIN profesor ON departamento.id_departamento = profesor.id_departamento
JOIN asignatura ON profesor.id_profesor = asignatura.id_profesor
JOIN detalle_asignatura ON asignatura.id_detalle = detalle_asignatura.id_detalle
LEFT JOIN detalle_matricula ON asignatura.id_asignatura = detalle_matricula.id_asignatura
WHERE detalle_matricula.id_matricula IS NULL;
Program did not output anything!
```

Consultas resumen
1. Devuelve el número total de alumnas que hay.

   ```sql
   SELECT COUNT(*)
   FROM alumno
   WHERE sexo = 'F';
   +----------+
   | COUNT(*) |
   +----------+
   |        2 |
   +----------+
   
   ```

   

2. Calcula cuántos alumnos nacieron en 1999.

   ```sql
   SELECT COUNT(*) AS numero_alumnos
   FROM alumno
   WHERE YEAR(fecha_nacimiento) = 1999;
   +----------------+
   | numero_alumnos |
   +----------------+
   |              1 |
   +----------------+
   
   ```

   

3. Calcula cuántos profesores hay en cada departamento. El resultado sólo
    debe mostrar dos columnas, una con el nombre del departamento y otra
    con el número de profesores que hay en ese departamento. El resultado
    sólo debe incluir los departamentos que tienen profesores asociados y
    deberá estar ordenado de mayor a menor por el número de profesores.

  ```sql
  SELECT departamento.nombre, COUNT(profesor.id_profesor) AS num_profesores
  FROM departamento
  LEFT JOIN profesor ON departamento.id_departamento = profesor.id_departamento
  GROUP BY departamento.nombre
  ORDER BY num_profesores DESC;
  +------------------------------+----------------+
  | nombre                       | num_profesores |
  +------------------------------+----------------+
  | Departamento de Informática  |              1 |
  | Departamento de Matemáticas  |              1 |
  | Departamento de Biología     |              1 |
  | Departamento de Historia     |              1 |
  +------------------------------+----------------+
  ```

  

4. Devuelve un listado con todos los departamentos y el número de profesores
    que hay en cada uno de ellos. Tenga en cuenta que pueden existir
    departamentos que no tienen profesores asociados. Estos departamentos
    también tienen que aparecer en el listado.

  ```sql
  SELECT departamento.nombre, COUNT(profesor.id_profesor) AS num_profesores
  FROM departamento
  LEFT JOIN profesor ON departamento.id_departamento = profesor.id_departamento
  GROUP BY departamento.nombre;
  +------------------------------+----------------+
  | nombre                       | num_profesores |
  +------------------------------+----------------+
  | Departamento de Informática  |              1 |
  | Departamento de Matemáticas  |              1 |
  | Departamento de Biología     |              1 |
  | Departamento de Historia     |              1 |
  +------------------------------+----------------+
  
  ```

  

5. Devuelve un listado con el nombre de todos los grados existentes en la base
    de datos y el número de asignaturas que tiene cada uno. Tenga en cuenta

que pueden existir grados que no tienen asignaturas asociadas. Estos grados
también tienen que aparecer en el listado. El resultado deberá estar
ordenado de mayor a menor por el número de asignaturas.

```sql
SELECT grado.nombre AS nombre_grado, COUNT(asignatura.id_asignatura) AS num_asignaturas
FROM grado
LEFT JOIN asignatura ON grado.id_grado = asignatura.id_grado
GROUP BY grado.nombre
ORDER BY num_asignaturas DESC;
+--------------------------+-----------------+
| nombre_grado             | num_asignaturas |
+--------------------------+-----------------+
| Ingeniería Informática   |               2 |
| Matemáticas              |               2 |
| Biología                 |               0 |
| Historia                 |               0 |
+--------------------------+-----------------+
```



6. Devuelve un listado con el nombre de todos los grados existentes en la base
  de datos y el número de asignaturas que tiene cada uno, de los grados que
  tengan más de 40 asignaturas asociadas.

  ```sql
  SELECT grado.nombre AS nombre_grado, COUNT(asignatura.id_asignatura) AS num_asignaturas
  FROM grado
  JOIN asignatura ON grado.id_grado = asignatura.id_grado
  GROUP BY grado.nombre
  HAVING num_asignaturas > 40;
  Program did not output anything!
  ```

  

7. Devuelve un listado que muestre el nombre de los grados y la suma del
  número total de créditos que hay para cada tipo de asignatura. El resultado
  debe tener tres columnas: nombre del grado, tipo de asignatura y la suma
  de los créditos de todas las asignaturas que hay de ese tipo. Ordene el
  resultado de mayor a menor por el número total de crédidos.

  ```sql
  
  SELECT grado.nombre AS nombre_grado, detalle_asignatura.tipo, SUM(detalle_asignatura.creditos) AS total_creditos
  FROM grado
  LEFT JOIN asignatura ON grado.id_grado = asignatura.id_grado
  LEFT JOIN detalle_asignatura ON asignatura.id_detalle = detalle_asignatura.id_detalle
  GROUP BY grado.nombre, detalle_asignatura.tipo
  ORDER BY total_creditos DESC;
  
  
  +--------------------------+-------------+----------------+
  | nombre_grado             | tipo        | total_creditos |
  +--------------------------+-------------+----------------+
  | Ingeniería Informática   | Obligatoria |             12 |
  | Matemáticas              | Obligatoria |             12 |
  | Biología                 | NULL        |           NULL |
  | Historia                 | NULL        |           NULL |
  +--------------------------+-------------+----------------+
  ```

  

8. Devuelve un listado que muestre cuántos alumnos se han matriculado de
  alguna asignatura en cada uno de los cursos escolares. El resultado deberá
  mostrar dos columnas, una columna con el año de inicio del curso escolar y
  otra con el número de alumnos matriculados.

  ```sql
  SELECT curso.año_inicio, COUNT(detalle_matricula.id_alumno) AS num_alumnos_matriculados
  FROM curso
  LEFT JOIN detalle_matricula ON curso.id_curso = detalle_matricula.id_curso
  GROUP BY curso.año_inicio;
  +-------------+--------------------------+
  | año_inicio  | num_alumnos_matriculados |
  +-------------+--------------------------+
  | 2018-09-01  |                        1 |
  | 2019-09-01  |                        1 |
  | 2020-09-01  |                        1 |
  | 2021-09-01  |                        1 |
  +-------------+--------------------------+
  ```

  

9. Devuelve un listado con el número de asignaturas que imparte cada
  profesor. El listado debe tener en cuenta aquellos profesores que no
  imparten ninguna asignatura. El resultado mostrará cinco columnas: id,
  nombre, primer apellido, segundo apellido y número de asignaturas. El
  resultado estará ordenado de mayor a menor por el número de asignaturas.

```sql
SELECT profesor.id_profesor, datos.nombre, datos.apellido1, datos.apellido2, COUNT(asignatura.id_asignatura) AS num_asignaturas
FROM profesor
LEFT JOIN asignatura ON profesor.id_profesor = asignatura.id_profesor
LEFT JOIN datos ON profesor.id_datos = datos.id_datos
GROUP BY profesor.id_profesor, datos.nombre, datos.apellido1, datos.apellido2
ORDER BY num_asignaturas DESC;
+-------------+--------+-----------+------------+-----------------+
| id_profesor | nombre | apellido1 | apellido2  | num_asignaturas |
+-------------+--------+-----------+------------+-----------------+
|           1 | Juan   | García    | López      |               1 |
|           2 | María  | Martínez  | Pérez      |               1 |
|           3 | Carlos | Sánchez   | Gómez      |               1 |
|           4 | Ana    | López     | Fernández  |               1 |
+-------------+--------+-----------+------------+-----------------+
```

Subconsultas
1. Devuelve todos los datos del alumno más joven.

   ```sql
   SELECT alumno.id_alumno, alumno.nif, alumno.id_datos, alumno.id_ubicacion, alumno.id_contacto, alumno.fecha_nacimiento, alumno.sexo
   FROM alumno
   WHERE alumno.fecha_nacimiento = (
       SELECT MIN(alumno.fecha_nacimiento)
       FROM alumno
   );
   +-----------+-----------+----------+--------------+-------------+------------------+------+
   | id_alumno | nif       | id_datos | id_ubicacion | id_contacto | fecha_nacimiento | sexo |
   +-----------+-----------+----------+--------------+-------------+------------------+------+
   |         4 | 44444444W |        4 |            4 |           4 | 1997-04-05       | M    |
   +-----------+-----------+----------+--------------+-------------+------------------+------+
   ```

   

2. Devuelve un listado con los profesores que no están asociados a un
  departamento.

  ```sql
  SELECT profesor.id_profesor, profesor.nif, profesor.id_datos, profesor.id_contacto, profesor.id_ubicacion, profesor.fecha_nacimiento, profesor.sexo, profesor.id_departamento
  FROM profesor
  WHERE profesor.id_departamento IS NULL;
  Program did not output anything!
  ```

  

3. Devuelve un listado con los departamentos que no tienen profesores
  asociados.

  ```sql
  SELECT departamento.id_departamento, departamento.nombre
  FROM departamento
  WHERE departamento.id_departamento NOT IN (
      SELECT id_departamento
      FROM profesor
      WHERE id_departamento IS NOT NULL
  );
  Program did not output anything!
  ```

  

4. Devuelve un listado con los profesores que tienen un departamento
  asociado y que no imparten ninguna asignatura.

  ```sql
  SELECT profesor.id_profesor, profesor.nif, profesor.id_datos, profesor.id_contacto, profesor.id_ubicacion, profesor.fecha_nacimiento, profesor.sexo, profesor.id_departamento
  FROM profesor
  LEFT JOIN asignatura ON profesor.id_profesor = asignatura.id_profesor
  WHERE profesor.id_departamento IS NOT NULL AND asignatura.id_asignatura IS NULL;
  Program did not output anything!
  ```

  

5. Devuelve un listado con las asignaturas que no tienen un profesor asignado.

   ```sql
   SELECT asignatura.id_asignatura, asignatura.cuatrimestre, asignatura.id_detalle, asignatura.id_profesor, asignatura.id_grado
   FROM asignatura
   WHERE asignatura.id_profesor IS NULL;
   Program did not output anything!
   ```

   

6. Devuelve un listado con todos los departamentos que no han impartido
  asignaturas en ningún curso escolar.

  ```sql
  
  SELECT departamento.id_departamento, departamento.nombre
  FROM departamento
  LEFT JOIN profesor ON departamento.id_departamento = profesor.id_departamento
  LEFT JOIN asignatura ON profesor.id_profesor = asignatura.id_profesor
  GROUP BY departamento.id_departamento, departamento.nombre
  HAVING COUNT(asignatura.id_asignatura) = 0;
  Program did not output anything!
  ```

  