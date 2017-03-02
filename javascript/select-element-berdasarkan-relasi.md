## Select element berdasarkan relasi (goodbye jQuery)

Relasi yang dimaksud di sini adalah parent dan children.
Misal, pada dokumen HTML memiliki markup:
```
<div>
  <a href="http://fineuploader.com">
    <span>Go to Fine Uploader</span>
  </a>
  <p>Some text</p>
  Some other text
</div>
```

Maka untuk mendapatkan parent element / Node:
```
// Assuming "a" is the <a> element in our HTML example,
// "result" will be the the <div> above it.
var result = document.querySelector('A').parentNode;

// Assuming "span" is the <span> element in our HTML example,
// the first parentNode is the <a>, while "result" is the <div>
// at the root of our example markup.
var result = document.querySelector('SPAN').parentNode.parentNode;

// Assuming "someText" is the "Some text" Text node in our HTML example,
// "result" will be the the <div> that contains it.
var result = document.querySelector('P').parentNode;
```

Untuk mendapatkan children:
```
// Assuming "div" is an Element object containing the <div> in our example HTML,
// result will contain an HTMLCollection holding 2 elements: <a> and <p>.
var result = document.querySelector('DIV').children

// The result will contain a NodeList holding 2 elements: <a> and <p>
// from our HTML fragment above.
var result = document.querySelectorAll('DIV > *');

// The result will be all <p> children of the <div>, which, in this case
// is only one element: <p>Some text</p>.
var result = document.querySelectorAll('DIV > P');
```
