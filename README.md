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
