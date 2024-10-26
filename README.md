# CampusBike
## Creación de tablas
```sql

CREATE TABLE Clientes (
    id_cliente INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    direccion VARCHAR(255),
    telefono VARCHAR(20),
    email VARCHAR(100),
    id_pais INT
);

CREATE TABLE País (
    id_pais INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    id_region INT
);

CREATE TABLE Región (
    id_region INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    id_ciudad INT
);

CREATE TABLE Ciudad (
    id_ciudad INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    id_sucursal INT
);

CREATE TABLE Sucursales (
    id_sucursal INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    direccion VARCHAR(255),
    id_ciudad INT
);

CREATE TABLE Proveedores (
    id_proveedor INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    telefono VARCHAR(20),
    direccion VARCHAR(255),
    email VARCHAR(100),
    id_pais INT
);

CREATE TABLE Repuesto (
    id_repuesto INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    precio DECIMAL(10, 2),
    id_proveedor INT
);

CREATE TABLE Productos (
    id_producto INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    categoria VARCHAR(100),
    precio DECIMAL(10, 2),
    stock INT,
    id_proveedor INT
);

CREATE TABLE Bicicleta (
    id_bicicleta INT AUTO_INCREMENT PRIMARY KEY,
    marca VARCHAR(100),
    tipo_bicicleta VARCHAR(50),
    valor DECIMAL(10, 2),
    id_proveedor INT
);

CREATE TABLE Ventas (
    id_venta INT AUTO_INCREMENT PRIMARY KEY,
    id_cliente INT,
    id_vendedor INT,
    id_bicicleta INT,
    fecha DATE,
    cantidad INT,
    total DECIMAL(10, 2)
);

CREATE TABLE Facturación (
    id_factura INT AUTO_INCREMENT PRIMARY KEY,
    id_venta INT,
    id_fecha INT,
    total DECIMAL(10, 2)
);

CREATE TABLE Empleados (
    id_empleado INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    cargo VARCHAR(50),
    telefono VARCHAR(20),
    email VARCHAR(100),
    id_sucursal INT
);

CREATE TABLE Stock (
    id_stock INT AUTO_INCREMENT PRIMARY KEY,
    id_producto INT,
    id_sucursal INT,
    cantidad INT
);

CREATE TABLE Pedidos (
    id_pedido INT AUTO_INCREMENT PRIMARY KEY,
    id_cliente INT,
    id_producto INT,
    cantidad INT,
    fecha_pedido DATE,
    estado VARCHAR(50)
);

CREATE TABLE Pago (
    id_pago INT AUTO_INCREMENT PRIMARY KEY,
    id_venta INT,
    tipo_pago VARCHAR(50),
    monto DECIMAL(10, 2),
    fecha_pago DATE
);

CREATE TABLE Sector_Venta (
    id_sectorv INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    id_sucursal INT
);

CREATE TABLE Cuentas_por_saldar (
    id_cuenta_por_saldar INT AUTO_INCREMENT PRIMARY KEY,
    id_proveedor INT,
    monto DECIMAL(10, 2),
    fecha_vencimiento DATE,
    estado VARCHAR(50)
);

CREATE TABLE Total_ventas (
    id_total_ventas INT AUTO_INCREMENT PRIMARY KEY,
    id_sucursal INT,
    total DECIMAL(10, 2),
    fecha DATE
);

CREATE TABLE Fecha (
    id_fecha INT AUTO_INCREMENT PRIMARY KEY,
    fecha DATE,
    descripcion VARCHAR(100)
);

```
## Llaves Foraneas
```sql
ALTER TABLE Clientes ADD CONSTRAINT fk_clientes_pais FOREIGN KEY (id_pais) REFERENCES País(id_pais);

ALTER TABLE País ADD CONSTRAINT fk_pais_region FOREIGN KEY (id_region) REFERENCES Región(id_region);

ALTER TABLE Región ADD CONSTRAINT fk_region_ciudad FOREIGN KEY (id_ciudad) REFERENCES Ciudad(id_ciudad);

ALTER TABLE Ciudad ADD CONSTRAINT fk_ciudad_sucursal FOREIGN KEY (id_sucursal) REFERENCES Sucursales(id_sucursal);

ALTER TABLE Sucursales ADD CONSTRAINT fk_sucursales_ciudad FOREIGN KEY (id_ciudad) REFERENCES Ciudad(id_ciudad);

ALTER TABLE Proveedores ADD CONSTRAINT fk_proveedores_pais FOREIGN KEY (id_pais) REFERENCES País(id_pais);

ALTER TABLE Repuesto ADD CONSTRAINT fk_repuesto_proveedor FOREIGN KEY (id_proveedor) REFERENCES Proveedores(id_proveedor);

ALTER TABLE Productos ADD CONSTRAINT fk_productos_proveedor FOREIGN KEY (id_proveedor) REFERENCES Proveedores(id_proveedor);

ALTER TABLE Bicicleta ADD CONSTRAINT fk_bicicleta_proveedor FOREIGN KEY (id_proveedor) REFERENCES Proveedores(id_proveedor);

ALTER TABLE Ventas ADD CONSTRAINT fk_ventas_cliente FOREIGN KEY (id_cliente) REFERENCES Clientes(id_cliente);
ALTER TABLE Ventas ADD CONSTRAINT fk_ventas_vendedor FOREIGN KEY (id_vendedor) REFERENCES Empleados(id_empleado);
ALTER TABLE Ventas ADD CONSTRAINT fk_ventas_bicicleta FOREIGN KEY (id_bicicleta) REFERENCES Bicicleta(id_bicicleta);

ALTER TABLE Facturación ADD CONSTRAINT fk_facturacion_venta FOREIGN KEY (id_venta) REFERENCES Ventas(id_venta);
ALTER TABLE Facturación ADD CONSTRAINT fk_facturacion_fecha FOREIGN KEY (id_fecha) REFERENCES Fecha(id_fecha);

ALTER TABLE Empleados ADD CONSTRAINT fk_empleados_sucursal FOREIGN KEY (id_sucursal) REFERENCES Sucursales(id_sucursal);

ALTER TABLE Stock ADD CONSTRAINT fk_stock_producto FOREIGN KEY (id_producto) REFERENCES Productos(id_producto);
ALTER TABLE Stock ADD CONSTRAINT fk_stock_sucursal FOREIGN KEY (id_sucursal) REFERENCES Sucursales(id_sucursal);

ALTER TABLE Pedidos ADD CONSTRAINT fk_pedidos_cliente FOREIGN KEY (id_cliente) REFERENCES Clientes(id_cliente);
ALTER TABLE Pedidos ADD CONSTRAINT fk_pedidos_producto FOREIGN KEY (id_producto) REFERENCES Productos(id_producto);

ALTER TABLE Pago ADD CONSTRAINT fk_pago_venta FOREIGN KEY (id_venta) REFERENCES Ventas(id_venta);

ALTER TABLE Sector_Venta ADD CONSTRAINT fk_sectorv_sucursal FOREIGN KEY (id_sucursal) REFERENCES Sucursales(id_sucursal);

ALTER TABLE Cuentas_por_saldar ADD CONSTRAINT fk_cuentas_proveedor FOREIGN KEY (id_proveedor) REFERENCES Proveedores(id_proveedor);

ALTER TABLE Total_ventas ADD CONSTRAINT fk_totalventas_sucursal FOREIGN KEY (id_sucursal) REFERENCES Sucursales(id_sucursal);

```
## Datos para las tablas
```sql
INSERT INTO Región (nombre) VALUES 
('Norte'),
('Sur'),
('Este'),
('Oeste'),
('Centro');

INSERT INTO Ciudad (nombre) VALUES
('Barcelona'),
('Madrid'),
('Valencia'),
('Sevilla'),
('Bilbao');

INSERT INTO Sucursales (nombre, direccion, id_ciudad) VALUES
('Sucursal Central Barcelona', 'Passeig de Gràcia 123', 1),
('Sucursal Madrid Norte', 'Calle Serrano 456', 2),
('Sucursal Valencia Centro', 'Avenida del Puerto 789', 3),
('Sucursal Sevilla Este', 'Avenida de la Constitución 321', 4),
('Sucursal Bilbao Sur', 'Gran Vía 654', 5);

UPDATE Ciudad SET id_sucursal = 1 WHERE nombre = 'Barcelona';
UPDATE Ciudad SET id_sucursal = 2 WHERE nombre = 'Madrid';
UPDATE Ciudad SET id_sucursal = 3 WHERE nombre = 'Valencia';
UPDATE Ciudad SET id_sucursal = 4 WHERE nombre = 'Sevilla';
UPDATE Ciudad SET id_sucursal = 5 WHERE nombre = 'Bilbao';

UPDATE Región SET id_ciudad = 1 WHERE nombre = 'Norte';
UPDATE Región SET id_ciudad = 2 WHERE nombre = 'Sur';
UPDATE Región SET id_ciudad = 3 WHERE nombre = 'Este';
UPDATE Región SET id_ciudad = 4 WHERE nombre = 'Oeste';
UPDATE Región SET id_ciudad = 5 WHERE nombre = 'Centro';

INSERT INTO País (nombre, id_region) VALUES
('España', 1),
('Francia', 2),
('Italia', 3),
('Alemania', 4),
('Portugal', 5);

INSERT INTO Proveedores (nombre, telefono, direccion, email, id_pais) VALUES
('Shimano Europe', '+34 912345678', 'Polígono Industrial 1', 'shimano@email.com', 1),
('Trek Bikes EU', '+34 923456789', 'Avenida Principal 2', 'trek@email.com', 2),
('Specialized EU', '+34 934567890', 'Calle Comercial 3', 'specialized@email.com', 3),
('Canyon Bicycles', '+34 945678901', 'Plaza Mayor 4', 'canyon@email.com', 4),
('Scott Sports', '+34 956789012', 'Ronda Industrial 5', 'scott@email.com', 5);

INSERT INTO Bicicleta (marca, tipo_bicicleta, valor, id_proveedor) VALUES
('Trek', 'Montaña', 1499.99, 2),
('Specialized', 'Carretera', 2499.99, 3),
('Canyon', 'Urbana', 899.99, 4),
('Scott', 'Eléctrica', 2999.99, 5),
('Trek', 'BMX', 699.99, 2);

INSERT INTO Productos (nombre, categoria, precio, stock, id_proveedor) VALUES
('Casco Protector', 'Protección', 89.99, 100, 1),
('Luces LED', 'Accesorios', 29.99, 150, 2),
('Candado Seguridad', 'Seguridad', 49.99, 75, 3),
('Bomba de Aire', 'Herramientas', 19.99, 200, 4),
('Kit Reparación', 'Herramientas', 15.99, 120, 5);

INSERT INTO Repuesto (nombre, precio, id_proveedor) VALUES
('Cadena Shimano', 29.99, 1),
('Frenos Disco', 89.99, 2),
('Cambio Trasero', 119.99, 3),
('Rueda Delantera', 149.99, 4),
('Sillín Gel', 39.99, 5);

INSERT INTO Empleados (nombre, cargo, telefono, email, id_sucursal) VALUES
('Ana García', 'Vendedor', '+34 611111111', 'ana@tienda.com', 1),
('Carlos Rodríguez', 'Mecánico', '+34 622222222', 'carlos@tienda.com', 2),
('Laura Martínez', 'Gerente', '+34 633333333', 'laura@tienda.com', 3),
('David Sánchez', 'Vendedor', '+34 644444444', 'david@tienda.com', 4),
('Elena Torres', 'Administrativo', '+34 655555555', 'elena@tienda.com', 5);

INSERT INTO Clientes (nombre, direccion, telefono, email, id_pais) VALUES
('Juan Pérez', 'Calle Mayor 1', '+34 666666666', 'juan@email.com', 1),
('María López', 'Avenida Central 2', '+34 677777777', 'maria@email.com', 2),
('Pedro González', 'Plaza España 3', '+34 688888888', 'pedro@email.com', 3),
('Sara Fernández', 'Calle Nueva 4', '+34 699999999', 'sara@email.com', 4),
('Miguel Ruiz', 'Paseo Marítimo 5', '+34 600000000', 'miguel@email.com', 5);

INSERT INTO Fecha (fecha, descripcion) VALUES
('2024-01-01', 'Año Nuevo'),
('2024-02-14', 'San Valentín'),
('2024-03-19', 'San José'),
('2024-04-01', 'Pascua'),
('2024-05-01', 'Día del Trabajo');

INSERT INTO Ventas (id_cliente, id_vendedor, id_bicicleta, fecha, cantidad, total) VALUES
(1, 1, 1, '2024-01-15', 1, 1499.99),
(2, 1, 2, '2024-02-20', 1, 2499.99),
(3, 4, 3, '2024-03-25', 1, 899.99),
(4, 4, 4, '2024-04-05', 1, 2999.99),
(5, 1, 5, '2024-05-10', 1, 699.99);

INSERT INTO Facturación (id_venta, id_fecha, total) VALUES
(1, 1, 1499.99),
(2, 2, 2499.99),
(3, 3, 899.99),
(4, 4, 2999.99),
(5, 5, 699.99);

INSERT INTO Stock (id_producto, id_sucursal, cantidad) VALUES
(1, 1, 20),
(2, 2, 30),
(3, 3, 15),
(4, 4, 40),
(5, 5, 25);

INSERT INTO Pedidos (id_cliente, id_producto, cantidad, fecha_pedido, estado) VALUES
(1, 1, 1, '2024-01-10', 'Entregado'),
(2, 2, 2, '2024-02-15', 'En proceso'),
(3, 3, 1, '2024-03-20', 'Pendiente'),
(4, 4, 3, '2024-04-01', 'Entregado'),
(5, 5, 2, '2024-05-05', 'En proceso');

INSERT INTO Pago (id_venta, tipo_pago, monto, fecha_pago) VALUES
(1, 'Tarjeta', 1499.99, '2024-01-15'),
(2, 'Efectivo', 2499.99, '2024-02-20'),
(3, 'Transferencia', 899.99, '2024-03-25'),
(4, 'Tarjeta', 2999.99, '2024-04-05'),
(5, 'Efectivo', 699.99, '2024-05-10');

INSERT INTO Sector_Venta (nombre, id_sucursal) VALUES
('Bicicletas', 1),
('Accesorios', 2),
('Repuestos', 3),
('Ropa', 4),
('Taller', 5);

INSERT INTO Cuentas_por_saldar (id_proveedor, monto, fecha_vencimiento, estado) VALUES
(1, 5000.00, '2024-06-01', 'Pendiente'),
(2, 7500.00, '2024-06-15', 'Pendiente'),
(3, 3000.00, '2024-06-30', 'Parcial'),
(4, 4500.00, '2024-07-15', 'Pendiente'),
(5, 2500.00, '2024-07-30', 'Parcial');

INSERT INTO Total_ventas (id_sucursal, total, fecha) VALUES
(1, 15000.00, '2024-01-31'),
(2, 12500.00, '2024-02-28'),
(3, 18000.00, '2024-03-31'),
(4, 13500.00, '2024-04-30'),
(5, 16500.00, '2024-05-31');

```
## Consultas
```sql
SELECT 
    s.nombre AS sucursal,
    c.nombre AS ciudad,
    r.nombre AS region,
    COUNT(v.id_venta) AS numero_ventas,
    SUM(v.total) AS total_ventas
FROM Sucursales s
JOIN Ciudad c ON s.id_ciudad = c.id_ciudad
JOIN Región r ON c.id_ciudad = r.id_ciudad
LEFT JOIN Empleados e ON e.id_sucursal = s.id_sucursal
LEFT JOIN Ventas v ON v.id_vendedor = e.id_empleado
GROUP BY s.nombre, c.nombre, r.nombre
ORDER BY total_ventas DESC;

SELECT 
    e.nombre AS empleado,
    e.cargo,
    s.nombre AS sucursal,
    COUNT(v.id_venta) AS ventas_realizadas,
    SUM(v.total) AS total_vendido,
    ROUND(AVG(v.total), 2) AS promedio_venta
FROM Empleados e
JOIN Sucursales s ON e.id_sucursal = s.id_sucursal
LEFT JOIN Ventas v ON v.id_vendedor = e.id_empleado
WHERE e.cargo = 'Vendedor'
GROUP BY e.nombre, e.cargo, s.nombre
HAVING COUNT(v.id_venta) > 0
ORDER BY total_vendido DESC;

SELECT 
    p.nombre AS producto,
    p.categoria,
    s.cantidad AS stock_actual,
    suc.nombre AS sucursal,
    prov.nombre AS proveedor,
    CASE 
        WHEN s.cantidad < 20 THEN 'Crítico'
        WHEN s.cantidad < 50 THEN 'Bajo'
        ELSE 'Normal'
    END AS nivel_stock
FROM Productos p
JOIN Stock s ON p.id_producto = s.id_producto
JOIN Sucursales suc ON s.id_sucursal = suc.id_sucursal
JOIN Proveedores prov ON p.id_proveedor = prov.id_proveedor
WHERE s.cantidad < 50
ORDER BY s.cantidad ASC;

SELECT 
    b.marca,
    b.tipo_bicicleta,
    r.nombre AS region,
    COUNT(v.id_venta) AS cantidad_vendida,
    SUM(v.total) AS ingresos_totales
FROM Bicicleta b
JOIN Ventas v ON b.id_bicicleta = v.id_bicicleta
JOIN Empleados e ON v.id_vendedor = e.id_empleado
JOIN Sucursales s ON e.id_sucursal = s.id_sucursal
JOIN Ciudad c ON s.id_ciudad = c.id_ciudad
JOIN Región r ON c.id_ciudad = r.id_ciudad
GROUP BY b.marca, b.tipo_bicicleta, r.nombre
ORDER BY cantidad_vendida DESC;

WITH promedio_compras AS (
    SELECT AVG(total) AS promedio_total
    FROM Ventas
)
SELECT 
    c.nombre AS cliente,
    c.email,
    p.nombre AS pais,
    COUNT(v.id_venta) AS numero_compras,
    SUM(v.total) AS total_gastado
FROM Clientes c
JOIN País p ON c.id_pais = p.id_pais
JOIN Ventas v ON c.id_cliente = v.id_cliente
GROUP BY c.nombre, c.email, p.nombre
HAVING SUM(v.total) > (SELECT promedio_total FROM promedio_compras)
ORDER BY total_gastado DESC;

SELECT 
    s.nombre AS sucursal,
    p.tipo_pago,
    COUNT(p.id_pago) AS numero_transacciones,
    SUM(p.monto) AS total_procesado,
    ROUND(AVG(p.monto), 2) AS monto_promedio
FROM Sucursales s
JOIN Empleados e ON s.id_sucursal = e.id_sucursal
JOIN Ventas v ON e.id_empleado = v.id_vendedor
JOIN Pago p ON v.id_venta = p.id_venta
GROUP BY s.nombre, p.tipo_pago
ORDER BY s.nombre, total_procesado DESC;

SELECT 
    p.nombre AS proveedor,
    pais.nombre AS pais,
    COUNT(cps.id_cuenta_por_saldar) AS facturas_pendientes,
    SUM(cps.monto) AS total_pendiente,
    MIN(cps.fecha_vencimiento) AS vencimiento_mas_proximo
FROM Proveedores p
JOIN País pais ON p.id_pais = pais.id_pais
JOIN Cuentas_por_saldar cps ON p.id_proveedor = cps.id_proveedor
WHERE cps.estado = 'Pendiente'
GROUP BY p.nombre, pais.nombre
ORDER BY total_pendiente DESC;

SELECT 
    MONTH(v.fecha) AS mes,
    COUNT(v.id_venta) AS total_ventas,
    SUM(v.total) AS ingresos,
    COUNT(DISTINCT v.id_cliente) AS clientes_unicos,
    ROUND(AVG(v.total), 2) AS ticket_promedio
FROM Ventas v
GROUP BY MONTH(v.fecha)
ORDER BY mes;

SELECT 
    DATEDIFF(MIN(v.fecha), p.fecha_pedido) AS tiempo_entrega,
    p.estado,
    COUNT(p.id_pedido) AS numero_pedidos,
    c.nombre AS cliente,
    s.nombre AS sucursal
FROM Pedidos p
JOIN Clientes c ON p.id_cliente = c.id_cliente
JOIN Productos prod ON p.id_producto = prod.id_producto
JOIN Stock st ON prod.id_producto = st.id_producto
JOIN Sucursales s ON st.id_sucursal = s.id_sucursal
LEFT JOIN Ventas v ON p.id_cliente = v.id_cliente
GROUP BY p.estado, c.nombre, s.nombre, p.fecha_pedido
HAVING tiempo_entrega IS NOT NULL
ORDER BY tiempo_entrega;

WITH ventas_por_producto AS (
    SELECT 
        p.id_producto,
        p.nombre,
        p.categoria,
        p.precio AS precio_unitario,
        SUM(ped.cantidad) AS unidades_vendidas,
        p.precio * SUM(ped.cantidad) AS ingresos_totales
    FROM Productos p
    JOIN Pedidos ped ON p.id_producto = ped.id_producto
    GROUP BY p.id_producto, p.nombre, p.categoria, p.precio
)
SELECT 
    categoria,
    COUNT(id_producto) AS numero_productos,
    SUM(unidades_vendidas) AS total_unidades,
    ROUND(AVG(precio_unitario), 2) AS precio_promedio,
    SUM(ingresos_totales) AS ingresos_totales
FROM ventas_por_producto
GROUP BY categoria
ORDER BY ingresos_totales DESC;

```

Hecho por (Luis Alberto Talero Martinez)

> [!NOTE]
> complicaciones 

> [!IMPORTANT]  
> se encuentra culminado 
