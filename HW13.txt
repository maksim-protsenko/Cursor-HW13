CREATE DATABASE airport;
CREATE TABLE if not exists airplanes
(
    id_airplane     SERIAL PRIMARY KEY,
    serial_number   text not null,
    airplane_model  text not null,
    number_of_seats int  not null,
    crew_quantity   int
);
CREATE TABLE if not exists pilots
(
    id_pilot SERIAL PRIMARY KEY,
    name     text not null,
    surname  text not null,
    age      int  not null
);
CREATE TABLE if not exists qualification_of_pilots
(
    id       SERIAL PRIMARY KEY,
    pilot_id int,
    plane_id int,
    CONSTRAINT qualification_pilot_id_fk
        FOREIGN KEY (pilot_id) REFERENCES pilots (id_pilot),
    CONSTRAINT qualification_plane_id_fk
        FOREIGN KEY (plane_id) REFERENCES airplanes (id_airplane)
);
CREATE TABLE if not exists airports
(
    id_airport       SERIAL PRIMARY KEY,
    country          text,
    city             text,
    name             text,
    CONSTRAINT airports_pilot_id_fk
        FOREIGN KEY (id_airport) REFERENCES pilots (id_pilot),
    CONSTRAINT airports_planes_id_fk
        FOREIGN KEY (id_airport) REFERENCES airplanes (id_airplane)
);

INSERT INTO airplanes (serial_number, airplane_model, number_of_seats, crew_quantity)
VALUES ('UA180', 'Boeing 747', 467, 8),
       ('UA007', 'Airbus A320', 180, 5);

INSERT INTO pilots(name, surname, age)
VALUES ('Alex', 'Skorobogatko', 35),
       ('Vasyl', 'Gruska', 42),
       ('Panas', 'Kovalenko', 50),
       ('Oleg', 'Yama', 48),
       ('Ulyana', 'Vpravna', 32);

INSERT INTO qualification_of_pilots (pilot_id, plane_id)
VALUES (1, 2),
       (1, 1),
       (2, 2),
       (3, 2),
       (4, 1),
       (5, 1),
       (5, 2);
INSERT INTO airports (country, city, name)
VALUES ('Ukraine', 'Kharkiv')