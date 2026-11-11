# Web Front-end Development

In this course, we learned client-side web development technologies. In the hierarchy of IoT Engineering, this course is located at the **Application Layer**, because the frontend provides the GUI in web browsers to display data and interact with users. 

We covered these core topics:
1. HTML5 Structure
2. CSS Box Model and Layout
3. JavaScript DOM Manipulation and Event-Driven Mechanism
4. Laboratory Practical Tasks
The Web Front-End workflow: 
```
HTML ---> DOM Tree ------> <-------CSSOM Tree <--- CSS
           ▲              |
           |              |
       JavaScript         |
                          ▼
                      Render Tree ---> Paint ---> Display
```
---

## 1. HTML5 Structure
HTML provides the structure of a web page and is parsed to DOM Tree, then HTML is not needed any more in this conversation. 

### Standard Structure
```javascript
<!DOCTYPE html>
<html>
    <head>
    </head>
    <body>
    </body>
</html>
```

### Tags & Elements
1 element = opening tag + content + closing tag or br, hr (void tag)
There're some semantic tags in order to avoid the overuse of `<div>` and make higher readability and accessibility.

### Block Elements vs Inline Elements
In the document flow, elements behave in two fundamental ways:
- **Block-level elements** (e.g., `<div>`, `<p>`, `<h1>`): Occupy an entire line, and have changeable `width` and `height`.
- **Inline elements** (e.g., `<span>`, `<a>`): Flow horizontally in 1 line. Have no changeable `width` and `height`.
- **Conversion**: We use `display: inline-block` or `display: flex` to let inline elements sit horizontally while accepting custom dimensions and padding.

---

## 2. CSS Box Model and Layout

CSS is used for styling and page layout. 

### The CSS Box Model
Every HTML element is rendered as a box. It includes 4 layers:
1. **Content**: The actual text, image, or child elements, configured via `width` and `height`.
2. **Padding**: Transparent inner spacing between the content and the border.
3. **Border**: The surrounding boundary line (width, style, color).
4. **Margin**: Transparent outer clearance separating this element from neighbouring boxes.

```
+---------------------------+
|          Margin           |
|  +---------------------+  |
|  |       Border        |  |
|  |  +---------------+  |  |
|  |  |    Padding    |  |  |
|  |  |  +---------+  |  |  |
|  |  |  | Content |  |  |  |
|  |  |  +---------+  |  |  |
|  |  +---------------+  |  |
|  +---------------------+  |
+---------------------------+
```


### Layout Tradeoff
We studied the evolution from traditional Float to modern Flexbox:
- **Float (`float: left/right`)**:
  - *Principle*: It takes elements out of the normal document flow to align them horizontally.
  - *Tradeoff / Drawback*: If child elements float, the parent container suffers from **Height Collapse** (its height collapses to zero). We must clear floats on the parent.
- **Flexbox (`display: flex`)**:
  - *Principle*: A modern 1-dimensional layout (row or column).
  - *Advantage*: No height collapse. It controls layout along the main axis (`justify-content: center`) and cross axis (`align-items: center`). It achieves perfect horizontal and vertical centering.
---

## 3. JavaScript DOM and Event-Driven Mechanism

JavaScript adds dynamic interaction to static web pages.

### DOM Tree and Operations
The **DOM (Document Object Model)** presents the HTML document in browser memory as a tree of object nodes. JavaScript can query, create, modify, and remove DOM nodes dynamically:
1. **Create**: `const newNode = document.createElement('newNode');`  
`parent.appendChild(newNode);`
2. **Modify**: `node.textContent = 'Hello World';`
3. **Query**: `document.querySelector("..")` 
4. **Remove**: `node.remove()`

### Event Handling: `addEventListener`
We learned the standard way to bind an event with callback: `addEventListener`
```javascript
button.addEventListener('click', function(event) {
    // Event callback logic
}, false); // false = bubbling phase
```
**Why `addEventListener`**:
1. Decouples JavaScript logic from HTML.
2. Allows binding multiple callback functions to the same element.

- **Event Bubbling**: When an event occurs on a child node, it bubbles up through the parent hierarchy to the root.

---


