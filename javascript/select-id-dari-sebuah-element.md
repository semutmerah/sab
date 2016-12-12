## Select ID dari sebuah element (jQuery Alternatives)

Misal, pada dokumen HTML memiliki markup:
```
<div id="my-element-id"></div>
```

Maka cara select element tersebut pada javascript adalah:

```
var result = document.getElementById('my-element-id');
result.id === 'my-element-id'; // returns true
```

atau

```
var result = document.querySelector('#my-element-id');
result.id = 'my-element-id'; // returns true
```

Cara kedua (querySelector) lebih lambat dari pada cara pertama, namun akan membaik seiring perkembangan browser.
