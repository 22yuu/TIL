MySql에서 고유한 아이디 값을 생성하는 방법

```SQL
// TABLE SCHEMA
CREATE TABLE User
(
	Id char(38) PRIMARY KEY,
	Username varchar (50) unique not null,
	Password varchar (100) not null,
	Name varchar (50) not null,
	LastName varchar (50) not null,
	Email varchar(100) unique not null
);

---
// Insert
INSERT INTO User VALUES (UUID(), 'admin', 'admin', 'GilDong', 'Hong', 'hgildong@gmail.com');

```

![UUID](./imgs/UUID_Result.png)
