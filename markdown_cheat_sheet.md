# Markdown Syntax and Their Uses

## Headers

Depends on the size you need it ranges from 1 to 6
```markdown
# Header 1
## Header 2
### Header 3
#### Header 4
##### Header 5
###### Header 6
```

## Emphasis

Italics

```markdown
*italic text*
```

or

```markdown
_italic text_
```
Renders text in italics.

### Bold
```markdown
**bold text**
```
or

```markdown
__bold text__
```
Renders text in bold.

### Strikethrough
```markdown
~~strikethrough text~~
```
Renders text with a strikethrough.

## Lists
Unordered List
```markdown

- Item 1
- Item 2
- Item 3
```
or

```markdown

* Item 1
* Item 2
* Item 3
```
Creates an unordered (bulleted) list.

Ordered List
```markdown

1. Item 1
2. Item 2
3. Item 3
```
Creates an ordered (numbered) list.

Nested List
```markdown

- Item 1
  - Subitem 1
  - Subitem 2
- Item 2
```
Creates a nested list.

### Links
Inline Link
```markdown
[link text](http://example.com)
```
Creates an inline link.

Reference Link
```markdown
[link text][1]
...
[1]: http://example.com
```
Creates a reference-style link.


### Images
Inline Image
```markdown

![alt text](http://example.com/image.jpg)
```
Displays an inline image.

Reference Image
```markdown
![alt text][1]
...
[1]: http://example.com/image.jpg
```
Displays a reference-style image.

### Code
Inline Code
```markdown

`inline code`
```
Renders inline code.

Code Block
<pre>
```markdown
```
code block
```
</pre>
Creates a code block.

Syntax Highlighted Code Block
<pre>
```python
print("Hello, world!")
```
</pre>
Creates a syntax-highlighted code block.


## Blockquotes
Blockquote
```markdown
> This is a blockquote.
```
Creates a blockquote.

Nested Blockquote

```markdown
> This is a blockquote.
> > This is a nested blockquote.
```
Creates a nested blockquote.

### Horizontal Rule
Horizontal Rule
```markdown
---
```
or

```markdown
***
```
or

```markdown
___
```
Creates a horizontal rule.

## Tables
Table
```markdown
| Header 1 | Header 2 |
|----------|----------|
| Cell 1   | Cell 2   |
| Cell 3   | Cell 4   |
```
Creates a table.

## Task Lists
Task List
```markdown
- [ ] Task 1
- [x] Task 2
```
Creates a task list with checkboxes.

## HTML

HTML Tags
```markdown

<p>This is a paragraph in HTML.</p>
```
Allows embedding HTML tags within Markdown.

