# Dbms
Quiz management system
Create database 
CREATE DATABASE IF NOT EXISTS quiz_management; 
USE quiz_management; 
-- Users Table 
CREATE TABLE IF NOT EXISTS users ( id INT 
AUTO_INCREMENT PRIMARY KEY, username 
VARCHAR(255) NOT NULL UNIQUE, password 
VARCHAR(255) NOT NULL, 
 role ENUM('admin', 'user') DEFAULT 'user', -- Defines roles for users (Admin or regular 
user) 
 created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP 
); 
-- Quizzes Table 
CREATE TABLE IF NOT EXISTS quizzes ( id 
INT AUTO_INCREMENT PRIMARY KEY, 
title VARCHAR(255) NOT NULL, subject 
VARCHAR(255) NOT NULL, created_by INT 
NOT NULL, 
 created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, 
 FOREIGN KEY (created_by) REFERENCES users(id) ON DELETE CASCADE --
Admin or creator of the quiz 
);
-- Questions Table 
CREATE TABLE IF NOT EXISTS questions ( id 
INT AUTO_INCREMENT PRIMARY KEY, 
 quiz_id INT, question_text TEXT 
NOT NULL, option_1 VARCHAR(255) 
NOT NULL, option_2 VARCHAR(255) 
NOT NULL, option_3 VARCHAR(255) 
NOT NULL, option_4 VARCHAR(255) 
NOT NULL, 
 correct_option INT NOT NULL, -- 1, 2, 3, or 4 based on the correct answer 
 FOREIGN KEY (quiz_id) REFERENCES quizzes(id) ON DELETE CASCADE 
); 
-- Answers Table (optional, for recording individual answers if needed) 
CREATE TABLE IF NOT EXISTS answers ( id INT 
AUTO_INCREMENT PRIMARY KEY, user_id INT, question_id 
INT, selected_option INT, 
 FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE, 
 FOREIGN KEY (question_id) REFERENCES questions(id) ON DELETE CASCADE 
); 
-- Results Table 
CREATE TABLE IF NOT EXISTS results ( id 
INT AUTO_INCREMENT PRIMARY KEY, 
user_id INT, quiz_id INT, score INT, 
 completed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, 
 FOREIGN KEY (user_id) REFERENCES users(id), 
 FOREIGN KEY (quiz_id) REFERENCES quizzes(id) 
);
Sample data for users (Admin and regular users) 
INSERT INTO users (username, password, role) VALUES