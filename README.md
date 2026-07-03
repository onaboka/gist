# gist
Solutions including PHP and JavaScript exercises with explanations and code samples

## Question 1
During a large data migration, you get the following error: Fatal error: Allowed memory size of 134217728 bytes exhausted (tried to allocate 54 bytes). You've traced the problem to the following snippet of code:

```php
$stmt = $pdo->prepare('SELECT * FROM largeTable');
$stmt->execute();
$results = $stmt->fetchAll(PDO::FETCH_ASSOC);
foreach ($results as $result) {
  // manipulate the data here
}
```

### Answer 
The memory eror happens because `fetchAll()` loads the entire result set into memory at once. For a large table, this quickly exhausts PHP's memory limit. 

```php
$stmt = $pdo->prepare('SELECT * FROM largeTable');
$stmt->execute();

while($result = $stmt->fetch(PDO::FETCH_ASSOC)) { ... }
```

I propose this fix, because:
- fetchAll() -> loads everything into memory
- fetch() -> one row at a time

