## Select element berdasarkan siblings (goodbye jQuery)

Siblings berarti kita memilih element yang masih dalam satu level tree.
Misal, pada dokumen HTML memiliki markup:
```
<div id="parent">
  <a href="https://github.com/semutmerah">Github</a>
  <span>Span text</span>
  <p>Paragraph text</p>
  <div>Div text</div>
  Text node
</div>
```

Maka untuk mendapatkan siblings element / Node secara subsequent (setelah element start):
```
// "result" contains a NodeList of all siblings that occur after the <span>
// in our example HMTL at the start of this section. These siblings are
// the <p> and the <div> elements.
var result = document.querySelectorAll('#parent > SPAN ~ *');

// Another general sibling selector that specifically targets any
// subsequent siblings of the <span> that are <div>s. In our case,
// there is only one such element - <div>Div text</div>. The
// "result" variable is a NodeList containing this one element.
var result = document.querySelectorAll('#parent > SPAN ~ DIV');

// This is an adjacent sibling selector in action. It will target
// the first sibling after the <span>. So, "result", will be the
// <p>Paragraph text</p>
var result = document.querySelector('#parent > SPAN + *');
```

Sedangkan untuk mendapatkan siblings element / Node secara preceding (sebelum) dan subsequent (sesudah):

**Cara 1 (Modern Browsers)**:
```
// Find all siblings that follow the <span> in our example HTML
var allSiblings = document.querySelectorAll('#parent > SPAN ~ *');

// Converts the allSiblings NodeList into an Array.
allSiblings = [].slice.call(allSiblings);
var currentElement = document.querySelector('#parent > SPAN');

// This loop executes until we run out of previous siblings, starting with the sibling before the <span>.
// Each sibling is added to the allSiblings array. After this loop is complete,
// the allSiblings array will contain all siblings of the <span> (before and after).
do {
  currentElement = currentElement.previousElementSibling;
  currentElement && allSiblings.unshift(currentElement);
} while (currentElement);
```

**Cara 2 (IE 8)**:
```
var allSiblings = document.querySelectorAll('#parent > SPAN ~ *');

// Converts the allSiblings NodeList into an Array.
var allSiblings = [].slice.call(allSiblings);
var currentElement = document.querySelector('#parent > SPAN');
do {
  currentElement = currentElement.previousSibling;

  // This differs from the previous example in that we must
  // exclude non-Element Nodes by examining the nodeType property.
  if (currentElement && currentElement.nodeType === 1) {
    allSiblings.unshift(currentElement);
  }
} while (currentElement);
```

Traverse ke semua subsequent siblings: Web API, Modern Browsers, and Internet Explorer 8:
```
// The first nextSibling refers to the <p>, and the 2nd nextSibling
// refers to the <div>Div text</div> element. The final nextSibling
// refers to the "Text node" Text Node, since nextSibling targets
// any type of Node. So, the result is this Text Node.
var result = document.querySelector('SPAN').nextSibling.nextSibling.nextSibling;

// Same as the above example, but the final nextElementSibling returns null,
// since the last Node in the example markup is not an Element. There are only
// 2 Element siblings following the <span>. Note that nextElementSibling
// is not available in ancient browsers.
var result = document.querySelector('SPAN').nextElementSibling.nextElementSibling.nextElementSibling;
```
