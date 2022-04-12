 --**************************************************
--Database Project 3
--Submission Date: 11-19-2021
--Author: Blake Prebeck
--**************************************************


--///////////////////
--Create DB
--///////////////////

use master;
go
drop database Steins;
go
create database Steins;
go
use Steins;

--///////////////////
--Create Tables
--///////////////////

--Create Person table
create table Person (
	PersonID    int         Not Null  identity(6000,1),
	NameFirst   char(30)    Not Null,
	NameLast    char(30)    Not Null,
	Address     char(50)    Not Null,
	City        char(30)    Not Null,
	State       char(2)     Not Null    default 'MI',
	Zip         char(5)     Not Null ,
	Phone       char(12)    Not Null    default 'No Phone',
	Email       varchar(50) Not Null    default 'No Email',
	Category    char(4)     Not Null,
	--Primary Key Constraint 
	constraint Person_PersonID_pk primary Key(PersonID),
	--Check Constraint
	constraint Person_Category_ck check (Category in ('cust','empl')),
);
go

--Create Customer table
create table Customer (
	PersonID	int			    Not Null,
	Status		char(15)	    Not Null,
	--primary key
	constraint customer_personid_pk primary key(PersonID),
	--foreign key
	constraint customer_personid_fk foreign key(PersonID) references Person(PersonID)
		on update cascade
		on delete no action
);
go

--Create Employee table
create table Employee (
	PersonID	    int				    Not Null,
	SSN			    char(11)			Not Null, 
	HireDate	    date			    Not Null,
	Pay			    decimal(9,2)	    Not Null,
	--primary key
	constraint employee_personid_pk primary key(PersonID),
	--foreign key
	constraint employee_personid_fk foreign key(PersonID) references Person(PersonID)
		on update cascade 
		on delete no action,
	--Unique Constraint
	constraint Employee_SSN_uk unique(SSN)
);
go

--Create Product Table
create table Product (
    ProductID           int             not null    identity(3000,1), 
    ProductName         char(30)        not null    default 'No Description',
    ProductDesc         varchar(50)     not null,
    ProductCost         decimal(9,2)    not null,
	--PK Constraint
	constraint Product_ProductID_pk primary key (ProductID),
);
go

--Create Inventory Table
create table Inventory (
    ProductID           int             not null,
    OnHand              int             not null,
    ReorderAmt          int             not null,
    --PK Constraint
	constraint Inventory_ProductID_pk primary key (ProductID),
	--FK Constraint
	constraint Inventory_ProductID_fk foreign key (ProductID) references Product (ProductID)
		on update cascade
		on delete no action,
    --CK Constraint
    constraint Inventory_OnHand_ck check (OnHand >= 0),
    constraint Inventory_ReorderAmt_ck check (ReorderAmt >= 0 ),
);
go

--Create Order table
create table Customer_Order (
	OrderID		    int			Not Null	identity(7000,1),
	OrderDate	    date		Not Null,
	CustomerID	    int			Not Null,
	EmployeeID	    int			Not Null,
	--Primary Key Constraint 
	constraint Customer_Order_OrderID_pk primary Key(OrderID),
	--Foreign Key Constraints
	constraint Customer_Order_CustomerID_fk foreign key(CustomerID) references Person(PersonID)
		on update cascade
		on delete no action,
	constraint Customer_Order_EmployeeID_fk foreign key(EmployeeID) references Person(PersonID)
		on update no action
		on delete no action
);
go

--Create Order_Product table
create table Order_Product (
	OrderID			int				    Not Null,
	ProductID		int			  	    Not Null,
	Price			decimal(9,2)	    Not Null,
	Quantity		int				    Not Null,
	--Primary Key Constraint
	constraint Order_Product_OrderProduct_pk primary key(OrderID, ProductID),
	--Foreign Key Constraints
	constraint Order_Product_Order_fk foreign key (OrderID) references Customer_Order(OrderID)
		on update cascade
		on delete no action,
	constraint Order_Product_Product_fk foreign key (ProductID) references Product(ProductID)
		on update cascade
		on delete no action,
	--Check Constraint
	constraint Order_Product_Quantity_ck check (Quantity <= 10)
);
go


--///////////////////
--Insert Data
--///////////////////

--Insert Data Into Person
insert into Person
	( NameLast, NameFirst, Address, City, Zip, Phone, Email, Category)
VALUES
	('Jameson','Adam','2345 Oak','Mt. Clemens','48043','586-555-7777','QuigM@yahoo.com','empl'),
	('Jameson','William','2345 Oak', 'Mt. Clemens','48043','586-555-8595', 'QuigM@yahoo.com','empl'),
	('Clarkston','Juliet','4762 N. River Rd.','Clinton Twp.','48036','586-555-4785', 'SamTheMan@gmailcom', 'cust'),
	('Madill','Danielle', '9894 Iron Wood Way', 'Rochester', '48306','586-555-6987', 'Scottie@comcast.net', 'cust'),
	('Bensinger','Sheryl','48694 Kelly Lea', 'Chesterfield', '48051', '586-555-6523', 'PattyCake@gmail.com','cust'),
	('Madill', 'Jayson', '4320 Village Oak Ln','Shelby Twp.','48315','586-555-7615', 'Jgreg@yahoo.com','cust'),
	('Smit', 'Joe', '8945 Forest', 'Shelby Twp.', '48315', '586-555-7397', 'MLeaf@comcast.net','cust'),
	('Garcia', 'Alice', '5673 Port Austin','Port Austin', '48467','586-555-7348', 'Griffie@comcast.net','cust'),
	('Sands','Pete', '84344 Stork','Shelby Twp.','48315','586-555-7841', 'Paulie@comcast.net','cust'),
	('Miller', 'Walt', '8434 Pin Oak', 'Shelby Twp.', '48315','555-555-5555', 'bateman19m@att.net','cust');
	go

--Inserting Data Into Customer Table
insert into Customer
    (PersonID, Status)
values
    (6002, 'Retail'),
    (6003, 'Retail'),
    (6004, 'Commercial'),
    (6005, 'Retail'),
    (6006, 'Retail'),
    (6007, 'Retail'),
    (6008, 'Commercial'),
    (6009, 'Commercial');
go

--Inserting Data Into Employee Table
insert into Employee
    (PersonID, SSN, HireDate, Pay)
values
    (6000, '555-12-3456', '2016-09-01', 20.00),
    (6001, '555-23-4567', '2020-02-11', 15.50);
go

--Inserting Data Into Product Table
insert into Product
    (ProductName, ProductDesc, ProductCost)
values
    ('Advertise Decades', 'Budweiser', 50.00),
    ('Birth of a Nation', 'Miller', 10.00),
    ('Bavarian', 'Strohs', 20.00),
    ('Corona Beer', 'Corona', 105.00),
    ('Disney Series', 'Disney', 30.00),
    ('Heritage', 'Coors', 8.00),
    ('Calendar Girl', 'Budweiser', 35.00),
    ('Civil War Series', 'Budweiser', 125.00),
    ('Clydesdale', 'Budweiser', 30.00),
    ('Lighthouse', 'Budweiser', 75.00);
go

--Inserting Data Into Inventory Table
insert into Inventory
    (ProductID, OnHand, ReorderAmt)
values
    (3000, 4, 1),
    (3001, 2, 3),
    (3002, 3, 2),
    (3003, 2, 3),
    (3004, 2, 3),
    (3005, 3, 2),
    (3006, 3, 2),
    (3007, 2, 3),
    (3008, 5, 0),
    (3009, 3, 2);
go

--Inserting Data Into Customer_Order Table
insert into Customer_Order
    (OrderDate, CustomerID, EmployeeID)
values
    ('2019-02-02', 6002, 6000),
    ('2019-03-09', 6003, 6001),
    ('2020-04-24', 6004, 6000),
    ('2020-07-27', 6005, 6001),
    ('2020-09-03', 6006, 6000),
    ('2021-01-14', 6007, 6001),
    ('2021-03-20', 6008, 6000),
    ('2021-05-27', 6009, 6001),
    ('2021-06-21', 6002, 6000),
    ('2021-11-17', 6003, 6001);
go

--Inserting Data Into Order_Product Table
insert into Order_Product
    (OrderID, ProductID, Price, Quantity)
values
    (7000, 3000, 95.00, 2), 
    (7001, 3001, 30.00, 2),
    (7002, 3002, 70.00, 2),
    (7003, 3003, 185.00, 1),
    (7004, 3004, 95.00, 2),
    (7005, 3005, 15.00, 3),
    (7006, 3006, 65.00, 2),
    (7007, 3007, 220.00, 1),
    (7008, 3008, 60.00, 3),
    (7009, 3009, 150.00, 1);
go
