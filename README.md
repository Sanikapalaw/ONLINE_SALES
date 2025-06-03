Online Sales Data Setup and Analysis
This repository contains SQL scripts for setting up an online_sales database, populating it with sample data, and performing various sales trend analyses using aggregate functions.

Objective
The primary objective is to demonstrate how to:

Create a database and a detailed online_sales table.

Insert sample sales data into the table.

Analyze sales trends by month, year, quarter, and specific categories using SQL aggregate functions like SUM() and COUNT(DISTINCT).

Identify top-performing periods based on revenue.

Database Setup and Data Population
The following SQL commands are used to create the database, define the online_sales table schema, and insert sample records.

1. Create Database and Select It
CREATE DATABASE online_sales;
USE online_sales;

2. Create online_sales Table
This table stores detailed information about each online order.

CREATE TABLE online_sales (
    order_id INT PRIMARY KEY,
    order_date DATE NOT NULL,
    amount DECIMAL(10, 2) NOT NULL,
    product_id INT,
    customer_id INT NOT NULL,
    product_name VARCHAR(100) NOT NULL,
    category VARCHAR(50) NOT NULL,
    price_per_unit DECIMAL(10, 2) NOT NULL,
    quantity INT NOT NULL,
    discount_amount DECIMAL(10, 2) DEFAULT 0,
    shipping_cost DECIMAL(10, 2) DEFAULT 0,
    payment_method VARCHAR(50) NOT NULL,
    order_status VARCHAR(50) NOT NULL,
    delivery_date DATE,
    region VARCHAR(50),
    customer_segment VARCHAR(50),
    referral_source VARCHAR(100),
    currency VARCHAR(5) DEFAULT 'USD'
);

3. Insert Sample Data
A comprehensive set of 80 sample records are inserted into the online_sales table, covering sales data from 2022 to 2025.

INSERT INTO online_sales (
    order_id, order_date, amount, product_id, customer_id, product_name, category,
    price_per_unit, quantity, discount_amount, shipping_cost, payment_method,
    order_status, delivery_date, region, customer_segment, referral_source, currency
) VALUES
(1, '2022-01-05', 120.50, 101, 1001, 'Laptop Basic', 'Electronics', 110.00, 1, 0.00, 10.50, 'Credit Card', 'Completed', '2022-01-10', 'North', 'New', 'Google', 'USD'),
(2, '2022-01-15', 200.00, 102, 1002, 'Wireless Mouse', 'Accessories', 25.00, 8, 0.00, 0.00, 'PayPal', 'Completed', '2022-01-20', 'South', 'Loyal', 'Direct', 'USD'),
(3, '2022-01-20', 75.25, 103, 1003, 'USB Hub', 'Accessories', 15.00, 5, 0.00, 0.25, 'Debit Card', 'Completed', '2022-01-25', 'East', 'New', 'Social Media', 'USD'),
(4, '2022-02-10', 150.00, 101, 1004, 'Laptop Basic', 'Electronics', 140.00, 1, 0.00, 10.00, 'Credit Card', 'Completed', '2022-02-15', 'West', 'Loyal', 'Google', 'USD'),
(5, '2022-02-22', 300.75, 104, 1005, 'Gaming Keyboard', 'Peripherals', 100.00, 3, 0.00, 0.75, 'PayPal', 'Completed', '2022-02-27', 'North', 'New', 'Ad Campaign', 'USD'),
(6, '2022-03-01', 90.00, 102, 1001, 'Wireless Mouse', 'Accessories', 20.00, 4, 0.00, 10.00, 'Credit Card', 'Completed', '2022-03-05', 'South', 'Loyal', 'Direct', 'USD'),
(7, '2022-03-18', 180.20, 105, 1006, 'External SSD', 'Storage', 170.00, 1, 0.00, 10.20, 'Debit Card', 'Completed', '2022-03-23', 'East', 'New', 'Referral', 'USD'),
(8, '2022-04-05', 250.00, 101, 1002, 'Laptop Basic', 'Electronics', 240.00, 1, 0.00, 10.00, 'Credit Card', 'Completed', '2022-04-10', 'West', 'Loyal', 'Google', 'USD'),
(9, '2022-04-12', 110.50, 103, 1007, 'USB Hub', 'Accessories', 20.00, 5, 0.00, 10.50, 'PayPal', 'Completed', '2022-04-17', 'North', 'New', 'Social Media', 'USD'),
(10, '2022-05-01', 400.00, 104, 1003, 'Gaming Keyboard', 'Peripherals', 130.00, 3, 0.00, 10.00, 'Debit Card', 'Completed', '2022-05-06', 'South', 'Loyal', 'Ad Campaign', 'USD'),
(11, '2022-05-19', 85.00, 102, 1008, 'Wireless Mouse', 'Accessories', 20.00, 4, 0.00, 5.00, 'Credit Card', 'Completed', '2022-05-24', 'East', 'New', 'Direct', 'USD'),
(12, '2022-06-03', 160.00, 101, 1004, 'Laptop Basic', 'Electronics', 150.00, 1, 0.00, 10.00, 'PayPal', 'Completed', '2022-06-08', 'West', 'Loyal', 'Google', 'USD'),
(13, '2022-06-25', 210.50, 105, 1009, 'External SSD', 'Storage', 200.00, 1, 0.00, 10.50, 'Debit Card', 'Completed', '2022-06-30', 'North', 'New', 'Referral', 'USD'),
(14, '2022-07-08', 130.00, 103, 1005, 'USB Hub', 'Accessories', 25.00, 5, 0.00, 5.00, 'Credit Card', 'Completed', '2022-07-13', 'South', 'Loyal', 'Social Media', 'USD'),
(15, '2022-07-30', 270.00, 104, 1010, 'Gaming Keyboard', 'Peripherals', 90.00, 3, 0.00, 0.00, 'PayPal', 'Completed', '2022-08-04', 'East', 'New', 'Ad Campaign', 'USD'),
(16, '2022-08-14', 95.00, 102, 1006, 'Wireless Mouse', 'Accessories', 20.00, 4, 0.00, 15.00, 'Debit Card', 'Completed', '2022-08-19', 'West', 'Loyal', 'Direct', 'USD'),
(17, '2022-08-28', 190.00, 101, 1011, 'Laptop Basic', 'Electronics', 180.00, 1, 0.00, 10.00, 'Credit Card', 'Completed', '2022-09-02', 'North', 'New', 'Google', 'USD'),
(18, '2022-09-07', 320.00, 105, 1007, 'External SSD', 'Storage', 310.00, 1, 0.00, 10.00, 'PayPal', 'Completed', '2022-09-12', 'South', 'Loyal', 'Referral', 'USD'),
(19, '2022-09-21', 140.00, 103, 1012, 'USB Hub', 'Accessories', 25.00, 5, 0.00, 15.00, 'Debit Card', 'Completed', '2022-09-26', 'East', 'New', 'Social Media', 'USD'),
(20, '2022-10-02', 280.00, 104, 1008, 'Gaming Keyboard', 'Peripherals', 90.00, 3, 0.00, 10.00, 'Credit Card', 'Completed', '2022-10-07', 'West', 'Loyal', 'Ad Campaign', 'USD'),
(21, '2022-10-17', 105.00, 102, 1013, 'Wireless Mouse', 'Accessories', 20.00, 5, 0.00, 5.00, 'PayPal', 'Completed', '2022-10-22', 'North', 'New', 'Direct', 'USD'),
(22, '2022-11-04', 350.00, 101, 1009, 'Laptop Basic', 'Electronics', 340.00, 1, 0.00, 10.00, 'Debit Card', 'Completed', '2022-11-09', 'South', 'Loyal', 'Google', 'USD'),
(23, '2022-11-20', 170.00, 105, 1014, 'External SSD', 'Storage', 160.00, 1, 0.00, 10.00, 'Credit Card', 'Completed', '2022-11-25', 'East', 'New', 'Referral', 'USD'),
(24, '2022-12-01', 450.00, 104, 1010, 'Gaming Keyboard', 'Peripherals', 140.00, 3, 0.00, 30.00, 'PayPal', 'Completed', '2022-12-06', 'West', 'Loyal', 'Ad Campaign', 'USD'),
(25, '2022-12-15', 220.00, 103, 1015, 'USB Hub', 'Accessories', 25.00, 8, 0.00, 20.00, 'Debit Card', 'Completed', '2022-12-20', 'North', 'New', 'Social Media', 'USD'),
(26, '2023-01-10', 130.00, 101, 1001, 'Laptop Basic', 'Electronics', 120.00, 1, 0.00, 10.00, 'Credit Card', 'Completed', '2023-01-15', 'South', 'Loyal', 'Google', 'USD'),
(27, '2023-01-25', 210.00, 102, 1002, 'Wireless Mouse', 'Accessories', 25.00, 8, 0.00, 10.00, 'PayPal', 'Completed', '2023-01-30', 'East', 'Loyal', 'Direct', 'USD'),
(28, '2023-02-05', 80.00, 103, 1003, 'USB Hub', 'Accessories', 15.00, 5, 0.00, 5.00, 'Debit Card', 'Completed', '2023-02-10', 'West', 'Loyal', 'Social Media', 'USD'),
(29, '2023-02-18', 160.00, 104, 1004, 'Gaming Keyboard', 'Peripherals', 70.00, 2, 0.00, 20.00, 'Credit Card', 'Completed', '2023-02-23', 'North', 'Loyal', 'Ad Campaign', 'USD'),
(30, '2023-03-03', 310.00, 105, 1005, 'External SSD', 'Storage', 300.00, 1, 0.00, 10.00, 'PayPal', 'Completed', '2023-03-08', 'South', 'Loyal', 'Referral', 'USD'),
(31, '2023-03-20', 100.00, 101, 1006, 'Laptop Basic', 'Electronics', 90.00, 1, 0.00, 10.00, 'Debit Card', 'Completed', '2023-03-25', 'East', 'Loyal', 'Google', 'USD'),
(32, '2023-04-01', 260.00, 102, 1007, 'Wireless Mouse', 'Accessories', 25.00, 10, 0.00, 10.00, 'Credit Card', 'Completed', '2023-04-06', 'West', 'Loyal', 'Direct', 'USD'),
(33, '2023-04-15', 120.00, 103, 1008, 'USB Hub', 'Accessories', 20.00, 5, 0.00, 20.00, 'PayPal', 'Completed', '2023-04-20', 'North', 'Loyal', 'Social Media', 'USD'),
(34, '2023-05-08', 410.00, 104, 1009, 'Gaming Keyboard', 'Peripherals', 130.00, 3, 0.00, 20.00, 'Debit Card', 'Completed', '2023-05-13', 'South', 'Loyal', 'Ad Campaign', 'USD'),
(35, '2023-05-25', 90.00, 105, 1010, 'External SSD', 'Storage', 80.00, 1, 0.00, 10.00, 'Credit Card', 'Completed', '2023-05-30', 'East', 'Loyal', 'Referral', 'USD'),
(36, '2023-06-07', 170.00, 101, 1011, 'Laptop Basic', 'Electronics', 160.00, 1, 0.00, 10.00, 'PayPal', 'Completed', '2023-06-12', 'West', 'Loyal', 'Google', 'USD'),
(37, '2023-06-20', 220.00, 102, 1012, 'Wireless Mouse', 'Accessories', 25.00, 8, 0.00, 20.00, 'Debit Card', 'Completed', '2023-06-25', 'North', 'Loyal', 'Direct', 'USD'),
(38, '2023-07-01', 140.00, 103, 1013, 'USB Hub', 'Accessories', 20.00, 6, 0.00, 20.00, 'Credit Card', 'Completed', '2023-07-06', 'South', 'Loyal', 'Social Media', 'USD'),
(39, '2023-07-16', 280.00, 104, 1014, 'Gaming Keyboard', 'Peripherals', 90.00, 3, 0.00, 10.00, 'PayPal', 'Completed', '2023-07-21', 'East', 'Loyal', 'Ad Campaign', 'USD'),
(40, '2023-08-09', 100.00, 105, 1015, 'External SSD', 'Storage', 90.00, 1, 0.00, 10.00, 'Debit Card', 'Completed', '2023-08-14', 'West', 'Loyal', 'Referral', 'USD'),
(41, '2023-08-22', 200.00, 101, 1001, 'Laptop Basic', 'Electronics', 190.00, 1, 0.00, 10.00, 'Credit Card', 'Completed', '2023-08-27', 'North', 'Loyal', 'Google', 'USD'),
(42, '2023-09-05', 330.00, 102, 1002, 'Wireless Mouse', 'Accessories', 25.00, 12, 0.00, 30.00, 'PayPal', 'Completed', '2023-09-10', 'South', 'Loyal', 'Direct', 'USD'),
(43, '2023-09-19', 150.00, 103, 1003, 'USB Hub', 'Accessories', 20.00, 7, 0.00, 10.00, 'Debit Card', 'Completed', '2023-09-24', 'East', 'Loyal', 'Social Media', 'USD'),
(44, '2023-10-01', 290.00, 104, 1004, 'Gaming Keyboard', 'Peripherals', 90.00, 3, 0.00, 20.00, 'Credit Card', 'Completed', '2023-10-06', 'West', 'Loyal', 'Ad Campaign', 'USD'),
(45, '2023-10-14', 110.00, 105, 1005, 'External SSD', 'Storage', 100.00, 1, 0.00, 10.00, 'PayPal', 'Completed', '2023-10-19', 'North', 'Loyal', 'Referral', 'USD'),
(46, '2023-11-02', 360.00, 101, 1006, 'Laptop Basic', 'Electronics', 350.00, 1, 0.00, 10.00, 'Debit Card', 'Completed', '2023-11-07', 'South', 'Loyal', 'Google', 'USD'),
(47, '2023-11-17', 180.00, 102, 1007, 'Wireless Mouse', 'Accessories', 25.00, 6, 0.00, 30.00, 'Credit Card', 'Completed', '2023-11-22', 'East', 'Loyal', 'Direct', 'USD'),
(48, '2023-12-05', 460.00, 103, 1008, 'USB Hub', 'Accessories', 20.00, 20, 0.00, 60.00, 'PayPal', 'Completed', '2023-12-10', 'West', 'Loyal', 'Social Media', 'USD'),
(49, '2023-12-20', 230.00, 104, 1009, 'Gaming Keyboard', 'Peripherals', 90.00, 2, 0.00, 50.00, 'Debit Card', 'Completed', '2023-12-25', 'North', 'Loyal', 'Ad Campaign', 'USD'),
(50, '2024-01-01', 140.00, 105, 1010, 'External SSD', 'Storage', 130.00, 1, 0.00, 10.00, 'Credit Card', 'Completed', '2024-01-06', 'South', 'Loyal', 'Referral', 'USD'),
(51, '2024-01-10', 220.00, 101, 1011, 'Laptop Basic', 'Electronics', 210.00, 1, 0.00, 10.00, 'PayPal', 'Completed', '2024-01-15', 'East', 'Loyal', 'Google', 'USD'),
(52, '2024-02-01', 90.00, 102, 1012, 'Wireless Mouse', 'Accessories', 20.00, 4, 0.00, 10.00, 'Debit Card', 'Completed', '2024-02-06', 'West', 'Loyal', 'Direct', 'USD'),
(53, '2024-02-15', 170.00, 103, 1013, 'USB Hub', 'Accessories', 25.00, 6, 0.00, 20.00, 'Credit Card', 'Completed', '2024-02-20', 'North', 'Loyal', 'Social Media', 'USD'),
(54, '2024-03-01', 320.00, 104, 1014, 'Gaming Keyboard', 'Peripherals', 100.00, 3, 0.00, 20.00, 'PayPal', 'Completed', '2024-03-06', 'South', 'Loyal', 'Ad Campaign', 'USD'),
(55, '2024-03-10', 110.00, 105, 1015, 'External SSD', 'Storage', 100.00, 1, 0.00, 10.00, 'Debit Card', 'Completed', '2024-03-15', 'East', 'Loyal', 'Referral', 'USD'),
(56, '2024-04-05', 180.00, 106, 1016, 'Smartwatch', 'Wearables', 170.00, 1, 0.00, 10.00, 'Credit Card', 'Completed', '2024-04-10', 'West', 'New', 'Google', 'USD'),
(57, '2024-04-18', 55.00, 107, 1017, 'Phone Case', 'Accessories', 10.00, 5, 0.00, 5.00, 'PayPal', 'Completed', '2024-04-23', 'North', 'New', 'Social Media', 'USD'),
(58, '2024-05-01', 420.00, 108, 1018, '4K Monitor', 'Displays', 400.00, 1, 0.00, 20.00, 'Debit Card', 'Completed', '2024-05-06', 'South', 'Loyal', 'Direct', 'USD'),
(59, '2024-05-12', 135.00, 109, 1019, 'Webcam', 'Peripherals', 40.00, 3, 0.00, 15.00, 'Credit Card', 'Completed', '2024-05-17', 'East', 'New', 'Ad Campaign', 'USD'),
(60, '2024-06-01', 250.00, 110, 1020, 'Noise Cancelling Headphones', 'Audio', 240.00, 1, 0.00, 10.00, 'PayPal', 'Completed', '2024-06-06', 'West', 'Loyal', 'Referral', 'USD'),
(61, '2024-06-15', 85.00, 107, 1016, 'Phone Case', 'Accessories', 10.00, 8, 0.00, 5.00, 'Debit Card', 'Completed', '2024-06-20', 'North', 'Loyal', 'Google', 'USD'),
(62, '2024-07-01', 310.00, 106, 1017, 'Smartwatch', 'Wearables', 150.00, 2, 0.00, 10.00, 'Credit Card', 'Completed', '2024-07-06', 'South', 'New', 'Social Media', 'USD'),
(63, '2024-07-20', 600.00, 108, 1018, '4K Monitor', 'Displays', 580.00, 1, 0.00, 20.00, 'PayPal', 'Completed', '2024-07-25', 'East', 'Loyal', 'Direct', 'USD'),
(64, '2024-08-01', 190.00, 109, 1019, 'Webcam', 'Peripherals', 45.00, 4, 0.00, 10.00, 'Debit Card', 'Completed', '2024-08-06', 'West', 'New', 'Ad Campaign', 'USD'),
(65, '2024-08-10', 300.00, 110, 1020, 'Noise Cancelling Headphones', 'Audio', 290.00, 1, 0.00, 10.00, 'Credit Card', 'Completed', '2024-08-15', 'North', 'Loyal', 'Referral', 'USD'),
(66, '2024-09-01', 110.00, 107, 1016, 'Phone Case', 'Accessories', 10.00, 10, 0.00, 10.00, 'PayPal', 'Completed', '2024-09-06', 'South', 'Loyal', 'Google', 'USD'),
(67, '2024-09-15', 200.00, 106, 1017, 'Smartwatch', 'Wearables', 190.00, 1, 0.00, 10.00, 'Debit Card', 'Completed', '2024-09-20', 'East', 'New', 'Social Media', 'USD'),
(68, '2024-10-01', 450.00, 108, 1018, '4K Monitor', 'Displays', 430.00, 1, 0.00, 20.00, 'Credit Card', 'Completed', '2024-10-06', 'West', 'Loyal', 'Direct', 'USD'),
(69, '2024-10-10', 160.00, 109, 1019, 'Webcam', 'Peripherals', 40.00, 4, 0.00, 0.00, 'PayPal', 'Completed', '2024-10-15', 'North', 'New', 'Ad Campaign', 'USD'),
(70, '2024-11-01', 270.00, 110, 1020, 'Noise Cancelling Headphones', 'Audio', 260.00, 1, 0.00, 10.00, 'Debit Card', 'Completed', '2024-11-06', 'South', 'Loyal', 'Referral', 'USD'),
(71, '2024-11-15', 120.00, 107, 1016, 'Phone Case', 'Accessories', 10.00, 10, 0.00, 20.00, 'Credit Card', 'Completed', '2024-11-20', 'East', 'Loyal', 'Google', 'USD'),
(72, '2024-12-01', 350.00, 106, 1017, 'Smartwatch', 'Wearables', 170.00, 2, 0.00, 10.00, 'PayPal', 'Completed', '2024-12-06', 'West', 'New', 'Social Media', 'USD'),
(73, '2024-12-10', 700.00, 108, 1018, '4K Monitor', 'Displays', 680.00, 1, 0.00, 20.00, 'Debit Card', 'Completed', '2024-12-15', 'North', 'Loyal', 'Direct', 'USD'),
(74, '2025-01-01', 210.00, 109, 1019, 'Webcam', 'Peripherals', 50.00, 4, 0.00, 10.00, 'Credit Card', 'Completed', '2025-01-06', 'South', 'New', 'Ad Campaign', 'USD'),
(75, '2025-01-15', 320.00, 110, 1020, 'Noise Cancelling Headphones', 'Audio', 310.00, 1, 0.00, 10.00, 'PayPal', 'Completed', '2025-01-20', 'East', 'Loyal', 'Referral', 'USD'),
(76, '2025-02-01', 150.00, 101, 1001, 'Laptop Pro', 'Electronics', 140.00, 1, 0.00, 10.00, 'Credit Card', 'Pending', '2025-02-06', 'North', 'VIP', 'Google', 'USD'),
(77, '2025-02-10', 80.00, 102, 1002, 'Gaming Mouse', 'Accessories', 30.00, 2, 0.00, 20.00, 'Debit Card', 'Completed', '2025-02-15', 'South', 'Loyal', 'Direct', 'USD'),
(78, '2025-03-01', 400.00, 103, 1003, 'Mechanical Keyboard', 'Peripherals', 100.00, 4, 0.00, 0.00, 'PayPal', 'Completed', '2025-03-06', 'West', 'New', 'Social Media', 'USD'),
(79, '2025-03-10', 95.00, 104, 1004, 'USB-C Adapter', 'Accessories', 20.00, 4, 5.00, 20.00, 'Credit Card', 'Completed', '2025-03-15', 'East', 'Loyal', 'Ad Campaign', 'USD'),
(80, '2025-03-20', 500.00, 105, 1005, 'High-End Graphics Card', 'Components', 480.00, 1, 0.00, 20.00, 'Bank Transfer', 'Shipped', '2025-03-25', 'North', 'VIP', 'Referral', 'USD');

Sales Trend Analysis Queries
Once the online_sales table is populated, you can run the following SQL queries to analyze various sales trends.

1. Monthly Revenue and Order Volume (Overall Trend)
This query provides a basic overview of monthly revenue and the number of unique orders across all years in the dataset, ordered chronologically.

SELECT
    EXTRACT(YEAR FROM order_date) AS sales_year,
    EXTRACT(MONTH FROM order_date) AS sales_month,
    SUM(amount) AS monthly_revenue,
    COUNT(DISTINCT order_id) AS monthly_order_volume
FROM
    online_sales
GROUP BY
    sales_year,
    sales_month
ORDER BY
    sales_year ASC,
    sales_month ASC;

2. Monthly Revenue and Order Volume for a Specific Year (e.g., 2023)
This query filters the results to show sales trends specifically for the year 2023. You can modify the WHERE clause to analyze any other year.

SELECT
    EXTRACT(YEAR FROM order_date) AS sales_year,
    EXTRACT(MONTH FROM order_date) AS sales_month,
    SUM(amount) AS monthly_revenue,
    COUNT(DISTINCT order_id) AS monthly_order_volume
FROM
    online_sales
WHERE
    EXTRACT(YEAR FROM order_date) = 2023
GROUP BY
    sales_year,
    sales_month
ORDER BY
    sales_year ASC,
    sales_month ASC;

3. Monthly Revenue and Order Volume for a Specific Product Category (e.g., 'Electronics')
This query focuses the analysis on sales trends within a particular product category, showing how specific product lines perform over time.

SELECT
    EXTRACT(YEAR FROM order_date) AS sales_year,
    EXTRACT(MONTH FROM order_date) AS sales_month,
    SUM(amount) AS monthly_revenue,
    COUNT(DISTINCT order_id) AS monthly_order_volume
FROM
    online_sales
WHERE
    category = 'Electronics'
GROUP BY
    sales_year,
    sales_month
ORDER BY
    sales_year ASC,
    sales_month ASC;

4. Quarterly Revenue and Order Volume
This query aggregates sales data by quarter, providing a broader view of trends throughout the year.

SELECT
    EXTRACT(YEAR FROM order_date) AS sales_year,
    EXTRACT(QUARTER FROM order_date) AS sales_quarter,
    SUM(amount) AS quarterly_revenue,
    COUNT(DISTINCT order_id) AS quarterly_order_volume
FROM
    online_sales
GROUP BY
    sales_year,
    sales_quarter
ORDER BY
    sales_year ASC,
    sales_quarter ASC;

5. Top 5 Months by Monthly Revenue
This query identifies the five months (across all years) that generated the highest total revenue, helping to highlight peak sales periods.

SELECT
    EXTRACT(YEAR FROM order_date) AS sales_year,
    EXTRACT(MONTH FROM order_date) AS sales_month,
    SUM(amount) AS monthly_revenue,
    COUNT(DISTINCT order_id) AS monthly_order_volume
FROM
    online_sales
GROUP BY
    sales_year,
    sales_month
ORDER BY
    monthly_revenue DESC
LIMIT 5;

Prerequisites
A database system compatible with standard SQL (e.g., PostgreSQL, MySQL, SQLite).

A SQL client or command-line interface to execute the queries.

Usage
Run the Database Setup and Data Population scripts: Execute the CREATE DATABASE, USE, CREATE TABLE, and INSERT INTO statements in your database environment. This will prepare your online_sales table.

Run the Analysis Queries: Once the table is set up and populated, you can execute any of the "Sales Trend Analysis Queries" to retrieve the desired insights.

Expected Output
Each analysis query will return a table with aggregated data, showing different perspectives on sales trends (e.g., monthly revenue, quarterly volume, top-performing months). The exact values will depend on the data inserted into your online_sales table.
