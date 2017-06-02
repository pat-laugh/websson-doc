---
last_modif: 2017-05-11
---
# Comments

Comments are ignored by the parser. There are two kinds of comments: the
line-comment and the multiline-comment.

Comments can be put nearly anywhere, including in a line-string.

## Line-comment

The line comment starts with `//` and last until the end of the line.

```websson
//this is a line-comment
```

## Multiline-comment

The multiline-comment starts with `/*` and ends with `*/`. Multiline-comments
may be put one into the other.

```websson
/* This multiline-comment
	/* contains another one within */
*/
```

## Within a line-string

Comments can be put within a line-string. They are only considered as a comment
if at the start of it or preceded by at least one whitespace character.

As such, the line-string `not//a comment`, would be equivalent to
`"not//a comment"`, whereas `is //a comment` would be equivalent to `"is"`.

Since a line-comment lasts until the end of the line, it ends a line-string.

Multiline-comments do not ever end a line-string, even if spread on multiple
lines &mdash; the multiline-comment makes the parser ignore any newline within
it that would've ended a line-string. Whitespace immediately following the end
of a multiline-comment is ignored, up to a newline (so only whitespace on the
same line as the `*/`).

The following code...
```websson
: This is /* comment */ a line-string /* another
	comment */ interspersed with comments //last comment
```
...would be equivalent to `"This is a line-string interspersed with comments"`.