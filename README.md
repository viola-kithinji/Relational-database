- SQL Project: Building a Relational Database Management System

DROP TABLE IF EXISTS users;
DROP TABLE IF EXISTS groups;
DROP TABLE IF EXISTS rooms;

CREATE TABLE users (
    user_id int PRIMARY KEY,
    user_name varchar(20) NOT NULL,
    group_id int NULL
);

INSERT INTO users (user_id, user_name, group_id) VALUES (1, 'Modesto', 1);
INSERT INTO users (user_id, user_name, group_id) VALUES (2, 'Ayine', 1);
INSERT INTO users (user_id, user_name, group_id) VALUES (3, 'Christopher', 2);
INSERT INTO users (user_id, user_name, group_id) VALUES (4, 'Cheong Woo', 2);
INSERT INTO users (user_id, user_name, group_id) VALUES (5, 'Saulat', 3);
INSERT INTO users (user_id, user_name, group_id) VALUES (6, 'Heidy', NULL);

CREATE TABLE groups (
    group_id int PRIMARY KEY,
    group_name varchar(20) NOT NULL
);

INSERT INTO groups (group_id, group_name) VALUES (1, 'I.T');
INSERT INTO groups (group_id, group_name) VALUES (2, 'Sales');
INSERT INTO groups (group_id, group_name) VALUES (3, 'Administration');
INSERT INTO groups (group_id, group_name) VALUES (4, 'Operations');

CREATE TABLE rooms (
    room_id int PRIMARY KEY,
    room_name varchar(20
