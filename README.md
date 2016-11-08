WpRecord
========

WpRecord is a simple [active record](https://en.wikipedia.org/wiki/Active_record_pattern) implementation, specifically created for a WordPress environment.

## What is active record?

The active record pattern is a design pattern. It is used to bridge the concepts of object oriented programming (OOP) and relational database management systems (RDBMS). When using the active record pattern, we can think of each row in a database table as representing an instance of an object. The class of the object corresponds to the table of the database. The columns in the database corresponds to the fields of the object.

For example, we might have a database table representing persons. The table would have the columns `id`, `firstName` and `lastName`. Let's look at the code to fetch and display the information about a particular person, with and without WpRecord. For the example, let's use the person with `id=5`.

The code in PHP, using the `$wpdb` object in WordPress, might look something like this:

```php
$person=$wpdb->get_row($wpdb->prepare("SELECT * FROM persons WHERE id=%s",5),ARRAY_A);
echo $person["firstName"]." ".$person["lastName"];
```

Using WpRecord, the code would instead be:

```php
$person=Person::findOne(5);
echo $person->firstName." ".$person->lastName;
```

