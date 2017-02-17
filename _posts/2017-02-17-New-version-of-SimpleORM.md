---
layout: post
title: New version of SimpleORM
date: 2017-02-17 10:28:00
disqus: y
---

Hi, 
I've been working on my ORM last days and I've reworked how results work.

First of all, **what's an ORM**?

An ORM is object-relational mapping, that is a programming technique for converting data between incompatible 
type systems in object-oriented programming languages, i.e SQL into PHP or Java. [Wikipedia](https://en.wikipedia.org/wiki/Object-relational_mapping)

My ORM is made in PHP and helps you to make queries to the database. Example:
```php
$result = MyModel::all()->execute();
```
is the same as you write
```php
$query = $connection->prepare("SELECT * FROM my_table");
$result = $query->execute();
```
As you can see, the ORM simplifies all queries and allows you to loop through results in a simple way using loop method:
```php
while($result->loop()) {
  $result->table_field;
}
```

This ORM has the basic functions: select, update, insert, delete, order by, limit, and simple where. I know there are 
lots of ORM's but this one acomplish all my needs and 

Feel free to clone or fork it!
[See SimpleORM](https://github.com/legomolina/simple-orm)
