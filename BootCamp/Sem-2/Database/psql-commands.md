# PSQL - Commands

`create database song_something;` - create databse
`\c song_something` - takes you into the database
`\l` - shows all databse files
`\d` - Lists all tables in the database

```
CREATE TABLE genres (id serial primary key, name varchar(100));
```
^^ Creates table called genres and adds an id column that automatically counts up and a name column which takes characters up to 100.
`INSERT INTO genres (name) VALUES ('hiphop');` - add those fields to a new item in the database
`SELECT id, name FROM genres;` - Search and find id and name in the genres table
`SELECT * FROM genres;` - Returns all items in the genres table
```sql
INSERT INTO genres (name) VALUES
('EDM'), ('classic rock'), ('classical');
```
^^ Create multiple entries at one time
`SELECT * FROM genres WHERE name = 'hip hop';` - Allows you to search specific items using specific search params
`SELECT * FROM genres WHERE is = 2 or id = 3;` - The above using or
`SELECT * FROM genres WHERE name LIKE 'classic%';` - Find similar items using the word classic
`UPDATE genres SET name = 'hip hop/rap' WHERE name = 'hip%hop';` - Look for entry with name of `hiphop` and change it to `hip hop/rap`!!! DO NOT FORGET WHERE OR IT WILL CHANGE EVERYTHING!!
`DELETE FROM genres WHERE name = 'classical';` - delete the entry with the name classical
`CREATE TABLE songs (id SERIAL PRIMARY KEY, name VARCHAR(255), genre_id SERIAL REFERENCES genres(id));` - Use foreign key to create an item in a table.
`\d` look at all the database names
`INSERT INTO songs (name, genre_id) VALUES ('Up', 3);` - Create a song with the name up and the genre of classic rock
