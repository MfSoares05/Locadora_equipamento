-- Updated SQL script for MySQL Workbench
CREATE DATABASE IF NOT EXISTS locadora_equipamentos;
USE locadora_equipamentos;

-- Table for users (unchanged)
CREATE TABLE IF NOT EXISTS users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL
);

-- Table for equipments with stock
CREATE TABLE IF NOT EXISTS equipments (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE,
    stock INT NOT NULL DEFAULT 0 -- Total available stock
);

-- Insert initial equipments with stock
INSERT INTO equipments (name, stock) VALUES 
('Betoneira', 10),
('Andaime', 15),
('Compactador', 8),
('Escora', 20);

-- Table for clients (unchanged)
CREATE TABLE IF NOT EXISTS clients (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    cpf VARCHAR(14) NOT NULL UNIQUE,
    address TEXT NOT NULL
);

-- Table for rentals with status
CREATE TABLE IF NOT EXISTS rentals (
    id INT AUTO_INCREMENT PRIMARY KEY,
    client_id INT NOT NULL,
    equipment_id INT NOT NULL,
    quantity INT NOT NULL,
    value DECIMAL(10, 2) NOT NULL,
    start_date DATE NOT NULL,
    end_date DATE NOT NULL,
    status ENUM('active', 'completed') DEFAULT 'active', -- Track rental status
    FOREIGN KEY (client_id) REFERENCES clients(id),
    FOREIGN KEY (equipment_id) REFERENCES equipments(id)
);
