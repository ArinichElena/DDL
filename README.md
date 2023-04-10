# DDL
#### Создать БД:
> CREATE DATABASE test_clinic;
<image src="https://github.com/ArinichElena/DDL/blob/main/СоздатьБД.png">

#### Создать папку, для табличного пространства:
> mkdir /home/admin/pg_ext_data
<image src="https://github.com/ArinichElena/DDL/blob/main/Создать%20папку%20(1).png">
<image src="https://github.com/ArinichElena/DDL/blob/main/Создать%20папку%20(2).png">

#### Поменять пользователя для папки:
> chown postgres:postgres /home/admin/pg_ext_data
<image src="https://github.com/ArinichElena/DDL/blob/main/Поменять%20пользователя%20для%20папки.png"> 

#### Создать табличное пространство:
> CREATE TABLESPACE ext_tabspace LOCATION '/home/admin/pg_ext_data';
<image src="https://github.com/ArinichElena/DDL/blob/main/Создать%20ТП%20(1).png"> 
<image src="https://github.com/ArinichElena/DDL/blob/main/Создать%20ТП%20(2).png">
<image src="https://github.com/ArinichElena/DDL/blob/main/Создать%20ТП%20(3).png">
  
#### Создать схему:
> CREATE SCHEMA test_clinic;
<image src="https://github.com/ArinichElena/DDL/blob/main/Создать%20схему.png">
<image src="https://github.com/ArinichElena/DDL/blob/main/Посмотреть%20схемы.png">
  
#### Создать роль:
> CREATE ROLE student CREATEDB;
<image src="https://github.com/ArinichElena/DDL/blob/main/Создать%20роли.png">
  
#### Создать роль в группе:
> CREATE ROLE alex IN ROLE student LOGIN PASSWORD '1234';
<image src="https://github.com/ArinichElena/DDL/blob/main/Создать%20роль%20в%20группе.png">
  
#### Создать таблицы:
<image src="https://github.com/ArinichElena/DDL/blob/main/Талицы%20по%20схемам.png">

---
* __Скрипты для справочников__
```sql
create table patient (
	id BIGSERIAL primary key,
	surname VARCHAR(100) not null,
	name VARCHAR(100) not null,
	patronymic VARCHAR(100),
	birthday DATE,
	medical_policy BIGINT UNIQUE,
	gender VARCHAR(32)
) tablespace ext_tabspace; 

create table clinic (
id SERIAL primary key,
name TEXT not null,
short_name TEXT not null,
address TEXT not null,
type_clinic_id INT not null references type_clinic
) tablespace ext_tabspace;

create table type_clinic (
id SERIAL primary key,
name VARCHAR(32) not null
) tablespace ext_tabspace;

create table laboratory (
id SERIAL primary key,
name TEXT not null,
short_name TEXT not null,
address TEXT not null,
clinic_id INT not null references directory_clinic.clinic
) tablespace ext_tabspace;
```

