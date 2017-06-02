---
last_modif: 2017-05-11
---
# Whitespace and separators

Whitespace is grouped into two categories: junk and line-junk.

Junk includes all Ascii control chars and the Ascii space. Junk also includes
comments, which are grouped as "junk operators". Junk operators start with a
forward slash.

Line-junk is junk excluding the newline char. It is useful for line-strings, and
anything else that requires junk only on a line to be ignored.

# Junk operators

Junk operators include the line-comment (`//...`), the multiline-comment
(`/*...*/`), and the line-escape. Comments are covered [here](../comments).

The line-escape is declared with `/~`. It must be followed solely by line-junk.
It tells the parser to ignore the next newline, and ignore all line-junk on the
line immediately after. Since junk operators can be put in a line-string, this
can be useful to do the equivalent of the concatenation of line-strings. Like
for comments, within a line-string, it must be at the start of it or preceded by
line-junk to be considered as a line-escape.

```websson
:A concatenated /~ //a comment is considered line-junk
	line-string
```
The above example is equivalent to `"A concatenated line-string"`.

# Separators

The newline plays a special role in WebSSON, as it is considered a separator. It
is considered an implicit separator. There are two separators in WebSSON. The
other is the comma, which is considered an explicit separator.

The newline is considered implicit, because no matter how many there are,
between two values, there is considered to be only one separator. It doesn't
allow void values. The comma, however, allows void values. The comma is also
useful to separate values on the same line. Void values are only allowed in
templates where keys corresponding to a void value have a default value.

Let's say the following template head is used...
```websson
!Test<v1: def1, v2: def2, v3: def3>
```

...and there are two tuples that implement it:
```websson
tuple1 = Test (
	100
	
	300
)
tuple2 = Test (
	100,
	,
	300
)
```

`tuple1` would be equivalent to `(v1 = 100, v2 = 300, v3: def3)`.<br>
`tuple2` would be equivalent to `(v1 = 100, v2: def2, v3 = 300)`.