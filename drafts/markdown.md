name: title-slide
class: center, middle, inverse
layout: true
---
name: section-slide
class: left, middle, inverse
layout: true
---
name: default
class: left, top
layout: true
---
name: title
template: title-slide

# Syntax overview Markdown
---
name: section_block elements
template: section-slide

.right-column[
# Block Elements
&nbsp;

- Paragraphs
- Headers
- Blockquotes
- Lists
- Code blocks
- Horizontal Rules
]
---
name: paragraphs
.left-column[
# Block Elements
## Paragraphs
]
.right-column[
- Paragraphs separated by blank lines
- Line breaks by spaces at the end of lines
]
---
name: headers
.left-column[
# Block Elements
## Paragraphs
## Headers
### Blabla
]
.right-column[
Headers in *setext* style use equal signs and dashes.
    This is an H1
    =============

    This is an H2
    -------------
Atx-style headers use hash characters at the start of a line.

    # This is an H1

    ## This is an H2

    ###### This is an H6
]
---
name: blockquotes-1
.left-column[
# Block Elements
## Paragraphs
## Headers
## Blockquotes
]
.right-column[
Blockquotes use e-mail style notation with '>' characters
    > This is a blockquote with two paragraphs. Lorem ipsum dolor
    > sit amet, consectetuer adipiscing elit. Aliquam hendrerit mi
    > posuere lectus. Vestibulum enim wisi, viverra nec, fringilla
    > in, laoreet vitae, risus.
    > 
    > Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    > Suspendisse id sem consectetuer libero luctus adipiscing.

One '>' before the first line of a hard-wrapped paragraph is sufficient:

    > This is a blockquote with two paragraphs. Lorem ipsum dolor
      sit amet, consectetuer adipiscing elit. Aliquam hendrerit
      mi posuere lectus. Vestibulum enim wisi, viverra nec,
      fringilla in, laoreet vitae, risus.

    > Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
      Suspendisse id sem consectetuer libero luctus adipiscing.

]
---
name: blockquotes-2
.left-column[
# Block Elements
## Paragraphs
## Headers
## Blockquotes
]
.right-column[
Nesting of blockquotes by adding additional levels of >:

    > This is the first level of quoting.
    >
    >> This is a nested blockquote.
    >
    > Back to the first level.

Use of other Markdown elements within a blockquote:
    > ## This is a header.
    > 
    > 1.   This is the first list item.
    > 2.   This is the second list item.
    > 
    > Here's some example code:
    > 
    >     return shell_exec("echo $input | $markdown_script");
]
---
name: lists
.left-column[
# Block Elements
## Paragraphs
## Headers
## Blockquotes
## Lists
]
.right-column[
### Formatting of lists
  - Markup with `*`, `+`, `-`

  - Indentation of list markers up to 3 characters

  - List markers have to be followed by a space or tab

  - Blank lines between list items produce &lt;p&gt; tags in the output

  - Multiple paragraphs per item are possible - indent subsequent
    paragraphs by 4 spaces

  - Markers of blockquotes need to be indented

  - Code blocks have to be indented by 8 spaces

  - Numbers followed by a period at beginning of a line needs to be escaped
]
---
name: code blocks
.left-column[
# Block Elements
## Paragraphs
## Headers
## Blockquotes
## Lists
## Code Blocks
]
.right-column[
* Produced by indenting every line at least 4 characters

* Code block continues until unindented line

* Markdown syntax ignored within code blocks
]
---
name: horizontal rules
.left-column[
# Block Elements
## Paragraphs
## Headers
## Blockquotes
## Lists
## Code Blocks
## Horizontal Rules
]
.right-column[

* Horizontal rule tag (&lt;hr/&gt;) produced by three or more `-`, `*` or `_` characters

* Spaces between the characters are allowed
]
---
name: section_span elements
template: section-slide

.right-column[
# Span Elements
&nbsp;

- Links
- Emphasis
- Code
- Images
]
---
name: links
.left-column[
# Span Elements
## Links
]
.right-column[
- Inline links
        [an example](http://example.com/ "Title")
- Reference style
        [an example][id]
        [another example] [id]

        [id]: http://example.com/  "Optional Title Here"
- Alternative formattings of reference style links:
            [id]: http://example.com/  "Optional Title Here"
            [id]: http://example.com/  'Optional Title Here'
            [id]: http://example.com/  (Optional Title Here)

            [id]: <http://example.com/>  "Optional Title Here"

            [id]: http://example.com/longish/path/to/resource/here
                  "Optional Title Here"
- Also possible
        [Example][]

        [Example]: http://example.com/
]
---
name: emphasis
.left-column[
# Span Elements
## Links
## Emphasis
]
.right-column[
- *&lt;em&gt;-emphasis* by using one `*` or `_`
        _emphasis_
- **&lt;strong&gt;-emphasis** by using one `**` or `__`
        __emphasis__
- Escape for literal asterisks
        \*no emphasis\*
]
---
name: code
.left-column[
# Span Elements
## Links
## Emphasis
## Code
]
.right-column[
- Wrap code within a normal paragraph with backtick quotes (`)
- Use multiple backticks for code sections containing literal backticks
    <pre>
    \`\`There is a literal backtick \` here.\`\`

    \`\` \`n interesting tick \`\`
    <pre>
]
---
name: images
.left-column[
# Span Elements
## Links
## Emphasis
## Code
## Images
]
.right-column[
- Syntax for inline images
        ![Alt text](/path/to/img.jpg)
        ![Alt text](/path/to/img.jpg "Optional title")
- Syntax for Reference-style image:
        ![Alt text][id]

        [id]: url/to/image  "Optional title attribute"

- Use &lt;img&gt; tag for specification of dimensions
]
---
name: section_miscellaneous
template: section-slide

.right-column[
# Miscellaneous
&nbsp;

- Automatic Links
- Backslash Escapes
]
---
name: miscellaneous
### Automatic links
Links will be created for URLs and e-mail addresses

    <http://example.com/>
    <xyz@example.com>
### Backslash Escapes
Markdown provides backslash escapes for the following characters:
<pre>
\   backslash  
`   backtick  
*   asterisk  
_   underscore  
{}  curly braces  
[]  square brackets  
()  parentheses  
#   hash mark  
+   plus sign  
-   minus sign (hyphen)  
.   dot  
!   exclamation mark  
</pre>
---
name: section_gfm
template: section-slide

.right-column[
# Github Flavoured Markdown
&nbsp;

- Syntax Highlighting
- Miscellaneous
]
---
.left-column[
# GFM
## Syntax highlighting
]
.right-column[
Use of a fenced code blocks and `default` as default higlight style of the presentation

```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```
produced by the code block
    ```ruby
    require 'redcarpet'
    markdown = Redcarpet.new("Hello World!")
    puts markdown.to_html
    ```
and slide show argument

```javascript
<script type="text/javascript">
  var slideshow = remark.create({highlightStyle: 'default'});
</script>
```
* * *
```
Some other code without a language
```
]
---
highlight-style: sunburst
.left-column[
# GFM
## Syntax highlighting
]
.right-column[
Use of a fenced code blocks and a slide property for styling

```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```
produced by the code block
    ```ruby
    require 'redcarpet'
    markdown = Redcarpet.new("Hello World!")
    puts markdown.to_html
    ```
and slide property

    highlight-style: sunburst
* * *
```
Some other code without a language
```
]
---
name: gfm miscellaneous
.left-column[
# GFM
## Syntax highlighting
## Miscellaneous
]
.right-column[
- Underscores in a word do not highlight as originally defined: my_var_name
- URL autolinking http://example.com produced by
        http://example.com
- Strikethrough. ~~This should be removed.~~ produced by
        ~~This should be removed.~~
- A table can be created with the code
        | Left-Aligned  | Center Aligned  | Right Aligned |
        | :------------ |:---------------:| -----:|
        | col 3 is      | some wordy text | $1600 |
        | col 2 is      | centered        |   $12 |
        | zebra stripes | are neat        |    $1 |

| Left-Aligned  | Center Aligned  | Right Aligned |
| :------------ |:---------------:| -----:|
| col 3 is      | some wordy text | $1600 |
| col 2 is      | centered        |   $12 |
| zebra stripes | are neat        |    $1 |
]
---
template: title-slide
# The End
