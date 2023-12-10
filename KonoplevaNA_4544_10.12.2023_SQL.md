## Работа с MySQL

- ### В ранее подключенном MySQL создать базу данных с названием "Human Friends".

      CREATE DATABASE Друзья_человека;

- ### Создать таблицы, соответствующие иерархии из вашей диаграммы классов.

      CREATE TABLE Родительский_класс (
        id INT PRIMARY KEY AUTO_INCREMENT,
        тип VARCHAR(50)
      );

      CREATE TABLE Домашние*животные (
        id INT PRIMARY KEY,
        вид VARCHAR(50),
        FOREIGN KEY (id) REFERENCES Родительский*класс(id)
      );

      CREATE TABLE Собаки (
        id INT PRIMARY KEY,
        имя VARCHAR(50),
        команда VARCHAR(50),
        дата*рождения DATE,
        FOREIGN KEY (id) REFERENCES Домашние*животные(id)
      );

      CREATE TABLE Кошки (
        id INT PRIMARY KEY,
        имя VARCHAR(50),
        команда VARCHAR(50),
        дата*рождения DATE,
        FOREIGN KEY (id) REFERENCES Домашние*животные(id)
      );

      CREATE TABLE Хомяки (
        id INT PRIMARY KEY,
        имя VARCHAR(50),
        команда VARCHAR(50),
        дата*рождения DATE,
        FOREIGN KEY (id) REFERENCES Домашние*животные(id)
      );

      CREATE TABLE Вьючные*животные (
        id INT PRIMARY KEY,
        вид VARCHAR(50),
        FOREIGN KEY (id) REFERENCES Родительский*класс(id)
      );
      
      CREATE TABLE Лошади (
        id INT PRIMARY KEY,
        имя VARCHAR(50),
        команда VARCHAR(50),
        дата*рождения DATE,
        FOREIGN KEY (id) REFERENCES Вьючные*животные(id)
      );
      
      CREATE TABLE Верблюды (
        id INT PRIMARY KEY,
        имя VARCHAR(50),
        команда VARCHAR(50),
        дата*рождения DATE,
        FOREIGN KEY (id) REFERENCES Вьючные*животные(id)
      );
      
      CREATE TABLE Ослы (
        id INT PRIMARY KEY,
        имя VARCHAR(50),
        команда VARCHAR(50),
        дата*рождения DATE,
        FOREIGN KEY (id) REFERENCES Вьючные*животные(id)
      );
      
      show databases;
      show tables;

- ### Заполнить таблицы данными о животных, их командах и датами рождения.

      INSERT INTO Верблюды ( имя, команда, дата_рождения)
      VALUES ('Шоколад', 'Ноo', '2021-11-01'),
             ('Рыжий', 'На месте' '2020-11-12'),
             ('Стрела', 'Ждать' '2022-09-05');
      
      INSERT INTO Кошки ( имя, команда, дата_рождения)
      VALUES ('Пуаро', 'Кис-кис', '2022-11-20'),
             ('Вася', 'Кушать', '2023-03-08');
      
      INSERT INTO Лошади ( имя, команда, дата_рождения)
      VALUES ('Спирит', 'Но', '2021-01-21'),
             ('Чернила', 'Стоп', '2022-03-08');
      
      INSERT INTO Ослы ( имя, команда, дата_рождения)
      VALUES ('Петя', 'Пошёл', '2018-01-21'),
             ('Дылда', 'Стой', '2020-03-08');
      
      INSERT INTO Собаки ( имя, команда, дата_рождения)
      VALUES ('Тоша', 'Дай лапу', '2018-01-25'),
             ('Бимка', 'Лежать', '2023-03-20');
      
      INSERT INTO Хомяки ( имя, команда, дата_рождения)
      VALUES ('Свин', 'Кушать', '2022-02-27'),
             ('Хома', 'Играть', '2023-10-18');

- ### Удалить записи о верблюдах и объединить таблицы лошадей и ослов.

      TRUNCATE TABLE Верблюды;
      
      CREATE TABLE Парнокопытные AS
      SELECT _ FROM Лошади
      UNION
      SELECT _ FROM Ослы;

- ### Создать новую таблицу для животных в возрасте от 1 до 3 лет и вычислить их возраст с точностью до месяца.

      CREATE TABLE Парнокопытные AS
      SELECT \*, TIMESTAMPDIFF(MONTH, дата*рождения, CURDATE()) AS возраст*в*месяцах
      FROM (
          SELECT 'Собаки' AS тип*животного, имя, команда, дата*рождения FROM Собаки
          UNION ALL
          SELECT 'Кошки' AS тип*животного, имя, команда, дата*рождения FROM Кошки
          UNION ALL
          SELECT 'Хомяки' AS тип*животного, имя, команда, дата*рождения FROM Хомяки
          UNION ALL
          SELECT 'Лошади' AS тип*животного, имя, команда, дата*рождения FROM Лошади
          UNION ALL
          SELECT 'Ослы' AS тип*животного, имя, команда, дата*рождения FROM Ослы
      ) AS животные
      WHERE дата*рождения >= DATE*SUB(CURDATE(), INTERVAL 3 YEAR)
      AND дата*рождения <= DATE_SUB(CURDATE(), INTERVAL 1 YEAR);

- ### Объединить все созданные таблицы в одну, сохраняя информацию о принадлежности к исходным таблицам.

      CREATE TABLE Полный*состав AS
      SELECT 'Собаки' AS тип*животного, имя, команда, дата*рождения FROM Собаки
      UNION ALL
      SELECT 'Кошки' AS тип*животного, имя, команда, дата*рождения FROM Кошки
      UNION ALL
      SELECT 'Хомяки' AS тип*животного, имя, команда, дата*рождения FROM Хомяки
      UNION ALL
      SELECT 'Лошади' AS тип*животного, имя, команда, дата*рождения FROM Лошади
      UNION ALL
      SELECT 'Ослы' AS тип*животного, имя, команда, дата_рождения FROM Ослы;
