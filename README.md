# bd-ejemplo
aprendiendo a crear base de datos

MySQL Workbench

1)CREAR BASE DE DATOS:   create database nombre; base

2)LISTAR BASE DE DATOS: show database;

3)TRABAJAR EN LA BASE DE DATOS:  use nombre;

4)CREAR TABLA: 
	CREATE TABLE usuarios (
	ID INT PRIMARY KEY AUTO_INCREMENT,
	nombre VARCHAR(100),
	correo_Electtronico VARCHAR(100) UNIQUE,
	Fecha_Registro DATE
);

RELACION ENTRE TABLAS

1) CREATE TABLE pedidos(
	ID INT PRIMARY KEY AUTO_INCREMENT,
	ID_Usuario INT,
	Producto varchar(100),
	fecha_pedido DATE,
	FOREIGN KEY (ID_usuario) REFERENCES usuarios(ID)
);

TRAER DATOS DE LA TABLA

select * from usuarios where id >2;

https://app.diagrams.net/

AGREGAR COLUMNA A TABLA
ALTER TABLE `tienda`.`usuarios`               //  ingreso a la BD tienda para modificar la tabla tienda 
ADD COLUMN 'apellido' VARCHAR(100) NULL AFTER 'nombre',       // agrego una columna llamada apellido
CHANGE COLUMN `fecha_registro` `telefono` VARCHAR(20) NULL DEFAULT NULL ;  // cambio el nombre de una columna

insert into usuarios (nombre, apellido,telefono)
values ("jhon","betava",3115329938);
select * from usuarios;

select * from productos order by precios desc limt 100

