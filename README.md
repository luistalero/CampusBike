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
