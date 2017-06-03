# ChitChat

This is the simple forum application written with Go for the book "Go Web Programming" from Manning Publication Co. The source code for this application is the basis for the Chapter 2 - Go ChitChat. 

However the code is a reference and is not a 1 - 1 match with the code in the book. There are portions of the code that is more detailed in here than in Chapter 2 (which is a simplified version of the source code here).

Some differences include:

* This version of ChitChat is configurable with a `config.json` file
* This version is able to log to a `chitchat.log` file
* There are test files in this code
* All structs are fully fleshed out (in the book chapter, they are only implied)
* Some of the functions are placed as methods for the struct types instead of being a part of the package

SQL：
create table users (
  id         serial primary key,
  uuid       varchar(64) not null unique,
  name       varchar(255),
  email      varchar(255) not null unique,
  password   varchar(255) not null,
  created_at timestamp not null
);
create table sessions (
  id         serial primary key,
  uuid       varchar(64) not null unique,
  email      varchar(255),
  user_id    integer references users(id),
  created_at timestamp not null
);
create table threads (
  id         serial primary key,
  uuid       varchar(64) not null unique,
  topic      text,
  user_id    integer references users(id),
  created_at timestamp not null
);

create table posts (
  id         serial primary key,
  uuid       varchar(64) not null unique,
  body       text,
  user_id    integer references users(id),
  thread_id  integer references threads(id),
  created_at timestamp not null
);

