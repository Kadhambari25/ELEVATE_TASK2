# ELEVATE_TASK2
# Car Rental Database Project

This repository contains the SQL scripts to create and manage a Car Rental Database.  

## Tables
- **CUSTOMER**: Stores customer details.
  CREATE TABLE CUSTOMER (
    Cust_ID INT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Phone VARCHAR(15) NOT NULL,
    Email VARCHAR(100),
    Address VARCHAR(255)
- **CAR**: Stores car details.
CREATE TABLE CAR (
    Vehicle_ID INT PRIMARY KEY,
    Model VARCHAR(100) NOT NULL,
    Year INT,
    Type VARCHAR(50),
    DailyRate DECIMAL(8,2),
    WeeklyRate DECIMAL(8,2),
    Availability VARCHAR(20) DEFAULT 'Yes',
    IsAvailable BOOLEAN DEFAULT TRUE

);
- **RENTALS**: Records car rentals.
CREATE TABLE RENTALS (
    Rental_No INT PRIMARY KEY,
    Cust_ID INT,
    Vehicle_ID INT,
    Rental_Type VARCHAR(10),
    Start_Date DATE,
    Return_Date DATE,
    Total_Days INT,
    Amount_Due DECIMAL(8,2),
    Status VARCHAR(20) DEFAULT 'Active',
    FOREIGN KEY (Cust_ID) REFERENCES CUSTOMER(Cust_ID),
    FOREIGN KEY (Vehicle_ID) REFERENCES CAR(Vehicle_ID)
);
- **PAYMENT**: Stores payment details.
CREATE TABLE PAYMENT (
    Payment_ID INT PRIMARY KEY,
    Rental_No INT,
    Payment_Date DATE,
    Amount_Paid DECIMAL(8,2),
    Payment_Method VARCHAR(20),
    FOREIGN KEY (Rental_No) REFERENCES RENTALS(Rental_No)

);
# Handle missing values using `NULL` or `DEFAULT` 'UPDATE' 'DELETE'
-- handling missing values using NULL or DEFAULT
-- Phone column cannot be NULL, so we used DEFAULT '0000000000'

ALTER TABLE CUSTOMER
MODIFY Phone VARCHAR(15) NOT NULL DEFAULT '0000000000';

-- Email and Address allow NULL, so you can insert NULL where missing
INSERT INTO CUSTOMER (Cust_ID, Name, Phone, Email, Address) VALUES
(11, 'Ramesh', '0000000000', NULL, NULL);

-- Use UPDATE and DELETE with WHERE conditions
-- Update a customer's phone number
UPDATE CUSTOMER
SET Phone = '9998887776'
WHERE Cust_ID = 2;
-- Mark a rental as completed
UPDATE RENTALS
SET Status = 'Completed'
WHERE Rental_No = 1;
-- Change availability of a car
UPDATE CAR
SET IsAvailable = FALSE, Availability = 'No'
WHERE Vehicle_ID = 1;

DELETE FROM PAYMENT
WHERE Rental_No = 3;

## Features
1. Insert rows using `INSERT INTO`.
2. Handle missing values using `NULL` or `DEFAULT`.
3. Update and delete rows using `UPDATE` and `DELETE`.

## Screenshots
### Table Creation
<img width="1916" height="1015" alt="image" src="https://github.com/user-attachments/assets/2dabe713-0641-4b47-b8d4-7d5bc2fccf15" />
<img width="1919" height="698" alt="image" src="https://github.com/user-attachments/assets/0cc3f45d-48e4-47dc-aacd-6bb2d2755940" />



### Inserting Data
<img width="851" height="511" alt="image" src="https://github.com/user-attachments/assets/bfb9957c-1f0e-494e-8329-bfa407549844" />


### Updating and Deleting
<img width="812" height="494" alt="image" src="https://github.com/user-attachments/assets/342b9a29-c6e3-4b72-88ad-8f58c6b1a78d" />

