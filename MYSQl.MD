РАБОТА MYSQL SERVER С ФАЙЛАМИ
=============================

### ЗАГРУЗКА ДАННЫХ ТАБЛИЦЫ ИЗ ФАЙЛА НА КОМПЬЮТЕРЕ

1. Входим на сервер
2. Изменяем значение переменной `local_infile=1`:

		set global local_infile=1;

3. Выходим из сервера
4. Заходим на сервер с помощью локальной системной переменной:

		mysql --local-infile=1 -u<user> -p<password> <database>;

5. Загружаем базу данных из .txt файла: 

		load data local infile '<path_to_file>' into table <table_name>;


### ВЫГРУЗКА ДАННЫХ ТАБЛИЦЫ В ФАЙЛ

**Перед тем как выполнять действия по извлечению данных из таблицы, необходимо
выбрать соответствующую базу данных.**

В результате выполнения следующей команды будет создан текстовый файл в том виде,
в котором его можно загрузить в таблицу БД:

	SELECT * FROM <table_name> INTO OUTFILE '<full_path_to_output_file>';

Так же можно изменить формат выгружаемого файла для лучшей совместимости, например:

	SELECT * FROM <table_name> INTO OUTFILE '<full_path_to_output_file>'
		FIELDS TERMINATED BY ',' ENCLOSED BY '"'
		LINES TERMINATED BY '\r\n';


### ВЫГРУЗКА МОДЕЛИ ТАБЛИЦЫ

В данном случае произойдёт импорт *модели таблицы из базы данных*, иными словами `.sql` скрипт
для создания таблицы данной структуры.

	mysqldump -u<user> -p<password> --tab="<full_path_to_directory>" <database> <table>

Где `<full_path_to_directory>` - путь до папки, в которую сохранится файл скрипта.
Имя файлу(ам) даётся автоматически.


### ЗАГРУЗКА ТАБЛИЦЫ В БАЗУ ДАННЫХ ИЗ ФАЙЛА SQL

	mysql -u<login> -p<password> <database_name> < "<full_path_to_file>"



ОБРАЩЕНИЕ К СИСТЕМНЫМ ПЕРЕМЕННЫМ
================================

- Просмотр значения: `select @@global.<global_variable>;`
- Установка значения: `set @@global.<global_variable>=<value>;`


# USERS #
login: 		emb
password: 	367as
role: 		db admin


mysqldump -uroot -proot --no-create-info --tab="C:\ProgramData\MySQL\MySQL Server 8.0\Uploads" schedule schedule