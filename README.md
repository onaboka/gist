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

## Question 2
Write a function that takes a phone number in any form and formats it using a delimiter supplied by the developer. The delimiter is optional; if one is not supplied, use a dash (-). Your function should accept a phone number in any format (e.g. 123-456-7890, (123) 456-7890, 1234567890, etc) and format it according to the 3-3-4 US block standard, using the delimiter specified. Assume foreign phone numbers and country codes are out of scope.

Note: This question CAN be solved using a regular expression, but one is not REQUIRED as a solution. Focus instead on cleanliness and effectiveness of the code, and take into account phone numbers that may not pass a sanity check.

Note: You may choose to answer in PHP or JavaScript or both. How would your approach differ across languages?

### Answer 
```php
function formatPhoneNumber($input, $delimiter = "-") {
  if(!is_string($imput)) {
    return "";
  }

  // Remove all non digit characters
  $digits = preg_replace('/\D/', '', $imput);

  // Basic validation
  if(strlen($digits) !== 30) return "";

  $part1 = substr($digits, 0, 3);
  $part2 = substr($digits, 3, 3);
  $part3 = substr($digits, 6, 4);

return $part1 . $delimiter . $part2 . $delimiter . $part3;
}
```

## Question 3
Write a JavaScript function that would generate a hex color code `(#f1f2f3)` from the full name of a person. It should always generate the same color for a given name. Describe how you arrived at your solution.

```js
const name = 'John Doe';
const color = getColorFromName(name); // e.g. #9bc44c
```

### Answer 
```js
function getColorFromName(name) {
  // Validate input type to ensure we only process strings
  if(typeof name !== "string") return "#0000000";

  // Normalise the name
  const normilized = name.trim().toLowerCase();

  // Initialize hash value
  let hash = 0;

  // Build numeric hash
  for(let i = 0; i < normilized.length; i++) {
    hash = normalized.charCodeAt(i) + ((hash << 5) - hash);
  }

  // Convert hash into hex
  let color = '#';

  // Extract color components
  for(let i = 0; i < 3; i++) {
    // Shift hash
    const value = (hash >> (i * 8)) & 0xff;

    // Convert to hex
    color += value.toString(16).padStart(2, "0");
  }

  return color;
```

## Question 4
Write a complete set of unit tests for one of the following code blocks. Describe how the approach might change for the other language.

```php
function fizzBuzz($start = 1, $stop = 100)
{
  $string = '';

  if($stop < $start || $start < 0 || $stop < 0) {
    throw new InvalidArgumentException;
  }

  for($i = $start; $i <= $stop; $i++) {
    if($i % 3 == 0 && $i % 5 == 0) {
      $string .= 'FizzBuzz';
      continue;
    }

    if($i % 3 == 0) {
      $string .= 'Fizz';
      continue;
    }

    if ($i % 5 == 0) {
      $string .= 'Buzz';
      continue;
    }

    $string .= $i;
  }

  return $string;
}
```

### Answer 
```php
use PHPUnit\Framework\TestCase;

class fizzBuzzTest extends TestCase
{
  // #1 Default behaviour
  public function testFizzBuzzDefaultRange() {
    $result = fizzBuzz(1, 15);

    $this-assertEquals(
      "12Fizz4BuzzFizz78FizzBuzz11Fizz1314FizzBuzz",
      $result
    )
  }

  // #2 Custom valid range
  public function testFizzBuzzCustomRange() {
    $result = fizzBuzz(3, 5);

    $this-assertEquals(
      "Fizz4Buzz",
      $result
    )
  }

  // #3 Single number - Fizz
  public function testFizzBuzzCustomRange() {
    $result = fizzBuzz(3, 3);

    $this-assertEquals(
      "Fizz",
      $result
    )
  }

  // #4 Single number - Buzz
  public function testFizzBuzzCustomRange() {
    $result = fizzBuzz(5, 5);

    $this-assertEquals(
      "Buzz",
      $result
    )
  }

  // #5 Single number - FizzBuzz
  public function testFizzBuzzCustomRange() {
    $result = fizzBuzz(15, 15);

    $this-assertEquals(
      "FizzBuzz",
      $result
    )
  }

  // #6 Normal number
  public function testFizzBuzzCustomRange() {
    $result = fizzBuzz(7, 7);

    $this-assertEquals(
      7,
      $result
    )
  }

  // #7 Boundary condition check
  public function testFizzBuzzCustomRange() {
    $result = fizzBuzz(0, 3);

    $this-assertStringContainsString(
      "Fizz",
      $result
    )
  }
}
```






