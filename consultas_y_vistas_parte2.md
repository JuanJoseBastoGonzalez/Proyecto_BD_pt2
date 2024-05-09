7. Debe generar 10 vistas por cada Base de datos (Las vistas pueden ser tomadas de los comandos sql ya desarrollados)

   1. Listado de grados con más de 40 asignaturas asociadas

   

   ```sql
   CREATE VIEW Vista_Grados_Con_Mas_De_40_Asignaturas AS
   SELECT grado.nombre AS nombre_grado, COUNT(asignatura.id_asignatura) AS num_asignaturas
   FROM grado
   JOIN asignatura ON grado.id_grado = asignatura.id_grado
   GROUP BY grado.nombre
   HAVING num_asignaturas > 40;
   
   ```

   2. Listado de alumnos más jóvenes

   ```sql
   CREATE VIEW Vista_Alumnos_Mas_Jovenes AS
   SELECT *
   FROM alumno
   WHERE fecha_nacimiento = (SELECT MIN(fecha_nacimiento) FROM alumno);
   
   ```

   3. Listado de profesores sin asociación a un departamento

   ```sql
   CREATE VIEW Vista_Profesores_Sin_Departamento AS
   SELECT profesor.*
   FROM profesor
   WHERE id_departamento IS NULL;
   
   ```

   4. Listado de departamentos sin profesores asociados

   ```sql
   CREATE VIEW Vista_Departamentos_Sin_Profesores AS
   SELECT departamento.*
   FROM departamento
   WHERE id_departamento NOT IN (SELECT id_departamento FROM profesor);
   
   ```

   5. Listado de asignaturas sin profesor asignado

   ```sql
   CREATE VIEW Vista_Asignaturas_Sin_Profesor AS
   SELECT *
   FROM asignatura
   WHERE id_profesor IS NULL;
   
   ```

   6. Listado de cursos escolares y el número de alumnos matriculados en cada uno

   ```sql
   CREATE VIEW Vista_Matriculas_Por_Curso AS
   SELECT curso.año_inicio, COUNT(detalle_matricula.id_alumno) AS num_alumnos_matriculados
   FROM curso
   LEFT JOIN detalle_matricula ON curso.id_curso = detalle_matricula.id_curso
   GROUP BY curso.año_inicio;
   
   ```

   7. Listado de grados y la suma total de créditos por tipo de asignatura

   ```sql
   CREATE VIEW Vista_Total_Creditos_Por_Grado AS
   SELECT grado.nombre AS nombre_grado, detalle_asignatura.tipo, SUM(detalle_asignatura.creditos) AS total_creditos
   FROM grado
   LEFT JOIN asignatura ON grado.id_grado = asignatura.id_grado
   LEFT JOIN detalle_asignatura ON asignatura.id_detalle = detalle_asignatura.id_detalle
   GROUP BY grado.nombre, detalle_asignatura.tipo;
   
   ```

   8. Listado de alumnos matriculados en asignaturas de un profesor específico

   ```sql
   CREATE VIEW Vista_Alumnos_Matriculados_Por_Profesor AS
   SELECT alumno.*
   FROM alumno
   JOIN detalle_matricula ON alumno.id_alumno = detalle_matricula.id_alumno
   JOIN asignatura ON detalle_matricula.id_asignatura = asignatura.id_asignatura
   WHERE asignatura.id_profesor = (SELECT id_profesor FROM profesor WHERE nombre = 'Nombre_Profesor');
   
   ```

   9. Listado de alumnos matriculados en un grado específico

   ```sql
   CREATE VIEW Vista_Alumnos_Matriculados_Por_Grado AS
   SELECT alumno.*
   FROM alumno
   JOIN detalle_matricula ON alumno.id_alumno = detalle_matricula.id_alumno
   JOIN asignatura ON detalle_matricula.id_asignatura = asignatura.id_asignatura
   JOIN grado ON asignatura.id_grado = grado.id_grado
   WHERE grado.nombre = 'Nombre_Grado';
   
   ```

   10. Listado de grados y el número de asignaturas que tiene cada uno, incluyendo grados sin asignaturas asociadas

   ```sql
   CREATE VIEW Vista_Numero_Asignaturas_Por_Grado AS
   SELECT grado.nombre AS nombre_grado, COUNT(asignatura.id_asignatura) AS num_asignaturas
   FROM grado
   LEFT JOIN asignatura ON grado.id_grado = asignatura.id_grado
   GROUP BY grado.nombre;
   
   ```

8. Debe generar 10 procedimientos almacenados por cada base de datos. Los procedimientos deben incluir procesos de Crear, Actualizar, eliminar o buscar

1. Crear un nuevo alumno

```sql
CREATE PROCEDURE Crear_Alumno(
    IN p_nif VARCHAR(10),
    IN p_id_datos INT,
    IN p_id_ubicacion INT,
    IN p_id_contacto INT,
    IN p_fecha_nacimiento DATE,
    IN p_sexo VARCHAR(10)
)
BEGIN
    INSERT INTO alumno (nif, id_datos, id_ubicacion, id_contacto, fecha_nacimiento, sexo)
    VALUES (p_nif, p_id_datos, p_id_ubicacion, p_id_contacto, p_fecha_nacimiento, p_sexo);
END;

```

2. Actualizar información de un alumno

```sql
CREATE PROCEDURE Actualizar_Informacion_Alumno(
    IN p_id_alumno INT,
    IN p_nuevo_nif VARCHAR(10),
    IN p_nuevo_fecha_nacimiento DATE,
    IN p_nuevo_sexo VARCHAR(10)
)
BEGIN
    UPDATE alumno
    SET nif = p_nuevo_nif, fecha_nacimiento = p_nuevo_fecha_nacimiento, sexo = p_nuevo_sexo
    WHERE id_alumno = p_id_alumno;
END;

```

3. Eliminar un alumno

```sql
CREATE PROCEDURE Eliminar_Alumno(
    IN p_id_alumno INT
)
BEGIN
    DELETE FROM alumno WHERE id_alumno = p_id_alumno;
END;

```

4. Buscar un alumno por su ID

```sql
CREATE PROCEDURE Buscar_Alumno_Por_ID(
    IN p_id_alumno INT
)
BEGIN
    SELECT *
    FROM alumno
    WHERE id_alumno = p_id_alumno;
END;

```

5. Crear una nueva asignatura

```sql
CREATE PROCEDURE Crear_Asignatura(
    IN p_cuatrimestre VARCHAR(20),
    IN p_id_detalle INT,
    IN p_id_profesor INT,
    IN p_id_grado INT
)
BEGIN
    INSERT INTO asignatura (cuatrimestre, id_detalle, id_profesor, id_grado)
    VALUES (p_cuatrimestre, p_id_detalle, p_id_profesor, p_id_grado);
END;

```

6. Actualizar información de una asignatura

```sql
CREATE PROCEDURE Actualizar_Informacion_Asignatura(
    IN p_id_asignatura INT,
    IN p_nuevo_cuatrimestre VARCHAR(20),
    IN p_nuevo_id_detalle INT,
    IN p_nuevo_id_profesor INT,
    IN p_nuevo_id_grado INT
)
BEGIN
    UPDATE asignatura
    SET cuatrimestre = p_nuevo_cuatrimestre, id_detalle = p_nuevo_id_detalle, id_profesor = p_nuevo_id_profesor, id_grado = p_nuevo_id_grado
    WHERE id_asignatura = p_id_asignatura;
END;

```

7. Eliminar una asignatura

```sql
CREATE PROCEDURE Eliminar_Asignatura(
    IN p_id_asignatura INT
)
BEGIN
    DELETE FROM asignatura WHERE id_asignatura = p_id_asignatura;
END;

```

8. 

1. Buscar una asignatura por su ID

```sql
CREATE PROCEDURE Buscar_Asignatura_Por_ID(
    IN p_id_asignatura INT
)
BEGIN
    SELECT *
    FROM asignatura
    WHERE id_asignatura = p_id_asignatura;
END;

```

9. Crear un nuevo profesor

```sql
CREATE PROCEDURE Crear_Profesor(
    IN p_nif VARCHAR(10),
    IN p_id_datos INT,
    IN p_id_contacto INT,
    IN p_id_ubicacion INT,
    IN p_fecha_nacimiento DATE,
    IN p_sexo VARCHAR(10),
    IN p_id_departamento INT
)
BEGIN
    INSERT INTO profesor (nif, id_datos, id_contacto, id_ubicacion, fecha_nacimiento, sexo, id_departamento)
    VALUES (p_nif, p_id_datos, p_id_contacto, p_id_ubicacion, p_fecha_nacimiento, p_sexo, p_id_departamento);
END;

```

10 . 

1. Actualizar información de un profesor

```sql
CREATE PROCEDURE Actualizar_Informacion_Profesor(
    IN p_id_profesor INT,
    IN p_nuevo_nif VARCHAR(10),
    IN p_nuevo_id_datos INT,
    IN p_nuevo_id_contacto INT,
    IN p_nuevo_id_ubicacion INT,
    IN p_nuevo_fecha_nacimiento DATE,
    IN p_nuevo_sexo VARCHAR(10),
    IN p_nuevo_id_departamento INT
)
BEGIN
    UPDATE profesor
    SET nif = p_nuevo_nif, id_datos = p_nuevo_id_datos, id_contacto = p_nuevo_id_contacto,
        id_ubicacion = p_nuevo_id_ubicacion, fecha_nacimiento = p_nuevo_fecha_nacimiento,
        sexo = p_nuevo_sexo, id_departamento = p_nuevo_id_departamento
    WHERE id_profesor = p_id_profesor;
END;

```