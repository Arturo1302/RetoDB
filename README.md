# Sistema de Registro de Pedidos - Base de Datos

## Descripción

Este proyecto consiste en el diseño de una base de datos para un sistema de registro de pedidos en una tienda en línea.
El objetivo principal es organizar la información de manera eficiente, evitando redundancias mediante el proceso de normalización.

---

## Objetivos

* Diseñar una base de datos estructurada y eficiente
* Aplicar principios de normalización
* Establecer relaciones entre entidades
* Garantizar integridad de datos mediante claves primarias y foráneas

---


El sistema está compuesto por las siguientes tablas:

### Clientes

Almacena la información de los clientes.

* ID_Cliente (PK)
* Nombre_Cliente

### Productos

Contiene los productos disponibles.

* ID_Producto (PK)
* Nombre_Producto

### Pedidos

Registra los pedidos realizados por los clientes.

* Numero_Pedido (PK)
* Fecha_Pedido
* ID_Cliente (FK)

### Detalles_Pedido

Relaciona los pedidos con los productos (muchos a muchos).

* ID_Detalle (PK)
* Numero_Pedido (FK)
* ID_Producto (FK)
* Cantidad

### Envios

Guarda la información del envío de cada pedido.

* ID_Envio (PK)
* Numero_Pedido (FK)
* Fecha_Envio

---

## Relaciones

* Un cliente puede tener muchos pedidos
* Un pedido puede tener varios productos
* Un producto puede estar en varios pedidos
* Un pedido tiene información de envío

---

##  Cómo usar

1. Crear la base de datos en tu gestor (MySQL, etc.)
2. Ejecutar el script SQL proporcionado
3. Insertar datos de prueba
4. Realizar consultas con JOIN para obtener información

---

## Codigo

```sql

CREATE TABLE Productos (
    ID_Producto INT PRIMARY KEY,
    Nombre_Producto VARCHAR(100) NOT NULL
);


CREATE TABLE Pedidos (
    Numero_Pedido INT PRIMARY KEY,
    Fecha_Pedido DATE NOT NULL,
    ID_Cliente INT,
    FOREIGN KEY (ID_Cliente)REFERENCES Clientes(ID_Cliente)
        ON DELETE RESTRICT
        ON UPDATE CASCADE
);

CREATE TABLE Detalles_Pedido (
    ID_Detalle INT PRIMARY KEY,
    Numero_Pedido INT,
    ID_Producto INT,
    Cantidad INT NOT NULL,
    FOREIGN KEY (Numero_Pedido)
        REFERENCES Pedidos(Numero_Pedido)
        ON DELETE RESTRICT
        ON UPDATE CASCADE,
    FOREIGN KEY (ID_Producto)REFERENCES Productos(ID_Producto)
        ON DELETE RESTRICT
        ON UPDATE CASCADE
);


CREATE TABLE Envios (
    ID_Envio INT PRIMARY KEY,
    Numero_Pedido INT,
    Fecha_Envio DATE NOT NULL,
    FOREIGN KEY (Numero_Pedido)REFERENCES Pedidos(Numero_Pedido)
        ON DELETE RESTRICT
        ON UPDATE CASCADE
);

```
![Imagen Diagrama](https://github.com/Arturo1302/RetoDB/blob/main/Captura%20desde%202026-03-27%2007-22-11.png)
