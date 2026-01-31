Null parameter passing for array PHP values.
=> Check with `is_array()` function and ternary operators.
```php
$lookupRefBracketedStringEnArr = (is_array($modified_bracketedString_en)) ? explode(',', $modified_bracketedString_en): array();
```

Null parameter passing for PHP strings.
=> Check with `if` clause.
```php
if($someVar != null){
	//proceed
}
```

