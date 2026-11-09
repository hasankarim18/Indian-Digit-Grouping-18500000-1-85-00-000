# Indian-Digit-Grouping-18500000-1-85-00-000

function format_number_indian( $number ) {
	$number = (int) round( (float) $number );
	$digits = (string) abs( $number );

	if ( strlen( $digits ) > 3 ) {
		$last3  = substr( $digits, -3 );
		$rest   = substr( $digits, 0, -3 );
		$rest   = preg_replace( '/\B(?=(\d{2})+(?!\d))/', ',', $rest );
		$digits = $rest . ',' . $last3;
	}

	return ( $number < 0 ? '-' : '' ) . $digits;
}


Here is a comprehensive description of the `pd_format_number_indian( $number )` function and how it works step-by-step.

### Overview

This custom PHP function takes a numerical input and formats it according to the **Indian numbering system** (e.g., converting `1234567` into `12,34,567`). Unlike the Western numbering system which groups digits in thousands (every 3 digits), the Indian system groups digits in thousands for the last three digits, and then in pairs of two digits thereafter.

---

### Step-by-Step Code Breakdown

1. **Rounding and Integer Conversion**
```php
$number = (int) round( (float) $number );

```


* Converts the input into a float, rounds it to the nearest whole number, and casts it into an integer. This strips out any decimal points (e.g., paise).


2. **Absolute Value and String Conversion**
```php
$digits = (string) abs( $number );

```


* Takes the absolute value (`abs`) to remove any negative sign temporarily so string manipulation can happen cleanly, then converts the number into a string (`(string)`).


3. **Length Check & Splitting**
```php
if ( strlen( $digits ) > 3 ) {
    $last3  = substr( $digits, -3 );
    $rest   = substr( $digits, 0, -3 );

```


* If the number has 4 or more digits, it splits the string into two parts:
* **`$last3`**: The final 3 digits on the right.
* **`$rest`**: Everything *before* the last 3 digits.




4. **Applying Indian Comma Grouping**
```php
$rest   = preg_replace( '/\B(?=(\d{2})+(?!\d))/', ',', $rest );
$digits = $rest . ',' . $last3;

```


* Uses a regular expression (`preg_replace`) to insert commas into the `$rest` portion every two digits from right to left.
* It then joins the formatted `$rest`, a comma, and the `$last3` digits back together.


5. **Handling Negative Numbers**
```php
return ( $number < 0 ? '-' : '' ) . $digits;

```


* Checks if the original number was negative. If it was, it prepends a minus sign (`-`) to the final formatted string; otherwise, it returns it as-is.