-- 1️⃣ Create Manger table
CREATE TABLE Manger (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    birth_date DATE,
    address VARCHAR(255)
);

-- 2️⃣ Drop address column
ALTER TABLE Manger
DROP COLUMN address;

-- 3️⃣ Add city_address and street columns
ALTER TABLE Manger
ADD COLUMN city_address VARCHAR(100),
ADD COLUMN street VARCHAR(100);

-- 4️⃣ Rename name column to full_name
ALTER TABLE Manger
RENAME COLUMN name TO full_name;  -- MySQL 8+, PostgreSQL
-- Oracle: ALTER TABLE Manger RENAME COLUMN name TO full_name;

-- 5️⃣ Make table read-only
-- Option 1: revoke write permissions
-- MySQL example
-- REVOKE INSERT, UPDATE, DELETE ON Manger FROM 'some_user'@'host';
-- PostgreSQL example
-- REVOKE INSERT, UPDATE, DELETE ON Manger FROM some_role;

-- Option 2: create read-only view
CREATE VIEW Manger_Read AS
SELECT * FROM Manger;

-- 6️⃣ Create Owner table with subset of columns
CREATE TABLE Owner AS
SELECT id, full_name AS name, birth_date
FROM Manger
WHERE 1=0;  -- structure only, no data

-- 7️⃣ Rename Manger table to Master
ALTER TABLE Manger
RENAME TO Master;

-- 8️⃣ Drop all tables
DROP TABLE IF EXISTS Master;
DROP TABLE IF EXISTS Owner;
DROP VIEW IF EXISTS Manger_Read;
