---
last_modif: 2017-06-19
---
# Text containers

Text containers avoid annoying repetition when a lot of strings are needed. They
put to light the usefulness of line-strings. A text container is preceded by
`::`. Only the list and tuple can be text containers. Using `::` followed by
braces creates a multiline-string, and while a text template head is allowed,
this is not the way to get one.

## Text list

A text list can only contain string values. However, a list can be expanded
inside it, as explained below. It's import to understand that **a text container
is only a convenience for the programmer; it doesn't enforce string values.**

`["s1", "s2", "s3"]`, `[:s1, :s2, :s3]`, and `::[s1, s2, s3]` are all equivalent.

## Text tuple

As written above, a text container is merely a convenience to easily write a lot
of strings. In a tuple, a key can still be assigned a value. This is done by
using the [explicit name char](../names#explicit-name).

`(:text, key=N, :more text)` and `::(text, $key=N, more text)` are equivalent.

## Expand

A container can be expanded within a text container. The expanded container
doesn't need to be a text container itself. The values in the container are not
converted to strings.

The following code is valid:
```websson
?numberedList[0, 1, 2, 3]

confusingList::[^numberedList, 4, 5, 6]
```
The value of `confusingList` is equivalent to `[0, 1, 2, 3, "4", "5", "6"]`.

## Separator

The empty line-string behaves differently in a text container. While `[:, :]`
and `["", ""]` are equivalent, `::[,]` would create an error. To use an empty
string within a text container, an escape must be used: `::[\e, \e]` is
equivalent to the two working examples.

This behavior allows the default value of a template head to be used while
having a text tuple. For instance, `<k1:s1, k2:s2, k3:s3>::(, s2, s3)` is
equivalent to `<k1:s1, k2:s2, k3:s3>(, :s2, :s3)`.

As a helpful summary, the chars to be wary of in a text container are: `$`, `^`,
and `,`. They might behave unexpectedly if you think every value in a text
container behaves as if an implicit `:` was put before them (that's a good way
to see how everything else behaves).

# End of line-string

In some other pages, it is written that the behavior of line-strings depends
on context without giving further details. Here's perhaps a good place to
explain exactly how they behave.

Line-strings behave differently depending on which container they are in. But
they only *might* be terminated by its end char or the separator.
They are however *always* terminated by the **newline**.

Whether or not the end char of the container or the separator terminates
line-strings is determined by how the container in which they are started. If
there is any non-[junk](../whitespace) character **on the same line** as the
**start char** of the container, then the **separator will always terminate them**.
Such a container is called a "line" container. The opposite is called a
"multiline" container. (I will eventually figure out a better terminology since
this brings confusion with the multiline-string, which can be both "line" and
"multiline".) This explains why something like `[:text, :text,]` is equivalent
to `["text", "text"]`.

The end char of the container, however, *might* end it.

In a "line" container, the start and end chars of the container are kept track
of within line-strings. This means that if the start and end of a container are
paired, then the end char doesn't end the line-string. For instance,
`(:()(), :([()]))` is equivalent to `("()()", "([()])")`.

In a "multiline" container, **the separator and the end char never end line-strings**.

```websson
[
	:A short poem, using commas, :And symbols like ] and }
]
```
This equivalent to `["A short poem, using commas, :And symbols like ] and }"]`!

---

The [document](../document) is a "multiline" container.