---
last_modif: 2017-06-09
---
# Strings

There are 3 ways to represent a string. There are the c-string, the line-string
and the multiline-string. The c-string is very simple. However, the line-string
and multiline-string are quite complex, so some details will be left out when
they are presented.

## C-string

The c-string &mdash; named as such because it is used in the C programming
language &mdash; is delimited by quotes. Everything within is part of the
string.

```websson
"this is a c-string"
```

## Line-string

The line-string is declared with a colon. Only characters on the same line as
the colon are part of the string. All whitespace before the first non-whitespace
char and after the last non-whitespace char is ignored.

For example, `:  a string  `, would be equivalent to `"a string"`.

## Multiline-string

The multiline-string is declared by two colons put together, followed by braces.

```websson
::
{
	This is a
	multiline-string
}
```

Each line behaves exactly like a line-string. The lines are appended together,
separated by a space. The above example would be equivalent to
`"this is a multiline-string"`.

## Escape characters

A character is escaped by using the backslash, immediately followed by another
character.

`\ [ 0 | a | b | c | e | f | n | r | s | t | v | x## | u#### | U######## ]`

The characters a, b, f, n, r, t, v, x, u, and U have the same meaning than in
the C programming language. There are also the chars e, for empty, s, for
space, and c, for escape (Ascii char). The escape s puts a space, which can be
useful if a space is needed at
the start or end of a line-string. The escape e puts nothing. It can be useful
to make it explicit that a string is empty.

The escape 0 represent the null char. It is **not** an octal escape! There are
no octal escapes in WebSSON.

All printable Ascii non-digit and non-letter chars are escapable. This means
`'\\'`, `'\"'`, `'\?'`, `'\:'`, etc., are all valid escapes.

## Escaped entities

An entity can be escaped by immediately preceding its name with a caret
(`'^'`). Only entities of type string are allowed to be escaped.

```websson
?name: First Last
result: My name is ^name!
```

The content associated with result would be `My name is First Last!`.

Entities can be escaped in any kind of string.