# Markdown syntax guide and writing on MWeb

## Philosophy

> Markdown is intended to be as easy-to-read and easy-to-write as is feasible.
> Readability, however, is emphasized above all else. A Markdown-formatted document should be publishable as-is, as plain text, without looking like it's been marked up with tags or formatting instructions.
> Markdown's syntax is intended for one purpose: to be used as a format for *writing* for the web.

<!-- more -->

## Notice

You can use  `CMD + 4` or `CMD + R` to preview the result.

## Headers

**Example:**

```
# This is an `<h1>` tag
## This is an `<h2>` tag
###### This is an `<h6>` tag
```

**Result:**

# This is an `<h1>` tag
## This is an `<h2>` tag
###### This is an `<h6>` tag

## Emphasis

**Example:**

```
*This text will be italic*
_This will also be italic_

**This text will be bold**
__This will also be bold__

*You **can** combine them*
```

**Shortcuts:**  `CMD + U`、`CMD + I`、`CMD + B`
**Result:**

*This text will be italic*
_This will also be italic_

**This text will be bold**
__This will also be bold__

*You **can** combine them*

## Newlines

End a line with two or more spaces + enter.
Just typing enter to newline,please set：`Preferences` - `Themes` - `Translate newlines to <br> tags`  enable ( default is enable )

## Lists

### Unordered

**Example:**

```
* Item 1 unordered list `* + SPACE`
* Item 2
* Item 2a unordered list `TAB + * + SPACE`
* Item 2b
```

**Shortcuts:**  `Option + U`
**Result:**

* Item 1 unordered list `* + SPACE`
* Item 2
* Item 2a unordered list `TAB + * + SPACE`
* Item 2b

### Ordered

**Example:**

```
1. Item 1 ordered list `Number + . + SPACE`
2. Item 2 
3. Item 3
1. Item 3a ordered list `TAB + Number + . + SPACE`
2. Item 3b
```

**Result:**

1. Item 1 ordered list `Number + . + SPACE`
2. Item 2 
3. Item 3
1. Item 3a ordered list `TAB + Number + . + SPACE`
2. Item 3b

### Task lists

**Example:**

```
- [ ] task one not finish `- + SPACE + [ ]`
- [x] task two finished `- + SPACE + [x]`
```

**Result:**

- [ ] task one not finish `- + SPACE + [ ]`
- [x] task two finished `- + SPACE + [x]`

## Images

**Example:**

```
![GitHub set up](https://help.github.com/assets/images/site/set-up-git.gif)
Format: ![Alt Text](url)
```

**Shortcuts:**  `Control + Shift + I`
The Library's document support drag & drop or `CMD + V` paste or `CMD + Option + I` to insert  the picture.
**Result:**

![GitHub set up](https://help.github.com/assets/images/site/set-up-git.gif)

In MWeb, you can use `-w + Number` to control image width, for example, set the image width 140px:

![GitHub set up-w140](https://help.github.com/assets/images/site/set-up-git.gif)

## Links

**Example:**

```
email <example@example.com>
[GitHub](http://github.com)
autolink  <http://www.github.com/>
```

**Shortcuts:**  `Control + Shift + L`
The Library's document support drag & drop or `CMD + Option + I` to insert attachment.
**Result:**

An email <example@example.com> link.
[GitHub](http://github.com)
Automatic linking for URLs
Any URL (like <http://www.github.com/>) will be automatically converted into a clickable link.

## Blockquotes

**Example:**

```
As Kanye West said:
> We're living the future so
> the present is our past.
```

**Shortcuts:**  `CMD + Shift + B`
**Result:**

As Kanye West said:
> We're living the future so
> the present is our past.

## Inline code

**Example:**

```
I think you should use an
`<addr>` `code` element here instead.
```

**Shortcuts:**  `CMD + K`
**Result:**

I think you should use an
`<addr>` `code` element here instead.

## Multi-line code

**Example:**

    ```js
    function fancyAlert(arg) {
        if(arg) {
            $.facebox({div:'#foo'})
        }
    
    }
    ```

**Shortcuts:**  `CMD + Shift + K`
**Result:**

```js
function fancyAlert(arg) {
    if(arg) {
        $.facebox({div:'#foo'})
    }

}
```

## Sequence and Flow chart

**Example:**


    ```sequence
    Andrew->China: Says Hello
    Note right of China: China thinks about it
    China-->Andrew: How are you?
    Andrew->>China: I am good thanks!
    ```

    ```flow
    st=>start: Start:>http://www.google.com[blank]
    e=>end:>http://www.google.com
    op1=>operation: My Operation
    sub1=>subroutine: My Subroutine
    cond=>condition: Yes
    or No?:>http://www.google.com
    io=>inputoutput: catch something...

    st->op1->cond
    cond(yes)->io->e
    cond(no)->sub1(right)->op1
    ```


**Result:** ( Please enable  `Preferences` - `Themes` - `Enable sequence & flow chart`, default is enable. )

```sequence
Andrew->China: Says Hello
Note right of China: China thinks about it
China-->Andrew: How are you?
Andrew->>China: I am good thanks!
```

```flow
st=>start: Start:>http://www.google.com[blank]
e=>end:>http://www.google.com
op1=>operation: My Operation
sub1=>subroutine: My Subroutine
cond=>condition: Yes
or No?:>http://www.google.com
io=>inputoutput: catch something...

st->op1->cond
cond(yes)->io->e
cond(no)->sub1(right)->op1
```


More info: <http://bramp.github.io/js-sequence-diagrams/>, <http://adrai.github.io/flowchart.js/>


## Tables

**Example:**

```
First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column
```

You can create tables by assembling a list of words and dividing them with hyphens - (for the first row), and then separating each column with a pipe |:

**Result:**

First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column


## Strikethrough

**Example:**

(like ~~this~~)

**Result:**

Any word wrapped with two tildes (like ~~this~~) will appear crossed out.

## Horizontal Rules

Following lines will produce a horizontal rule:


```
***

*****

- - -
```

**Result:**

***

*****

- - -

## LaTex

Use double US dollars sign pair for Block level Math formula, and one US dollar sign pair for Inline Level.

```
For example this is a Block level $$x = {-b \pm \sqrt{b^2-4ac} \over 2a}$$ formula, and this is an inline Level $x = {-b \pm \sqrt{b^2-4ac} \over 2a}$ formula.

\\[ \frac{1}{\Bigl(\sqrt{\phi \sqrt{5}}-\phi\Bigr) e^{\frac25 \pi}} =
1+\frac{e^{-2\pi}} {1+\frac{e^{-4\pi}} {1+\frac{e^{-6\pi}}
{1+\frac{e^{-8\pi}} {1+\ldots} } } } \\]

```

**Result:**

For example this is a Block level $$x = {-b \pm \sqrt{b^2-4ac} \over 2a}$$ formula, and this is an inline Level $x = {-b \pm \sqrt{b^2-4ac} \over 2a}$ formula.

\\[ \frac{1}{\Bigl(\sqrt{\phi \sqrt{5}}-\phi\Bigr) e^{\frac25 \pi}} =
1+\frac{e^{-2\pi}} {1+\frac{e^{-4\pi}} {1+\frac{e^{-6\pi}}
{1+\frac{e^{-8\pi}} {1+\ldots} } } } \\]

## Footnote

**Example:**

```
This is a footnote:[^sample_footnote]
```

**Result:**

This is a footnote:[^sample_footnote]

[^sample_footnote]: footnote text detail...

## Comment And Read More..

<!-- comment -->
<!-- more -->
Actions->Insert Read More Comment *OR* `CMD + .`

## TOC

**Example:**

```
[TOC]
```

**Result:**

[TOC]


