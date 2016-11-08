WpRecord
========

WpRecord is a simple implementation of the [active record pattern](https://en.wikipedia.org/wiki/Active_record_pattern), specifically created for a WordPress environment.

## What is active record?

The active record pattern is a design pattern. It is used to bridge the concepts of [object oriented programming](https://en.wikipedia.org/wiki/Object-oriented_programming) and [relational database management systems](https://en.wikipedia.org/wiki/Relational_database_management_system). When using the active record pattern, we can think of each row in a database table as representing an instance of an object. The class of the object corresponds to the table of the database. The columns in the database corresponds to the fields of the object.

## An example

For example, we might have a database table representing persons. The table would have the columns `id`, `firstName` and `lastName`. Let's look at the code to fetch and display the information about a particular person, with and without WpRecord. For the example, let's use the person with `id=5`.

Using the `$wpdb` object in WordPress, our code might look something like this:

```php
$person=$wpdb->get_row($wpdb->prepare("SELECT * FROM persons WHERE id=%s",5),ARRAY_A);
echo $person["firstName"]." ".$person["lastName"];
```

Using WpRecord, the code would instead be:

```php
$person=Person::findOne(5);
echo $person->firstName." ".$person->lastName;
```

Say that we instead would like to fetch all persons with the surname "Lee". Using the `$wpdb` object, the code would be:

```php
$persons=$wpdb->get_result($wpdb->prepare("SELECT * FROM persons WHERE lastName=%s","Lee"),ARRAY_A);
```

Using WpRecord, the code would be:

```php
$persons=Person::findAllBy("lastName","Lee");
```

SQL is a powerful language used to extract information from a database. However, in a real world database application, many of the queries are quite simple. They are often of the type in the example, such as "find an object with a particular value for the primary key", or "find all objects with a specific value for a given column". In these situations, having the SQL statements in the middle doesn't really serve a real purpose, and it might make the code cluttered and difficult to read. Here, using an active record implementation will make the code smaller and cleaner.


