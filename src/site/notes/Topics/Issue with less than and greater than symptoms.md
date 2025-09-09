---
{"dg-publish":true,"permalink":"/topics/issue-with-less-than-and-greater-than-symptoms/"}
---


This is one of the simplest scenario:

This is how a symptom exists in the word document.
```
||For twelve days pain below right scapula; < in evening, after exertion, by deep inspiration and by moving right arm; > by pressure and lying down, especially on right side; the pain extends over a spot as large as the palm; when severe it extends to corresponding part of left side.
```

This is how it is saved in the database by the program:
```html
<bar-two-normal>For twelve days pain below right scapula; &lt; in evening, after exertion, by deep inspiration and by moving right arm; &gt; by pressure and lying down, especially on right side; the pain extends over a spot as large as the palm; when severe it extends to corresponding part of left side.</bar-two-normal>
```

The < is saved as `&lt;` and > as` &gt;`
The semicolon appearing for these symbols, produces inappropriate results when processed by the program:
```html
<bar-two-normal class="text-grade-2">For twelve days pain below right scapula</bar-two-normal>;<bar-two-normal class="text-grade-2"> &lt;</bar-two-normal>;<bar-two-normal class="text-grade-2"> in evening</bar-two-normal>,<bar-two-normal class="text-grade-2"> after exertion</bar-two-normal>,<bar-two-normal class="text-grade-2"> by deep inspiration and by moving right arm</bar-two-normal>;<bar-two-normal class="text-grade-2"> &gt;</bar-two-normal>;<bar-two-normal class="text-grade-2"> by pressure and lying down</bar-two-normal>,<bar-two-normal class="text-grade-2"> especially on right side</bar-two-normal>;<bar-two-normal class="text-grade-2"> the pain extends over a spot as large as the palm</bar-two-normal>;<bar-two-normal class="text-grade-2"> when severe it extends to corresponding part of left side</bar-two-normal>.
```

This processed symptom is shown to the user as:
```
For twelve days pain below right scapula; <; in evening, after exertion, by deep inspiration and by moving right arm; >; by pressure and lying down, especially on right side; the pain extends over a spot as large as the palm; when severe it extends to corresponding part of left side.
```

Note:
If the processed program is to be manipulated, the replacement of semicolon ; of &lt; or &gt; directly may change the symptom string as semicolon appears also as part of the symptom.

If processing is made with usage of < or > symbols, it affects the xml tags and overall symptom structure is disturbed.