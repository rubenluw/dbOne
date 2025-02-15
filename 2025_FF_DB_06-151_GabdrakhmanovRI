## Отчет по практике базы данных

### Выполнил: Габдрахманов Расиль 06-151

<!-- <br/><br/><br/><br/><br/><br/> -->



Описание базы данных: база данных представляет собой данные пользователей и их сообщения для небольшого мессенджера. Состоит из 4 таблиц - в двух из них информация о пользователях и их настройках платформы, в двух других информация о сообщениях.

Краткое описание таблиц:

- 1\) *Users (id\_user, login, password)* - информация о логине, пароле и id пользователя
- 2\) *Users\_information (id\_user, name, surname, age, color\_scheme)* - информация о имени, фамилии, возрасте, цветовой схеме интерфейса
- 3\) *Messages (id\_message, id\_sender, id\_recipient, date\_message, time\_message)* - информация о сообщениях, id сообщения, от кого, кому, дата сообщения и время
- 4\) *Data\_messages (id\_data, id\_message, text\_message, voice\_message, photo\_message, file\_message)* - данные о сообщениях, хранит идентификатор сообщения, к которому принадлежат данные, текст сообщения, путь до голосового файла сообщения, путь до фото, путь до файла

Схема базы данных,таблицы приведены к 3 нормальной форме:
![13.png](images/13.png)

### 1) Таблица Users:
#### Users (id\_user, login, password) - информация о логине, пароле и id пользователя

id\_user - идентификатор пользователя, первичный ключ<br/>
login - логин пользователя,символьное меньше 50, уникальное, длина больше 3, not null<br/>
password - хэш пароля(sha256) пользователя, символьное меньше 100, длина больше 0, not null<br/>

### 2) Таблица Users\_information:
#### Users\_information (id\_user, name, surname, age, color\_scheme) - информация о имени, фамилии, возрасте, цветовой схеме интерфейса

id\_user - идентификатор пользователя, первичный ключ, внешний ключ к таблице Users стобцу id\_user
name - имя пользователя,символьное меньше 50, длина больше 0, not null<br/>
surname - фамилия пользователя,символьное меньше 50, значение по умолчанию 'none', not null<br/>
age - возраст пользователя,целое число, значение по умолчанию 0, not null<br/>
color\_scheme - цветовая схема интерфейса пользователя,символьное меньше 10, значение по умолчанию 'light', not null<br/>

### 3) Таблица Messages:
#### Messages (id\_message, id\_sender, id\_recipient, date\_message, time\_message) - информация о сообщениях, id сообщения, от кого, кому, дата сообщения и время

id\_message - идентификатор сообщения, первичный ключ<br/>
id\_sender - идентификатор отправителя, целое, внешний ключ к таблице Users стобцу id\_user<br/>
id\_recipient - идентификатор получателя, целое, внешний ключ к таблице Users стобцу id\_user<br/>
data\_message - дата сообщения,тип дата, not null<br/>
time\_message - время сообщения,тип время, not null<br/>

### 4) Таблица Data\_messages:
#### Data\_messages (id\_data, id\_message, text\_message, voice\_message, photo\_message, file\_message) - данные о сообщениях, хранит идентификатор сообщения, к которому принадлежат данные, текст сообщения, путь до голосового файла сообщения, путь до фото, путь до файла

id\_data - идентификатор пакета данных, первичный ключ<br/>
id\_message - идентификатор сообщения, целое, внешний ключ к таблице Messages стобцу id\_message<br/>
text\_message - текст сообщения, текстовое, значение по умолчанию 'none', not null<br/>
voice\_message - путь до голосового сообщения, текстовое, значение по умолчанию 'none', not null<br/>
photo\_message - путь до фото, текстовое, значение по умолчанию 'none', not null<br/>
file\_message - путь до файла, текстовое, значение по умолчанию 'none', not null<br/>


### 1) Таблица Users:
![1.png](images/1.png)

### 2) Таблица Users\_information:
![2.png](images/2.png)

### 3) Таблица Messages:
![3.png](images/3.png)

### 4) Таблица Data\_messages:
![4.png](images/4.png)


## Задание 1.

1\.1\. Создадим необходимые таблицы:

>Для выбранной БД создать необходимые таблицы, используя соответствующие команды.
Должны быть заданы все ограничения на таблицы с использованием ключей, типов и других
ограничений (автоинкрементное, уникальное, обязательное целое, символьное и т.п.).

- Таблица Users:
```sql
create table users(
  id_user serial,
  login varchar(50) not null,
  password varchar(100) not null,
  
  primary key(id_user),
  unique(login),
  check(char_length(login)>=3),
  check(char_length(password)>0)
);
```
- Таблица Users\_information:
```sql
create table users_information(
  id_user serial,
  name varchar(50) not null,
  surname varchar(50) not null default 'none',
  age integer not null default 0,
  color_scheme varchar(10) not null default 'light',

  primary key(id_user),
  foreign key (id_user) references users(id_user),
  check(char_length(name)>0)
);
```
- Таблица Messages:
```sql
create table messages(
  id_message serial,
  id_sender integer,
  id_recipient integer,
  date_message date not null,
  time_message time not null,

  primary key(id_message),
  foreign key (id_sender) references users(id_user),
  foreign key (id_recipient) references users(id_user)
);
```
- Таблица Data\_messages:
```sql
create table data_messages(
  id_data serial,
  id_message integer,
  text_message text not null default 'none',
  voice_message text not null default 'none',
  photo_message text not null default 'none',
  file_message text not null default 'none',

  primary key(id_data),
  foreign key(id_message) references messages(id_message)
);
```

- Результат создания таблицы Users:<br/>
![5.png](images/5.png)

- Результат создания таблицы Users\_information:<br/>
![6.png](images/6.png)

- Результат создания таблицы Messages:<br/>
![7.png](images/7.png)

- Результат создания таблицы Data\_messages:<br/>
![8.png](images/8.png)


1\.2\. Команды изменения и удаления:

>Для каждой команды создания таблицы или ограничения должны быть приведены команды
изменения или удаления.

- Добавить столбец в таблицу:
```sql
alter table users
  add password_second varchar(100);
```

- Добавить ограничение столбца:
```sql
alter table users
  alter column password_second set not null;
```

- Удалить ограничение столбца:
```sql
alter table users
  alter column password_second drop not null;
```

- Добавить ограничения таблицы:
```sql
alter table users
  add constraint check_password_second check(char_length(password_second)>0);
```

- Удалить ограничения таблицы:
```sql
alter table users
  drop constraint check_password_second;
```

- Удалить столбец из таблицы:
```sql
alter table users
  drop column password_second;
```

## Задание 2.

2\.1\. Заполним таблицы данными:

>Наполнить созданные таблицы данными. Таблица с PK должна иметь не менее 5 записей.
В соответствующих таблицах с FK, которые имеются связь с таблицей PK, должны иметь от
4 записей с FK, ссылающимися на 1 запись PK “главной” таблицы.​
Т.е. в основной таблице 5+ записей с PK, а в каждой подчиненной таблице через связи
PK-FK 5*4 = 20+ записей. Если таблиц более 4х, то количество таких подчиненных через
PK-FK записей можно сократить до 5*3 = 15 для каждой из FK-таблиц. Допускается
пропускать некоторые пары PK-FK в случае отсутствия реальных данных.

- Таблица Users:
```sql
insert into users (login,password) values 
  ('mike',digest('qwerty','sha256')),
  ('bob',digest('lapmmm','sha256')),
  ('rayan',digest('rettlop','sha256')),
  ('andrew',digest('nbi86Unn??@wq','sha256')),
  ('lera',digest('dfkNemcpwKKKKewwe','sha256'));
```

- Таблица Users\_information:
```sql
insert into users_information (name,surname,age,color_scheme) values
  ('mike','jonson',20,'light'),
  ('bob','lampada',22,'dark'),
  ('rayan','milson',19,'dark'),
  ('adrew','sanclidiav',20,'light'),
  ('lera','olaeva',21,'dark');
```

- Таблица Messages:
```sql
insert into messages(id_sender,id_recipient,date_message,time_message) values
  (1,2,'2025-01-10','10:10:05'),
  (1,3,'2025-01-10','04:34:01'),
  (1,4,'2025-01-11','13:17:45'),
  (1,5,'2025-02-11','23:11:59'),
  (2,1,'2025-01-11','10:10:05'),
  (2,3,'2025-01-12','12:13:05'),
  (2,4,'2025-01-10','15:05:23'),
  (2,5,'2025-01-12','01:01:35'),
  (3,1,'2025-01-16','08:43:34'),
  (3,2,'2025-01-22','23:12:06'),
  (3,4,'2025-01-23','12:13:09'),
  (3,5,'2025-01-25','14:18:13'),
  (4,1,'2025-01-25','09:33:54'),
  (4,2,'2025-02-04','03:53:43'),
  (4,3,'2025-01-06','07:04:23'),
  (4,5,'2025-01-10','17:08:11'),
  (5,1,'2025-01-12','19:32:32'),
  (5,2,'2025-01-12','11:43:39'),
  (5,3,'2025-01-13','14:23:28'),
  (5,4,'2025-03-24','07:55:37');
```

- Таблица Data\_messages:
```sql
insert into data_messages (id_message,text_message,voice_message,photo_message,file_message) values
  (1,'hello bob',default,'mike/2/1.jpg',default),
  (1,default,default,'mike/2/2.jpg',default),
  (1,default,default,'mike/2/3.jpg',default),
  (1,default,default,'mike/2/4.jpg',default),
  (2,'hello rayan',default,'mike/3/1.jpg',default),
  (2,default,default,'mike/3/2.jpg',default),
  (2,default,default,'mike/3/3.jpg',default),
  (2,default,default,'mike/3/4.jpg',default),
  (3,'hello adrew',default,'mike/4/1.jpg',default),
  (3,default,default,'mike/4/2.jpg',default),
  (3,default,default,'mike/4/3.jpg',default),
  (3,default,default,'mike/4/4.jpg',default),
  (4,'hello lera',default,default,'mike/5/1.zip'),
  (4,default,default,default,'mike/5/2.zip'),
  (4,default,default,default,'mike/5/3.zip'),
  (4,default,default,default,'mike/5/4.zip'),
  (5,'mike, thank you',default,'bob/1/1.jpg',default),
  (5,default,default,'bob/1/2.jpg',default),
  (5,default,default,'bob/1/3.jpg',default),
  (5,default,default,'bob/1/4.jpg',default),
  (6,'hello rayan',default,default,default),
  (7,default,'bob/4/1.mp4',default,default),
  (8,'hello lera,how are you?',default,default,default),
  (9,'hello mike,from rayan',default,default,default),
  (10,'hello bob',default,default,default),
  (11,'hello adrew',default,default,default),
  (12,'hello lera',default,default,default),
  (13,'hello mike, from adrew',default,default,default),
  (14,'hello bob, from adrew',default,default,default),
  (15,'hello rayan, from adrew',default,default,default),
  (16,'hello lera, from adrew',default,default,default),
  (17,'hello mike, from lera',default,default,default),
  (18,'hello bob, from lera',default,default,default),
  (19,'hello rayan, from lera',default,default,default),
  (20,'hello adrew, from lera',default,default,default);
```

Результат заполнения таблиц можно увидеть в начале отчета

2\.2\. Команды изменения и удаления:

>Для каждой команды создания записи должны быть приведены команды изменения или
удаления.

- Добавить запись в таблицу:
```sql
insert into users (login,password) values 
  ('mike_second',digest('qwerty_second','sha256'));
```

- Изменить запись в таблице:
```sql
update users
  set login='mike_third'
where id_user=1;
```

- Удалить запись из таблицы:
```sql
delete from users
where id_user=1;
```


## Задание 3.

3\.1\. Напишем запрос для вывода из таблицы Users\_information имени и возраста, тех людей кому 20 лет:

>Написать sql-запрос для поиска данных в таблице с фильтром по любому числовому
параметру.

```sql
select name, age 
from users_information
where age=20;
```

Выполнение запроса:<br/>
![9.png](images/9.png)

3\.2\. Напишем запрос для вывода из таблицы Data\_messages текстовых сообщений, которые отправлял пользователь mike:

>Написать sql-запрос для вывода значений основной таблицы, удовлетворяющие фильтру по
какой-либо из характеристик подчиненной таблицы.

```sql
select text_message
from data_messages
where (
  (select login 
  from users
  where id_user=
    (select id_sender
    from messages
    where messages.id_message=data_messages.id_message)
  )='mike'
  and (text_message!='none')
);
```

Выполнение запроса:<br/>
![10.png](images/10.png)


3\.3\. Напишем запрос для вывода из таблицы Users логинов пользователей, кто отправлял сообщения 11 января 2025 года:

>Написать sql-запрос для вывода отличающихся полей (выбрать одно из полей) у записей,
имеющих идентичные поля (выбрать одно из полей) в любой из подчиненных таблиц.

```sql
select login
from users
where '2025-01-11' IN (
  select date_message
  from messages
  where id_sender=users.id_user
);
```

Выполнение запроса:<br/>
![11.png](images/11.png)


3\.4\. Напишем запрос для вывода из таблицы Users логинов пользователей, кто отправлял сообщения утро - с 8 утра до 10 и при этом пользовался темной темой, то есть узнаем тех пользователей, у кого темная тема включена всегда, не только ночью:

>Написать sql-запрос для поиска данных в основной таблице, имеющих числовой фильтр в
двух подчиненных таблицах.


```sql
select login
from users
where(
  (
    (
    select count(time_message)
    from messages
    where (id_sender=users.id_user) and (time_message between '08:00:00' and '10:00:00') 
    )>0
  )
  and
  (
    (
    select color_scheme
    from users_information
    where users_information.id_user=users.id_user
    )='dark'
  )

);
```

Выполнение запроса:<br/>
![12.png](images/12.png)


## Задание 4.

4\.1\. Напишем запрос для создания представления основной таблицы и одной подчиненной:

>Написать sql-запрос для создания представления, содержащего данные из основной
таблицы (несколько полей) и одной из подчиненных таблиц (несколько полей).

```sql
create view view_one as
  select login,name,surname
  from users,users_information
  where users.id_user=users_information.id_user;
```

Выполнение представления:<br/>
![14.png](images/14.png)

4\.2\. Напишем запрос для создания представления основной таблицы и нескольких подчиненных:

>Написать sql-запрос для создания представления, содержащего данные из основной
таблицы (несколько полей) и некоторых данных из всех подчиненных таблиц (можно 1-2
поля).

```sql
create view view_two as
  select login,name,surname,text_message,date_message,time_message
  from users,users_information,messages,data_messages
  where
    users_information.id_user=users.id_user
    and messages.id_sender=users.id_user
    and data_messages.id_message=messages.id_message
    and data_messages.text_message!='none'
  ;
```

Выполнение представления:<br/>
![15.png](images/15.png)