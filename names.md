---
last_modif: 2017-05-10
---
# Names

A name starts with a letter or any non-Ascii char. After the first letter, there
can be digits. Hyphens and underscores can be put inside a name. They’re
considered separators; they can only be inside the name and cannot be put
consecutively. All names are case-sensitive.

## Keyword

A keyword is a name that always has a value. All keywords have aliases with an
equivalent value.

| Keyword | One-letter alias | Other aliases |
| ------- | ------- | --- |
| `null`  | `N` | `Null`, `nil`, `Nil` |
| `false` | `F` | `False` |
| `true`  | `T` | `True` |
| `bool`  | `B` | `Bool` |
| `byte`  | (none) | `Byte` |
| `short` | (none) | `Short` |
| `int`   | `I` | `Int` |
| `long`  | `L` | `Long` |
| `float` | `F` | `Float` |
| `double`| `D` | `Double` |
| `string`| `S` | `String` |

## Entity

An entity is a name that is equivalent to a value. There are two kinds of
entities: abstract and concrete. Abstract entities are declared with `!`, and
concrete entities with `?`. The name must not conflict with a keyword (except if
within a namespace, as explained far below).

Entities are used by simply writing their name, like for a keyword.

```websson
!person<first-name, last-name, age>
?name: Last

<person>
[
	(:First, name, 38)
	(:Second, name, 47)
]
```

## Key

A key is a name that is associated with a value. Except if in a dictionary, a key
must not conflict with a keyword or an entity.

### Explicit name

In cases where the same name as a keyword or entity must be used, the name can
be preceded with a `$`. This creates an explicit name.

For instance, this is valid:
```websson
$true = true
```

A key of the name "true" is associated with the keyword `true`.

## Namespace and scoped name

An entity within a namespace can be accessed by using the scope resolution
operator: `.`. Only a namespace may be followed by it.

```websson
!nspace { ?ent = 200 }
value = nspace.ent
```

An entity's name must only be unique within its namespace, and can be the same
as keywords or entities defined before.
