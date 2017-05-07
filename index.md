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

## Inspiration based on other formats

Formats like XML and JSON are considered to be human-readable, but to me they
don't seem as readable as a human-readable format should be. I looked at
something like YAML, but I don't like container limits based on tablature. Also,
YAML doesn't allow tabs (the character), which is just very bad.... About XML,
it really annoys me to have to remember what tag was opened to then specify it
when closing it. Using tablature or chars signaling the start and end is much
better. JSON is good, but not good enough. You could consider WebSSON to be an
improvement based on JSON. I've used CSV. You can easily get the equivalent of
CSV with WebSSON.

WebSSON is not a superset of JSON, although you can achieve the same using very
similar syntax. Especially, strings in WebSSON are **not** exactly like strings
in JSON. I tried to make things similar, but only if it did not negatively
affect the quality of the language.