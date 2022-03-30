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
    room_name varchar(20) NOT NULL
);

INSERT INTO rooms (room_id, room_name) VALUES (1, '101');
INSERT INTO rooms (room_id, room_name) VALUES (2, '102');
INSERT INTO rooms (room_id, room_name) VALUES (3, 'Auditorium A');
INSERT INTO rooms (room_id, room_name) VALUES (4, 'Auditorium B');

CREATE TABLE group_rooms (
    group_id int NOT NULL REFERENCES groups(group_id),
    room_id int NOT NULL REFERENCES rooms(room_id),
    CONSTRAINT pk_group_rooms PRIMARY KEY (group_id, room_id)
);

INSERT INTO group_rooms (group_id, room_id) VALUES (1, 1);
INSERT INTO group_rooms (group_id, room_id) VALUES (1, 2);
INSERT INTO group_rooms (group_id, room_id) VALUES (2, 2);
INSERT INTO group_rooms (group_id, room_id) VALUES (2, 3);

-- All groups, and the users in each group. A group should appear even if there are no users assigned to the group.
SELECT g.group_name AS group, u.user_name AS user
	FROM groups g
		LEFT JOIN users u
		ON g.group_id = u.group_id
ORDER BY group, user;

-- All rooms, and the groups assigned to each room. The rooms should appear even if no groups have been assigned to them.
SELECT r.room_name AS room, g.group_name AS group
	FROM rooms r
		LEFT JOIN group_rooms gr
		ON r.room_id = gr.room_id
			LEFT JOIN groups g
			ON gr.group_id = g.group_id
ORDER BY room, group;

-- A list of users, the groups that they belong to, and the rooms to which they are assigned. This should be sorted alphabetically by user, then by group, then by room.
SELECT u.user_name AS user, g.group_name AS 'group', r.room_name AS room
	FROM users u
		LEFT JOIN groups g
        	ON u.group_id = g.group_id
			LEFT JOIN group_rooms gr
            		ON g.group_id = gr.group_id
				LEFT JOIN rooms r
                		ON gr.room_id = r.room_id
