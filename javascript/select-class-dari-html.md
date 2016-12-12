## Select Class dari html (goodbye jQuery)

Misal, pada dokumen HTML memiliki markup:
```
<span class="some-class"></span>
```

Maka cara select element tersebut pada javascript adalah:

```
var result = document.getElementsByClassName('some-class');
result[0].className === 'some-class'; // returns true
```

atau

```
var result = document.querySelectorAll('.some-class');
result[0].className ==== 'some-class'; // returns true
```
