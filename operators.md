---
last_modif: 2017-06-01
---
# Operators

There are only two operators in WebSSON: the dot operator, and expand. There is
no addition for numbers, no concatenation for strings, not even a unary minus
or plus sign.

## Dot operator

The dot operator is represented by a period. It is used to access the member of
a namespace or enum.

```websson
!Nspace { ?Member = 0 }
!Enum [ Member ]
Nspace.Member //0
Enum.Member //0
```

## Expand

Expand is represented by a caret. What it does is take an entity and make it so
as if the contents of the entity were in place of where expand is used.

It can be used in strings to do the equivalent of a concatenation:

```websson
?s: more content
:There is ^s.
```
This is equivalent to `"There is more content."`

It can also be used in any container.

```websson
?aList[1, 2, 3]
[0, ^aList, 4, 5]
```
This equivalent to `[0, 1, 2, 3, 4, 5]`.

### Restrictions

Expand can only be used with entities matching the type of the container
they're expanded within. So only a string can be expanded within a string, only
a list can be expanded within a list, etc.

Expand is a unary operator and so must always be immediately followed by its
operand.

### Within a string

Within a string, if the expand operator is not immediately followed by a
name-start (indicating an entity) then it is interpreted as a regular character
without any special meaning. For instance, the strings `"a ^ caret"` and
`"a \^ caret"` are equivalent.

If the entity is a namespace, it may be expanded by using the dot operator. The
dot operator is a binary operator and so in usual circumstances allows
whitespace between its operands, but in a string no whitespace is allowed.

```websson
!Content { ?s: more content }
:There is ^Content.s.
```
This gives the same result as above.

### The document

The body of the document is equivalent to a tuple. Therefore, tuples can be
expanded within it.

The head of the document is equivalent to a series of entity declarations.
Therefore, namespaces can be expanded within it, making all entities in the
namespace accessible without having to reference it using the dot operator. This
cannot be done with enums.