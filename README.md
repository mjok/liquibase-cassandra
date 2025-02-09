liquibase-cassandra[![Build and Test Extention](https://github.com/liquibase/liquibase-cassandra/actions/workflows/build.yml/badge.svg)](https://github.com/liquibase/liquibase-cassandra/actions/workflows/build.yml)
===================

Liquibase extension for Cassandra Support.


### Setup local test environment with Liquibase Test Harness

start cassandra

`docker run -p 9042:9042 --rm --name cassandra3 -d cassandra:3`

`docker run -p 9043:9042 --rm --name cassandra4 -d cassandra:4.0`

NOTE: Cassandra 4.0-rc1 is not behaving on Windows 10, Docker Desktop 3.3.3. Have run successfully on Centos 8.

get ip

`docker inspect cassandra3`

`docker inspect cassandra4.0`
 
start another instance for cqlsh, check for IP address, replace mentioned IP with the one inspect command shows. Repeat for other Cassandra instance(s).

`docker run -it --rm cassandra bash`

`> cqlsh 172.17.0.2`

execute the following CQL (from test.cql):

```
CREATE KEYSPACE betterbotz
  WITH REPLICATION = { 
   'class' : 'SimpleStrategy', 
   'replication_factor' : 1 
  };
USE betterbotz;
DROP TABLE IF EXISTS authors;
CREATE TABLE authors (
                         id int,
                         first_name varchar,
                         last_name varchar,
                         email varchar,
                         birthdate date,
                         added timestamp,
                         PRIMARY KEY (id)
);

INSERT INTO authors(id, first_name, last_name, email, birthdate, added) VALUES
(1,'Courtney','Hodkiewicz','borer.edison@example.org','1986-01-22','1983-08-23 14:55:09');
INSERT INTO authors(id, first_name, last_name, email, birthdate, added) VALUES
(2,'Marielle','Kuhlman','llakin@example.org','1995-08-08','1984-03-05 01:25:02');
INSERT INTO authors(id, first_name, last_name, email, birthdate, added) VALUES
(3,'Emmanuel','Gleichner','jean.zemlak@example.net','1997-05-09','1977-08-09 10:28:04');
INSERT INTO authors(id, first_name, last_name, email, birthdate, added) VALUES
(4,'Hertha','Goodwin','hollis.gusikowski@example.org','2014-08-21','2009-01-28 11:02:56');
INSERT INTO authors(id, first_name, last_name, email, birthdate, added) VALUES
(5,'Ewald','Sauer','juvenal35@example.com','1988-10-10','2000-11-02 00:37:53');


DROP TABLE IF EXISTS posts;
CREATE TABLE posts (
                       id int,
                       author_id int,
                       title varchar,
                       description varchar,
                       content text,
                       inserted_date date,
                       PRIMARY KEY (id)
);

INSERT INTO posts(id, author_id, title, description, content, inserted_date) VALUES
(1,1,'sit','in','At corporis est sint beatae beatae.','1996-05-04');
INSERT INTO posts(id, author_id, title, description, content, inserted_date) VALUES
(2,2,'nisi','et','Sunt nemo magni et tenetur debitis blanditiis.','2000-05-25');
INSERT INTO posts(id, author_id, title, description, content, inserted_date) VALUES
(3,3,'ratione','blanditiis','Ipsa distinctio doloremque et ut.','1997-09-22');
INSERT INTO posts(id, author_id, title, description, content, inserted_date) VALUES
(4,4,'ad','et','Repudiandae porro explicabo officiis sed quis voluptate et.','1978-12-13');
INSERT INTO posts(id, author_id, title, description, content, inserted_date) VALUES
(5,5,'deserunt','temporibus','Mollitia reiciendis debitis est voluptatem est neque.','1979-12-06');
```
