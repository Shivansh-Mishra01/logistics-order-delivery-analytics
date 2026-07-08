create database LogisticsDB;
use LogisticsDB;
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY AUTO_INCREMENT,
    customer_name VARCHAR(100) NOT NULL,
    phone VARCHAR(15) UNIQUE,
    city VARCHAR(50) NOT NULL
);
CREATE TABLE Drivers (
    driver_id INT PRIMARY KEY AUTO_INCREMENT,
    driver_name VARCHAR(100) NOT NULL,
    phone VARCHAR(15) UNIQUE,
    license_no VARCHAR(30) UNIQUE NOT NULL
);
CREATE TABLE Vehicles (
    vehicle_id INT PRIMARY KEY AUTO_INCREMENT,
    vehicle_no VARCHAR(20) UNIQUE NOT NULL,
    vehicle_type VARCHAR(50),
    capacity INT
);
CREATE TABLE Routes (
    route_id INT PRIMARY KEY AUTO_INCREMENT,
    source_city VARCHAR(50) NOT NULL,
    destination_city VARCHAR(50) NOT NULL,
    distance INT
);
CREATE TABLE Orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT NOT NULL,
    order_date DATE,
    shipment_value DECIMAL(10,2),
    status VARCHAR(30),

    FOREIGN KEY (customer_id)
    REFERENCES Customers(customer_id)
);
CREATE TABLE Shipments (
    shipment_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT NOT NULL,
    driver_id INT NOT NULL,
    vehicle_id INT NOT NULL,
    route_id INT NOT NULL,
    dispatch_date DATE,
    delivery_date DATE,
    status VARCHAR(30),

    FOREIGN KEY (order_id) REFERENCES Orders(order_id),
    FOREIGN KEY (driver_id) REFERENCES Drivers(driver_id),
    FOREIGN KEY (vehicle_id) REFERENCES Vehicles(vehicle_id),
    FOREIGN KEY (route_id) REFERENCES Routes(route_id)
);
CREATE TABLE Invoices (
    invoice_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT NOT NULL,
    amount DECIMAL(10,2),
    invoice_date DATE,

    FOREIGN KEY (order_id)
    REFERENCES Orders(order_id)
);
CREATE TABLE Payments (
    payment_id INT PRIMARY KEY AUTO_INCREMENT,
    invoice_id INT NOT NULL,
    payment_date DATE,
    payment_status VARCHAR(20),

    FOREIGN KEY (invoice_id)
    REFERENCES Invoices(invoice_id)
);
INSERT INTO Customers (customer_name, phone, city) VALUES
('Customer1','9870000001','City1'),
('Customer2','9870000002','City2'),
('Customer3','9870000003','City3'),
('Customer4','9870000004','City4'),
('Customer5','9870000005','City0'),
('Customer6','9870000006','City1'),
('Customer7','9870000007','City2'),
('Customer8','9870000008','City3'),
('Customer9','9870000009','City4'),
('Customer10','9870000010','City0'),
('Customer11','9870000011','City1'),
('Customer12','9870000012','City2'),
('Customer13','9870000013','City3'),
('Customer14','9870000014','City4'),
('Customer15','9870000015','City0');

INSERT INTO Drivers (driver_name, phone, license_no) VALUES
('Driver1','9770000001','LIC0001'),
('Driver2','9770000002','LIC0002'),
('Driver3','9770000003','LIC0003'),
('Driver4','9770000004','LIC0004'),
('Driver5','9770000005','LIC0005'),
('Driver6','9770000006','LIC0006'),
('Driver7','9770000007','LIC0007'),
('Driver8','9770000008','LIC0008'),
('Driver9','9770000009','LIC0009'),
('Driver10','9770000010','LIC0010'),
('Driver11','9770000011','LIC0011'),
('Driver12','9770000012','LIC0012'),
('Driver13','9770000013','LIC0013'),
('Driver14','9770000014','LIC0014'),
('Driver15','9770000015','LIC0015');

INSERT INTO Vehicles (vehicle_no, vehicle_type, capacity) VALUES
('UP16AA0001','Truck',5100),
('UP16AA0002','Truck',5200),
('UP16AA0003','Truck',5300),
('UP16AA0004','Truck',5400),
('UP16AA0005','Truck',5500),
('UP16AA0006','Truck',5600),
('UP16AA0007','Truck',5700),
('UP16AA0008','Truck',5800),
('UP16AA0009','Truck',5900),
('UP16AA0010','Truck',6000),
('UP16AA0011','Truck',6100),
('UP16AA0012','Truck',6200),
('UP16AA0013','Truck',6300),
('UP16AA0014','Truck',6400),
('UP16AA0015','Truck',6500);

INSERT INTO Routes (source_city, destination_city, distance) VALUES
('City1','City2',60),
('City2','City3',70),
('City3','City4',80),
('City4','City5',90),
('City5','City6',100),
('City6','City7',110),
('City7','City8',120),
('City8','City9',130),
('City9','City10',140),
('City10','City11',150);

INSERT INTO Orders (customer_id, order_date, shipment_value, status) VALUES
(2,'2026-07-02',10500,'Delivered'),
(3,'2026-07-03',11000,'Delivered'),
(4,'2026-07-04',11500,'Pending'),
(5,'2026-07-05',12000,'Delivered'),
(6,'2026-07-06',12500,'Delivered'),
(7,'2026-07-07',13000,'Pending'),
(8,'2026-07-08',13500,'Delivered'),
(9,'2026-07-09',14000,'Delivered'),
(10,'2026-07-10',14500,'Pending'),
(11,'2026-07-11',15000,'Delivered'),
(12,'2026-07-12',15500,'Delivered'),
(13,'2026-07-13',16000,'Pending'),
(14,'2026-07-14',16500,'Delivered'),
(15,'2026-07-15',17000,'Delivered'),
(1,'2026-07-16',17500,'Pending'),
(2,'2026-07-17',18000,'Delivered'),
(3,'2026-07-18',18500,'Delivered'),
(4,'2026-07-19',19000,'Pending'),
(5,'2026-07-20',19500,'Delivered'),
(6,'2026-07-21',20000,'Delivered');

INSERT INTO Shipments (order_id, driver_id, vehicle_id, route_id, dispatch_date, delivery_date, status) VALUES
(1,2,2,2,'2026-07-02','2026-07-03','Delivered'),
(2,3,3,3,'2026-07-03','2026-07-04','Delivered'),
(3,4,4,4,'2026-07-04','2026-07-05','Delivered'),
(4,5,5,5,'2026-07-05',NULL,'In Transit'),
(5,6,6,6,'2026-07-06','2026-07-07','Delivered'),
(6,7,7,7,'2026-07-07','2026-07-08','Delivered'),
(7,8,8,8,'2026-07-08','2026-07-09','Delivered'),
(8,9,9,9,'2026-07-09',NULL,'In Transit'),
(9,10,10,10,'2026-07-10','2026-07-11','Delivered'),
(10,11,11,1,'2026-07-11','2026-07-12','Delivered'),
(11,12,12,2,'2026-07-12','2026-07-13','Delivered'),
(12,13,13,3,'2026-07-13',NULL,'In Transit'),
(13,14,14,4,'2026-07-14','2026-07-15','Delivered'),
(14,15,15,5,'2026-07-15','2026-07-16','Delivered'),
(15,1,1,6,'2026-07-16','2026-07-17','Delivered'),
(16,2,2,7,'2026-07-17',NULL,'In Transit'),
(17,3,3,8,'2026-07-18','2026-07-19','Delivered'),
(18,4,4,9,'2026-07-19','2026-07-20','Delivered'),
(19,5,5,10,'2026-07-20','2026-07-21','Delivered'),
(20,6,6,1,'2026-07-21',NULL,'In Transit');

INSERT INTO Invoices (order_id, amount, invoice_date) VALUES
(1,10500,'2026-07-02'),
(2,11000,'2026-07-03'),
(3,11500,'2026-07-04'),
(4,12000,'2026-07-05'),
(5,12500,'2026-07-06'),
(6,13000,'2026-07-07'),
(7,13500,'2026-07-08'),
(8,14000,'2026-07-09'),
(9,14500,'2026-07-10'),
(10,15000,'2026-07-11'),
(11,15500,'2026-07-12'),
(12,16000,'2026-07-13'),
(13,16500,'2026-07-14'),
(14,17000,'2026-07-15'),
(15,17500,'2026-07-16'),
(16,18000,'2026-07-17'),
(17,18500,'2026-07-18'),
(18,19000,'2026-07-19'),
(19,19500,'2026-07-20'),
(20,20000,'2026-07-21');

INSERT INTO Payments (invoice_id, payment_date, payment_status) VALUES
(1,'2026-07-04','Paid'),
(2,'2026-07-05','Paid'),
(3,'2026-07-06','Paid'),
(4,NULL,'Pending'),
(5,'2026-07-08','Paid'),
(6,'2026-07-09','Paid'),
(7,'2026-07-10','Paid'),
(8,NULL,'Pending'),
(9,'2026-07-12','Paid'),
(10,'2026-07-13','Paid'),
(11,'2026-07-14','Paid'),
(12,NULL,'Pending'),
(13,'2026-07-16','Paid'),
(14,'2026-07-17','Paid'),
(15,'2026-07-18','Paid'),
(16,NULL,'Pending'),
(17,'2026-07-20','Paid'),
(18,'2026-07-21','Paid'),
(19,'2026-07-22','Paid'),
(20,NULL,'Pending');
# TOTAL CUSTOMERS 
SELECT COUNT(*) AS Total_Customers
FROM Customers;

#Total Orders
SELECT COUNT(*) AS Total_Orders
FROM Orders;

# Customer Wise Orders (JOIN)
SELECT c.customer_name, o.order_id, o.shipment_value
FROM Customers c
JOIN Orders o
ON c.customer_id = o.customer_id;

# Top 5 Customers by Shipment Value
SELECT c.customer_name,
SUM(o.shipment_value) AS Total_Value
FROM Customers c
JOIN Orders o
ON c.customer_id = o.customer_id
GROUP BY c.customer_name
ORDER BY Total_Value DESC
LIMIT 5;

# Driver Wise Deliveries
SELECT d.driver_name,
COUNT(s.shipment_id) AS Total_Deliveries
FROM Drivers d
JOIN Shipments s
ON d.driver_id = s.driver_id
GROUP BY d.driver_name;

# Delayed Shipments
SELECT shipment_id,
order_id,
driver_id,
delivery_date
FROM Shipments
WHERE status='Delayed';

# Pending Payments
SELECT invoice_id,
payment_status
FROM Payments
WHERE payment_status='Pending';

# Monthly Revenue
SELECT MONTH(order_date) AS Month,
SUM(shipment_value) AS Revenue
FROM Orders
GROUP BY MONTH(order_date);

# Highest Shipment Value
SELECT *
FROM Orders
ORDER BY shipment_value DESC
LIMIT 1;

# Complete Shipment Report (Multi-Table JOIN)
SELECT
c.customer_name,
o.order_id,
d.driver_name,
v.vehicle_no,
r.source_city,
r.destination_city,
s.status
FROM Shipments s
JOIN Orders o ON s.order_id=o.order_id
JOIN Customers c ON o.customer_id=c.customer_id
JOIN Drivers d ON s.driver_id=d.driver_id
JOIN Vehicles v ON s.vehicle_id=v.vehicle_id
JOIN Routes r ON s.route_id=r.route_id;

# Customer Order Report
DELIMITER $$
CREATE PROCEDURE CustomerOrderReport()
BEGIN
    SELECT
        c.customer_id,
        c.customer_name,
        COUNT(o.order_id) AS Total_Orders,
        SUM(o.shipment_value) AS Total_Shipment_Value
    FROM Customers c
    JOIN Orders o
        ON c.customer_id = o.customer_id
    GROUP BY c.customer_id, c.customer_name;
END $$
DELIMITER ;

# Pending Payments Report
DELIMITER $$
CREATE PROCEDURE PendingPayments()
BEGIN
    SELECT
        i.invoice_id,
        i.amount,
        p.payment_status
    FROM Invoices i
    JOIN Payments p
        ON i.invoice_id = p.invoice_id
    WHERE p.payment_status = 'Pending';
END $$
DELIMITER ;

CALL CustomerOrderReport();
CALL PendingPayments();

