---
---
<style>pre{tab-size:4;}</style>

WebSSON is a data format language. The goal is to have something that is
human-readable with minimal redundancy.

Other important goals in developing the language are making sure everything is
**consistent**, that there are **no surprises**, that it's **simple** to write,
and that it is **efficient** to parse and serialize.

I'm developing a parser and a serializer in C++. The source code is available
[here](https://github.com/pat-laugh/websson-libraries).

This page is intended as a quick tutorial. It is assumed that you'll infer a
personal understanding of the concepts. Further information about everything
will be provided in other pages.

## Basic structures

### Dictionary

A dictionary contains key-value pairs. It is declared with braces.

```websson
{
	first-name: First
	last-name: Last
}
```

### List

A list only contains values. It is declared with square brackets.

```websson
[
	true
	123
]
```

## Keys and values

### Keys

A key is a name. A name starts with a letter or any non-Ascii char. After the
first letter, there can be digits. Hyphens and underscores can be put inside a
name. They're considered separators; they can only be inside the name and cannot
be put consecutively. All names are case-sensitive.

Examples of valid names: `a-name`, `a_name`, `aName`, `a01`.

### Value

A value can be a name. It is then considered a keyword or an entity. Entities
are names that someone associated with a value.

An incomplete list of keywords include: `null`, `false`, `true`.

A value can also be a number. A number starts with a digit.

It can be a string. A string can be put within quotes, or can be declared using
a colon, as seen above. The colon represents a *line-string*, a string that fits
on a single line. Everything after the colon is considered part of the string.

It can also be a structure.

### Associating a value to a key

In the example of the dictionary, there are keys associated to values. There,
strings are associated to keys. The meaning of the colon is very different in
WebSSON than in a lot of other languages. It really means to assign a
line-string. Therefore, doing something like `key: 123` would associate a
**string** to the key, and not a number!

To associate a number, and anything else, to a key, the equal sign is used.
For anything that is declared without using the start of a name or a number, the
equal string can be omitted.

Here's an example:
```websson
{
	first-name: First
	last-name: Last
	age = 38
	numbers
	{
		home: 890 456-7123
		work: 890 357-1246
	}
}
```

## Advanced structures

### Tuple

A tuple is like the mixture of a dictionary and a list. It maintains the order of
values (like a list), and its values can be accessed by name (like a
dictionary). It is declared using parentheses.

```websson
(
	name: First Last
	38
)
```

### Template

A template is used in conjunction with tuples to avoid duplication of keys. It
is declared using angle brackets.

For example, to make a list people's names and age, a template could be used to
avoid redundant keys:
```websson
<first-name, last-name, age>
[
	(:First, :Last, 38)
	(:Second, :Third, 47)
]
```

The example shows a list of tuples sharing the same keys, but with different
values associated with them. We can also see the line-strings being terminated by
a comma. This is not always the case. Their behavior depends on context.

## More stuff

This page describes very succinctly a few of the language's functionalities.
More information will eventually be written....

More information about [strings](strings).

## Inspiration based on other formats

Formats like XML and JSON are considered to be human-readable, but to me they
don't seem as readable as a human-readable format should be. I looked at
something like YAML, but I don't like container limits based on tablature. Also,
YAML doesn't allow tabs (the character), which is just very bad.... About XML,
it really annoys me to have to remember what tag was opened to then specify it
when closing it. Using tablature or chars signalling the start and end is much
better. JSON is good, but not good enough. You could consider WebSSON to be an
improvement based on JSON. I've used CSV. You can easily get the equivalent of
CSV with WebSSON.

WebSSON is not a superset of JSON, although you can achieve the same using very
similar syntax. Especially, strings in WebSSON are **not** exactly like strings
in JSON. I tried to make things similar, but only if it did not negatively
affect the quality of the language.

By the way, WebSSON is an acronym for WebSS Object Notation. WebSS is another
language I am developing. Its name is an acronym for Web Source-to-Source. I
started developing WebSS before WebSSON, but have since spent much more effort
on WebSSON.