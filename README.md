## E-Commerce Database Design and analysis
### DB Schema Script 

create database store;
use store;

create table if not exists category (
category_id int auto_increment primary key,
category_name varchar(50) not null
)auto_increment=1;

create table if not exists product (
product_id int auto_increment primary key,
category_id int,
product_name varchar(50) not null,
description text not null,
price numeric(9,2) not null,
stock_quantity int,
constraint product_category_fk foreign key (category_id) references category (category_id)
) auto_increment=1;

create table if not exists customer (
customer_id int auto_increment primary key,
first_name varchar(50) not null,
last_name varchar(50) not null,
email varchar(100) not null,
password varchar(50) not null
)auto_increment=1;

create table if not exists orders (
order_id int auto_increment primary key,
customer_id int,
order_date date DEFAULT (CURRENT_DATE),
total_amount numeric(10,2) not null,
constraint customer_order_fk foreign key (customer_id) references customer (customer_id)
)auto_increment=1;

create table if not exists order_details (
order_detail_id int auto_increment primary key,
order_id int,
product_id int,
quantity int not null,
unit_price numeric(9,2) not null,
constraint order_order_details_fk foreign key (order_id) references orders (order_id),
constraint product_order_details_fk foreign key (product_id) references product (product_id)
)auto_increment=1;
