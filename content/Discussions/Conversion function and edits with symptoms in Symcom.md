---
{"dg-publish":true,"permalink":"/discussions/conversion-function-and-edits-with-symptoms-in-symcom/"}
---


```
*Severe headache,° with deep red eyes and dry lips.
```

```html
*<asterisk-bold>Severe </asterisk-bold><asterisk-bold>headache</asterisk-bold><asterisk-normal>,</asterisk-normal>°<degree-normal> with deep </degree-normal><degree-em>red eyes</degree-em><degree-normal> and dry lips</degree-normal>.
```

Above string is passed as a parameter to conversion function. 

```php
// Inside conversion function
//...
//...
$conversionArr = array(
				'asterisk-normal' => '',
				'asterisk-bold' => 'strong',
				'degree-em' => 'em',
				'degree-normal' => '',
				'degree-bold' => 'strong'
			);
```

```html
*<strong>Severe </strong><strong>headache</strong>,° with deep <em>red eyes</em> and dry lips.
```


Global grading values:
```
grade 1 : normal
grade 2 : italics
grade 3 : bold
```


Grade settings for a particular source:
![Pasted image 20250211113451.png](assets/images/Pasted%20image%2020250211113451.png)
