## Select element tag dari html (goodbye jQuery)

Misal, pada dokumen HTML memiliki markup:
```
<code>System.out.println("Hello Rasyid!");</code>
```

Maka cara select element tersebut pada javascript adalah:

```
var result = document.getElementsByTagName('CODE');
result[0].tagName === 'CODE'; // returns true
```

atau

```
var result = document.querySelectorAll('CODE');
result[0].tagName ==== 'CODE'; // returns true
```

atau jika diketahui hanya ada satu element tag <code>

```
document.querySelector('CODE').tagName === 'CODE';
```
