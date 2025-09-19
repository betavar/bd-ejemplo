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
