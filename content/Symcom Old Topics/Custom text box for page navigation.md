---
{"dg-publish":true,"permalink":"/topics/custom-text-box-for-page-navigation/"}
---

#comparison 

Custom text box in the comparison page is used to navigate to the page when sources are big and large number of pages are shown in the comparison process.

### Frontend Changes
1. Under `nav` html tag of the pagination section, a span tag is created with class  `custom-page-section`.
2. Inside this class an input element is taken with name and id as `custom_page_text_box`.
3. CSS changes are added in the `new-comparison-table-style.css` script under `dev-exp/assets/css`.

### Event Control
1. When id `custom_page_text_box` is changed, it is captured with`on change` JavaScript event.
2. The input value is validated only for digits and its range is checked within total number of pages.
3. Once validation is passed, the present address of the URL is taken in JavaScript variable `presentAddress`.
4. The variable `presentAddress` is checked for existence of page parameter and accordingly input page value is modified and the webpage is reloaded.
5. Failure of validation leads to display of alert with message "No symptoms to show."

Related Scripts:
- `comparison.php`
- `comparison-super.php`
- `new-comparison-table-style.css`
