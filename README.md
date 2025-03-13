# MySQL-2nd-Year-Practice-Questionss
-- Database creation
CREATE DATABASE bookstore_management;
USE bookstore_management;

-- Create Authors table
CREATE TABLE authors (
    author_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    birth_date DATE,
    nationality VARCHAR(50),
    biography TEXT,
    email VARCHAR(100)
);

-- Create Books table
CREATE TABLE books (
    book_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(100) NOT NULL,
    author_id INT,
    genre VARCHAR(50),
    publication_date DATE,
    isbn VARCHAR(20) UNIQUE,
    price DECIMAL(6,2),
    stock_quantity INT DEFAULT 0,
    publisher VARCHAR(100),
    page_count INT,
    FOREIGN KEY (author_id) REFERENCES authors(author_id) ON DELETE SET NULL
);

-- Create Customers table
CREATE TABLE customers (
    customer_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    phone VARCHAR(15),
    address VARCHAR(255),
    city VARCHAR(50),
    state VARCHAR(2),
    zip_code VARCHAR(10),
    registration_date DATE,
    loyalty_points INT DEFAULT 0
);

-- Create Sales table
CREATE TABLE sales (
    sale_id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT,
    sale_date DATE,
    total_amount DECIMAL(8,2),
    payment_method VARCHAR(20),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id) ON DELETE SET NULL
);

-- Create Sale_Items table (junction table for sales and books)
CREATE TABLE sale_items (
    sale_id INT,
    book_id INT,
    quantity INT,
    price_per_unit DECIMAL(6,2),
    PRIMARY KEY (sale_id, book_id),
    FOREIGN KEY (sale_id) REFERENCES sales(sale_id) ON DELETE CASCADE,
    FOREIGN KEY (book_id) REFERENCES books(book_id) ON DELETE CASCADE
);

-- Insert data into Authors table
INSERT INTO authors (first_name, last_name, birth_date, nationality, biography, email) VALUES
('J.K.', 'Rowling', '1965-07-31', 'British', 'Author of Harry Potter series', 'jkrowling@example.com'),
('Stephen', 'King', '1947-09-21', 'American', 'Master of horror fiction', 'sking@example.com'),
('Jane', 'Austen', '1775-12-16', 'British', 'Classic English literature author', 'jausten@example.com'),
('George', 'Orwell', '1903-06-25', 'British', 'Author of 1984 and Animal Farm', 'gorwell@example.com'),
('Agatha', 'Christie', '1890-09-15', 'British', 'Queen of mystery novels', 'achristie@example.com'),
('Ernest', 'Hemingway', '1899-07-21', 'American', 'Nobel Prize winner and modernist', 'ehemingway@example.com'),
('Toni', 'Morrison', '1931-02-18', 'American', 'Nobel Prize winner and novelist', 'tmorrison@example.com'),
('Gabriel', 'García Márquez', '1927-03-06', 'Colombian', 'Magic realism pioneer', 'gmarquez@example.com');

-- Insert data into Books table
INSERT INTO books (title, author_id, genre, publication_date, isbn, price, stock_quantity, publisher, page_count) VALUES
('Harry Potter and the Philosopher''s Stone', 1, 'Fantasy', '1997-06-26', '978-0747532743', 19.99, 45, 'Bloomsbury', 320),
('The Shining', 2, 'Horror', '1977-01-28', '978-0385121675', 15.99, 28, 'Doubleday', 447),
('Pride and Prejudice', 3, 'Classic', '1813-01-28', '978-1503290563', 12.99, 35, 'T. Egerton', 432),
('1984', 4, 'Dystopian', '1949-06-08', '978-0451524935', 14.99, 42, 'Secker & Warburg', 328),
('Murder on the Orient Express', 5, 'Mystery', '1934-01-01', '978-0062693662', 11.99, 30, 'Collins Crime Club', 256),
('The Old Man and the Sea', 6, 'Literary Fiction', '1952-09-01', '978-0684801223', 13.99, 25, 'Charles Scribner''s Sons', 128),
('Beloved', 7, 'Historical Fiction', '1987-09-13', '978-1400033416', 16.99, 20, 'Alfred A. Knopf', 324),
('One Hundred Years of Solitude', 8, 'Magical Realism', '1967-05-30', '978-0060883287', 18.99, 22, 'Harper & Row', 417),
('It', 2, 'Horror', '1986-09-15', '978-0670813025', 17.99, 33, 'Viking Press', 1138),
('Animal Farm', 4, 'Political Satire', '1945-08-17', '978-0452284241', 10.99, 38, 'Secker & Warburg', 112),
('Sense and Sensibility', 3, 'Classic', '1811-10-30', '978-1503292864', 12.99, 27, 'Thomas Egerton', 384),
('Death on the Nile', 5, 'Mystery', '1937-11-01', '978-0062073556', 11.99, 29, 'Collins Crime Club', 288);

-- Insert data into Customers table
INSERT INTO customers (first_name, last_name, email, phone, address, city, state, zip_code, registration_date, loyalty_points) VALUES
('Michael', 'Johnson', 'mjohnson@example.com', '555-123-4567', '123 Main St', 'New York', 'NY', '10001', '2022-01-15', 150),
('Emily', 'Davis', 'edavis@example.com', '555-234-5678', '456 Elm St', 'Boston', 'MA', '02108', '2022-02-20', 85),
('Robert', 'Wilson', 'rwilson@example.com', '555-345-6789', '789 Oak Ave', 'Chicago', 'IL', '60601', '2022-03-10', 210),
('Sophia', 'Martinez', 'smartinez@example.com', '555-456-7890', '101 Pine Rd', 'Los Angeles', 'CA', '90001', '2022-03-25', 120),
('William', 'Anderson', 'wanderson@example.com', '555-567-8901', '202 Maple Dr', 'Seattle', 'WA', '98101', '2022-04-05', 95),
('Olivia', 'Taylor', 'otaylor@example.com', '555-678-9012', '303 Cedar Ln', 'Denver', 'CO', '80201', '2022-04-20', 75),
('James', 'Thomas', 'jthomas@example.com', '555-789-0123', '404 Birch Ct', 'Austin', 'TX', '73301', '2022-05-10', 180),
('Emma', 'Jackson', 'ejackson@example.com', '555-890-1234', '505 Walnut St', 'Miami', 'FL', '33101', '2022-05-25', 65);

-- Insert data into Sales table
INSERT INTO sales (customer_id, sale_date, total_amount, payment_method) VALUES
(1, '2023-01-15', 59.97, 'Credit Card'),
(2, '2023-01-20', 12.99, 'PayPal'),
(3, '2023-02-05', 33.98, 'Credit Card'),
(1, '2023-02-10', 14.99, 'Debit Card'),
(4, '2023-02-15', 48.97, 'Credit Card'),
(5, '2023-03-01', 19.99, 'PayPal'),
(6, '2023-03-10', 27.98, 'Debit Card'),
(7, '2023-03-15', 36.98, 'Credit Card'),
(8, '2023-03-20', 18.99, 'PayPal'),
(2, '2023-04-01', 29.98, 'Credit Card'),
(3, '2023-04-15', 42.97, 'Debit Card'),
(4, '2023-04-20', 11.99, 'Credit Card');

-- Insert data into Sale_Items table
INSERT INTO sale_items (sale_id, book_id, quantity, price_per_unit) VALUES
(1, 1, 2, 19.99),
(1, 4, 1, 14.99),
(2, 3, 1, 12.99),
(3, 5, 1, 11.99),
(3, 7, 1, 16.99),
(4, 4, 1, 14.99),
(5, 1, 1, 19.99),
(5, 6, 1, 13.99),
(5, 10, 1, 10.99),
(6, 1, 1, 19.99),
(7, 8, 1, 18.99),
(7, 9, 0.5, 17.99),
(8, 2, 1, 15.99),
(8, 7, 1, 16.99),
(9, 8, 1, 18.99),
(10, 5, 1, 11.99),
(10, 10, 1, 10.99),
(11, 1, 1, 19.99),
(11, 6, 1, 13.99),
(11, 9, 0.5, 17.99),
(12, 5, 1, 11.99);
(9, 8, 1, 18.99),
(10, 5, 1, 11.99),
(10, 10, 1, 10.99),
(11, 1, 1, 19.99),
(11, 6, 1, 13.99),
(11, 9, 0.5, 17.99),
(12, 5, 1, 11.99);

-- Question List

-- Question 1: 
-- Write a query to display the title, price, and stock quantity of all books.

-- Question 2: 
-- Write a query to find all books written by "Stephen King".

-- Question 3: 
-- Write a query to count how many books are in each genre.

-- Question 4: 
-- Write a query to find the top 3 most expensive books.

-- Question 5: 
-- Write a query to calculate the total amount spent by each customer.

-- Question 6:
-- Write a query to find all books with stock quantity less than 25.

-- Question 7:
-- Write a query to list all books sold in March 2023.

-- Question 8: 
-- Write a query to count sales by payment method.

-- Question 9: 
-- Write a query to list all authors from Britain.

-- Question 10: 
-- Write a query to find all books that have never been sold.

**Note: You have to create and add a file and code the answers of the questions mentioned above in it.
**
