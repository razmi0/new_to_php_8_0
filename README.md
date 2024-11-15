# New in php 8.0

## 1. Named Arguments

```php
function namedArguments($name, $age, $city) {
    echo "Name: $name, Age: $age, City: $city";
}

namedArguments(age: 25, name: 'John', city: 'New York');
```

## 2. Nullsafe Operator

```php
class User {
    public function getCity() {
        return 'New York';
    }
}

$user = new User();

echo $user?->getCity()?->name;
```

## 3. Constructor Property Promotion

```php
class User {
    public function __construct(
        public string $name,
        public int $age,
        public string $city
    ) {}
}

$user = new User(name: 'John', age: 25, city: 'New York');
```

## 4. Match Expression

```php
$day = 'Monday';

switch ($day) {
    case 'Monday':
        echo 'First day of the week';
        break;
    case 'Tuesday':
        echo 'Second day of the week';
        break;
    default:
        echo 'Another day of the week';
}

// Using match expression instead of switch
echo match($day) {
    'Monday' => 'First day of the week',
    'Tuesday' => 'Second day of the week',
    default => 'Another day of the week'
};
```

## 5. Attributes

```php

// Add functionnal metadata to your code



// Declare an attribute that can be used on classes
// Declare an attribute class Route that defines a path and methods
#[Attribute(Attribute::TARGET_CLASS)]
class Route
{
    public function __construct(
        public string $path,
        public array $methods
    ) {
        print_r([
            "path" => $path,
            "methods" => $methods,
        ]);
    }
}



// Use the Route attribute on a class Controller
#[Route(path: "/hello", methods: ["GET"])]
class Controller {}



// Instantiate a new reflection object for the Controller class
$controllerReflector = new ReflectionClass(Controller::class);


// Get the Route attribute from the Controller class
$routeAttributes = $controllerReflector->getAttributes("Route");

// From routeAttributes, get the first element(Route attribute) and instantiate it
// The constructor of the Route attribute will be called and the path and methods will be printed
$routeInstance = $routeAttributes[0]->newInstance();

// You can directly access the arguments of the Route attribute and do whatever you want with them
$routePath = $routeAttributes[0]->getArguments()["path"];
$routeMethods = $routeAttributes[0]->getArguments()["methods"];


```

## 6. Union Types ( but not generics yet :disappointed:)

```php

// Union types allow you to accept multiple types for a parameter or return type

function foo(int|string $value): int|string {
    return $value;
}

echo foo(5); // 5
```

## 7. New String Functions

```php

// str_contains
echo str_contains('Hello World', 'World'); // true

// str_starts_with
echo str_starts_with('Hello World', 'Hello'); // true

// str_ends_with
echo str_ends_with('Hello World', 'World'); // true

```

## 8. New Array Functions

```php

// array_key_first
$array = ['a' => 1, 'b' => 2, 'c' => 3];
echo array_key_first($array); // a

// array_key_last
echo array_key_last($array); // c

// array_is_list
// a list is an array that has integer keys starting from 0 and increasing by 1
$array = ['a' => 1, 'b' => 2, 'c' => 3];
echo array_is_list($array); // false

$array = [1, 2, 3];
echo array_is_list($array); // true

```

## 9. New Null Coalescing Assignment Operator

```php

// Null coalescing assignment operator assigns the value of its right-hand operand to its left-hand operand only if the left-hand operand is null

$city = null;
$city ??= 'New York';
echo $city; // New York

```

## 10. New Throw Expression

```php

// Throw expression allows you to throw exceptions in an expression context

$age = 17;
$age >= 18 ?: throw new Exception('You must be 18 years or older to enter this site');

```

## 11. New Weak Maps

```php

// Weak maps allow creating a map from objects to arbitrary values without preventing the objects from being garbage collected

$map = new WeakMap();
$obj = new stdClass();
$map[$obj] = 'value';

```

## 12. New Just In Time Compilation

```php

// PHP 8.0 introduces a new JIT compiler that can improve the performance of PHP code

```

## 13. New Trailing Comma Syntax

```php

// Trailing commas are now allowed in function calls, closures, and in the argument list of function definitions

function foo(
    int $a,
    int $b,
) {}

```

## 14. New Token As Object

```php

// PHP 8.0 introduces a new token_get_all() function that returns an object for each token
// A token is an object with the following properties:
// - id: The token ID
// - line: The line in which the token occurs
// - text: The text of the token


$tokens = token_get_all('<?php echo "Hello World";');

foreach ($tokens as $token) {
    if (is_array($token)) {
        echo token_name($token[0]) . PHP_EOL;
    } else {
        echo $token . PHP_EOL;
    }
}

```

## 15. New Saner Numeric Strings

```php

// PHP 8.0 introduces a new behavior for numeric strings
// Numeric strings are now interpreted as numbers in arithmetic operations

echo '10' + '10'; // 20

```
