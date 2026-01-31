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


## Login issues on setup

Issues on logging in during initial setup primarily is caused by Laravel API authentication failure.

For old symcom version:
```
Debug:
1. The login.php page on folder root.
2. The api/login.php page. Print out the response and exit the script to avoid navigation to different script.
3. The unauthenticated-main-call.php script for URL issues during CURL requests.
4. The controller scripts on "root\symcom\api\app\Http\Controllers\V1". On exceptions, echo out the exception message.
5. Check the ".env" of the laravel application in "root\symcom\api". Verify credentials including base url and absolute url.
6. Check the "constants.php" inside "root\symcom\api\config" for any static value error.
7. Check route.php in "root\config". Check credentials including base url and absolute url.
```

For new symcom version:
```
Debug:
1. Check docker credentials, base url and abosolute urls on ".env" in project root.
2. Check apache config in "docker\apache" for routing issues.
3. Check config.php in "symcom-core-app\config". Check credentials, base url and absolute url.
4. Check .env file in "symcom-laravel-app". Check credentials, base urls and absolute urls.
5. Check "symcom-core-app\login.php" and follow associated scripts like "symcom-core-app\api\login.php", "symcom-core-app\api\unauthenticated-main-call.php". Print out responses and exit for furthur automatic navigation to different script.
6. Check related controllers in "symcom-laravel-app\app\Http\Controllers\Api" and add message in Exception clauses for better debug.
7. Check "symcom-laravel-app\config" and constants.php for any issues relating to static value declaration.
```
