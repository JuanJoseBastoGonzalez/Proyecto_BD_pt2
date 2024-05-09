tabla profesor 

```sql
CREATE TABLE profesor (
id_profesor varcahar(10) NOT NULL  PRIMARI KEY,
nif VARCHAR(10),
id_datos VARCHAR(10),
id_contacto VARCHAR(10),
fecha_nacimiento DATE,
sexo VARCHAR(10),
id_departamento VARCHAR(10)
);
```

tabla asignatura

```sql
CREATE TABLE asignactura(
id_asignatura INT(10) NOT NULL PRIMARY KEY,
id_detalle INT(10),
cuatrimestre VARCHAR(20),
id_profeso INT(10),
id_grado VARCHAR(10)
);
```

tabla grado

```sql
CREATE TABLE grado(
id_grado VARCHAR(10) NOT NULL AUTO_INCREMENT PRIMARY KEY,
nombre VARCHAR(100)
);
```

tabla detalle_asignatura

```sql
CREATE TABLE detalle_asifnatura(
id_detalle INT(10) NOT NULL PRIMARY KEY,
nombre VARCHAR(100),
creditos INT(4),
tipo VARCHAR(100),
curso VARCHAR(100)
);
```

tabla detalle_matricula

```sql
CREATE TABLE detalle_matricula (
id_matricula INT(10) AUTO_INCREMENT PRIMARY KEY,
id_alumno VARCHAR(10),
id_asignatura INT(10),
id_curso INT(10)
);
```

tabla curso

```sql
CREATE TABLE curso(
id_curso INT(10) AUTO_INCREMENT PRIMARY KEY,
año_inicio DATE,
año_fin DATE
);
```

tabla departamento 

```sql
CREATE TABLE departamento(
id_departamento VARCHAR(10) AUTO_INCREMENT PRIMARY KEY,
nombre VARCHAR(50)
);
```

tabla datos 

```sql
CREATE TABLE datos(
id_datos VARCHAR(10) NOT NULL PRIMARY KEY,
nombre VARCHAR(50),
apellido1 VARCHAR(50),
apellido2 VARCHAR(50)
);
```

tabla ubicacion 

```sql
CREATE TABLE  ubicacion (
id_ubicacion VARCHAR(10) NOT NULL PRIMARY KEY,
direccion VARCHAR(50),
id_ciudad INT(10)
);
```

tabla ciudad

```sql
CREATE TEBLE ciudad (
id_ciudad INT(10) NOT NULL PRIMARY KEY,
nombre VARCHAR(50),
codigo_postal VARCHAR(8)
);
```

tabla contacto

```SQL
CREATE TABLE contacto (
id_contacto VARCHAR(10) NOT NULL PRIMARY KEY,
numero INT(10),
tipo VARCHAR(20)
);
```

tabla alumno 

```SQL
CREATE TABLE alumno (
id_alumno VARCHAR(10) NOT NULL PRIMARY KEY,
nif VARCHAR(10),
id_datos VARCHAR(10),
Id_contacto VARCHAR(10),
fecha_nacimiento DATE,
sexo VARCHAR(10)
);
```









```
CREATE TABLE profesor (
    id_profesor INT(10) AUTO_INCREMENT PRIMARY KEY,
    nif VARCHAR(10),
    id_datos INT(10),
    id_contacto INT(10),
    id_ubicacion INT(10),
    fecha_nacimiento DATE,
    sexo VARCHAR(10),
    id_departamento INT(10)
);

CREATE TABLE asignatura (
    id_asignatura INT(10) NOT NULL AUTO_INCREMENT PRIMARY KEY,
    cuatrimestre VARCHAR(20),
    id_detalle INT(10),
    id_profesor INT(10),
    id_grado INT(10)
);

CREATE TABLE grado (
    id_grado INT(10) AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100)
);

CREATE TABLE detalle_asignatura (
    id_detalle INT(10) AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    creditos INT,
    tipo VARCHAR(100),
    curso VARCHAR(100)
);

CREATE TABLE detalle_matricula (
    id_matricula INT(10) AUTO_INCREMENT PRIMARY KEY,
    id_alumno INT(10),
    id_asignatura INT(10),
    id_curso INT(10)
);

CREATE TABLE curso (
    id_curso INT(10) AUTO_INCREMENT PRIMARY KEY,
    año_inicio DATE,
    año_fin DATE
);

CREATE TABLE departamento (
    id_departamento INT(10) AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50)
);

CREATE TABLE datos (
    id_datos INT(10) AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
    apellido1 VARCHAR(50),
    apellido2 VARCHAR(50)
);

CREATE TABLE ubicacion (
    id_ubicacion INT(10) AUTO_INCREMENT PRIMARY KEY,
    direccion VARCHAR(50),
    id_ciudad INT(10)
);

CREATE TABLE ciudad (
    id_ciudad INT(10) AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
    codigo_postal VARCHAR(8)
);

CREATE TABLE contacto (
    id_contacto INT(10) AUTO_INCREMENT PRIMARY KEY,
    numero INT(10),
    tipo VARCHAR(20)
);

CREATE TABLE alumno (
    id_alumno INT(10) AUTO_INCREMENT PRIMARY KEY,
    nif VARCHAR(10),
    id_datos INT(10),
    id_ubicacion INT(10),
    id_contacto INT(10),
    fecha_nacimiento DATE,
    sexo VARCHAR(10)
);



-- Agregar datos a la tabla de grados
INSERT INTO grado (nombre) VALUES 
('Ingeniería Informática'),
('Matemáticas'),
('Biología'),
('Historia');

-- Agregar datos a la tabla de departamentos
INSERT INTO departamento (nombre) VALUES 
('Departamento de Informática'),
('Departamento de Matemáticas'),
('Departamento de Biología'),
('Departamento de Historia');

-- Agregar datos a la tabla de profesores
INSERT INTO profesor (nif, id_datos, id_contacto, id_ubicacion, fecha_nacimiento, sexo, id_departamento) VALUES
('12345678A', 1, 1, 1, '1980-05-15', 'M', 1),
('23456789B', 2, 2, 2, '1975-09-20', 'F', 2),
('34567890C', 3, 3, 3, '1990-03-10', 'M', 3),
('45678901D', 4, 4, 4, '1988-11-25', 'F', 4);

-- Agregar datos a la tabla de datos
INSERT INTO datos (nombre, apellido1, apellido2) VALUES
('Juan', 'García', 'López'),
('María', 'Martínez', 'Pérez'),
('Carlos', 'Sánchez', 'Gómez'),
('Ana', 'López', 'Fernández');

-- Agregar datos a la tabla de contacto
INSERT INTO contacto (numero, tipo) VALUES
(123456789, 'Teléfono'),
(987654321, 'Teléfono'),
(555555555, 'Teléfono'),
(777777777, 'Teléfono');

-- Agregar datos a la tabla de ubicación
INSERT INTO ubicacion (direccion, id_ciudad) VALUES
('Calle Principal 123', 1),
('Avenida Central 456', 2),
('Plaza Mayor 789', 3),
('Paseo de la Victoria 321', 4);

-- Agregar datos a la tabla de ciudad
INSERT INTO ciudad (nombre, codigo_postal) VALUES
('Ciudad A', '12345'),
('Ciudad B', '54321'),
('Ciudad C', '67890'),
('Ciudad D', '09876');

-- Agregar datos a la tabla de asignaturas
INSERT INTO asignatura (cuatrimestre, id_detalle, id_profesor, id_grado) VALUES
('Primer Cuatrimestre', 1, 1, 1),
('Segundo Cuatrimestre', 2, 2, 1),
('Primer Cuatrimestre', 3, 3, 2),
('Segundo Cuatrimestre', 4, 4, 2);

-- Agregar datos a la tabla de detalle_asignatura
INSERT INTO detalle_asignatura (nombre, creditos, tipo, curso) VALUES
('Programación', 6, 'Obligatoria', 'Tercer Curso'),
('Álgebra Lineal', 6, 'Obligatoria', 'Tercer Curso'),
('Biología Celular', 6, 'Obligatoria', 'Segundo Curso'),
('Historia Contemporánea', 6, 'Obligatoria', 'Segundo Curso');

-- Agregar datos a la tabla de alumnos
INSERT INTO alumno (nif, id_datos, id_ubicacion, id_contacto, fecha_nacimiento, sexo) VALUES
('11111111X', 1, 1, 1, '1999-02-10', 'F'),
('22222222Y', 2, 2, 2, '1998-11-28', 'M'),
('33333333Z', 3, 3, 3, '2000-07-15', 'F'),
('44444444W', 4, 4, 4, '1997-04-05', 'M');

-- Agregar datos a la tabla de cursos
INSERT INTO curso (año_inicio, año_fin) VALUES
('2018-09-01', '2019-06-30'),
('2019-09-01', '2020-06-30'),
('2020-09-01', '2021-06-30'),
('2021-09-01', '2022-06-30');

-- Agregar datos a la tabla de detalle_matricula
INSERT INTO detalle_matricula (id_alumno, id_asignatura, id_curso) VALUES
(1, 1, 1),
(2, 2, 2),
(3, 3, 3),
(4, 4, 4);

```







```

```

