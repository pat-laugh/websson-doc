---
last_modif: 2017-06-02
---
# The document

The document is what contains WebSSON code &mdash; the whole file. It is a
structure delimited by the file's start and end. It consists of a head and a body
implicitly separated. That is, the head cannot contain anything of the body, and
vice versa. The document implicitly starts with the head and as soon as an
element only belonging to the body is seen, the body starts.

## Document head

The document head is basically a list of entity definitions. It can contain the
definition for abstract and concrete entities. It can also contain imports and
options. A namespace can be expanded within the document head.

```websson
?concreteEntity = 0
!AbstractEntity { ?bodyComment:line-string is not allowed in head }
@Date //import
#--version:1.0.0 //option
^AbstractEntity //expand namespace

:Start of body since ^bodyComment
```
An import by itself acts like the expansion of a document's head, as if it were
a namespace being expanded.

The order of statements matter. Unlike in a namespace, a previously defined
entity can be used by another one.

All statements within the document head start with one of these characters: `?`,
`!`, `@`, `#`, and `^`. If the parser sees any other character, it assumes the
body starts. As for the expand operator, if the entity being expanded is not a
namespace, then the parser also assumes the body has started.

## Document body

The document body only contains concrete items and is meant to be directly
consumed by a user. The document body behaves exactly like a tuple, without the
parentheses. It cannot be mixed with elements that should be in the document
head. For example, you can't define an entity after the body started.