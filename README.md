# bd-ejemplo
aprendiendo a crear base de datos

MySQL Workbench

1)CREAR BASE DE DATOS:   create database nombre;

2)LISTAR BASE DE DATOS: show database;

3)TRABAJAR EN LA BASE DE DATOS:  use nombre;

4)CREAR TABLA: 
	CREATE TABLE usuarios (
	ID INT PRIMARY KEY AUTO_INCREMENT,
	nombre VARCHAR(100),
	correo_Electtronico VARCHAR(100) UNIQUE,
	Fecha_Registro DATE
);

AGREGAR INFORMACION A TABLA

insert into usuarios (nombre, apellido,telefono)
values ("jhon","betava",3115329938);
select * from usuarios;

RELACION ENTRE TABLAS

1) CREATE TABLE pedidos(
	ID INT PRIMARY KEY AUTO_INCREMENT,
	ID_Usuario INT,
	Producto varchar(100),
	fecha_pedido DATE,
	FOREIGN KEY (ID_usuario) REFERENCES usuarios(ID)
);

// TRAER DATOS DE LA TABLA //
select * from usuarios where id >2;

// pagina para hacer la relacion de tablas en diagramas //
https://app.diagrams.net/

//  AGREGAR COLUMNA A TABLA //

ALTER TABLE `tienda`.`usuarios`               //  ingreso a la BD tienda para modificar la tabla tienda 
ADD COLUMN 'apellido' VARCHAR(100) NULL AFTER 'nombre',       // agrego una columna llamada apellido
CHANGE COLUMN `fecha_registro` `telefono` VARCHAR(20) NULL DEFAULT NULL ;  // cambio el nombre de una columna


select * from productos order by precios desc limt 100


CONSULTA DE BD

select count(*) from customers;
select count(*) from customers where city = "nantes";
cuente cuantos usuarios hay en esta ciudad nantes

select * from customers;
select * from products;
select avg(buyPrice) from products;
promedio de la columna de productos

select * from customers where customerName like "la%"
mostrar los elementos de la lista que empiezan con la
select * from customers where customerName like "%la%"
mostrar los elementos que contenga la palabra la

select * from customers where customerNumber in (110,111,112,113);

select * from customers where customerNumber not in (110,111,112,113);

select * from orders where orderDate between "2003-01-10" and "2003-02-10";
select * from orders where shippedDate >= "2003-01-10" and shippedDate < "2003-02-10";
mostrar las dordenes en un rango de fechas 

select orderNumber, sum(quantityOrdered * priceEach) from orderdetails group by orderNumber;
select orderNumber, sum(quantityOrdered) from orderdetails group by orderNumber;

SELECT * FROM classicmodels.products;
select productLine, count(productCode) from products group by productLine;

// mostrar la cantidad de clientes por ciudad y cambiar el nombre de mi columna customerNumber por clientes  //
SELECT * FROM classicmodels.customers;
select city, count(customerNumber) as clientes from customers group by city order by clientes desc;

select productName, productLine, buyPrice
from products where buyprice > (select avg(buyprice) from products);

select * from customers where customerNumber in (
select customerNumber from orders where orderDate between "2003-01-10" and "2003-03-10"
);

select customerNumber from orders where orderDate between "2003-01-10" and "2003-03-10";

// unir columnas en una sola, de diferentres tablas //
select customerName from customers union select firstName from employees;


// unir dos tablas en una sola //
select * from orderdetails od inner join orders on od.orderNumber;

// consultar dos tablas a la vez //
select od.orderNumber, p.productName, od.quantityOrdered, od.priceEach, p.buyPrice, (od.quantityOrdered * od.priceEach) as total, orderDate, o.status
from orderdetails od
inner join orders o
on od.orderNumber = o.orderNumber
inner join products p
on p.productCode = od.productCode
where od.orderNumber = 10100

SELECT c.customerName, c.contactLastName, e.firstName, e.lastName, j.firstName, j.lastName, j.jobTitle from customers c
inner join employees e
on e.employeeNumber = c.salesRepEmployeeNumber
inner join employees j 
on j.employeeNumber = e.reportsTo;


use classicmodels;
select * from classicmodels.customers;
select * from classicmodels.payments;

select c.customerName, p.checkNumber, p.amount
from customers c 
left join payments p 
on p.customerNumber = c.customerNumber
where p.checkNumber is null ;


// consultar el cliente que mas a comprado y sumar el valor //
select c.customerName, sum(amount) as pagos
from customers c
join payments p
on p.customerNumber = c.customerNumber
group by p.customerNumber
order by pagos desc;


//  crear una nueva tabla uniendo columnas de otras y que quede grabada //

create view vista_productos_bajos as
select productCode, productName, quantityInStock from products
where quantityInStock;

//  eliminar la tabla de view(vista) //

drop view vista_productos_bajos;

// ejemplo de crear tablas de vistas //

create view ventasClientes as
select c.customerName, sum(od.priceEach * od.quantityOrdered) as total
from orderdetails od
join orders o 
on o.orderNumber = od.orderNumber
join customers c
on c.customerNumber = o.customerNumber
group by customerName
order by total desc;

select * from ventasClientes;

// crear funciones y lugo llamarlas //

use classicmodels;

DELIMITER //
create function totalpedidos(clienteId int)
returns decimal(10,2)
deterministic
begin
 declare total decimal(10,2);
 select sum(od.priceEach * od.quantityOrdered) into total
 from orders o 
 join orderdatails od
 on o.orderNumber = od.orderNumber 
 where customerNumber = clienteId;
 return total;
end //
DELIMITER ;

-- Uso
select customerName, totalPedidos(customerNumber) as gasto
from customers order by gasto desc;

//                           //
@app.route("/search")
def search():
    q = request.args.get ("q")
    return f"el parametro de busqueda es {q}"

como buscar en la web el parametro search
http://127.0.0.1:5000/search?q=jhon

//                             //
from flask import url_for, redirect 
@app.route("/old")
def old():
    return redirect(url_for("about"))

http://127.0.0.1:5000/old



