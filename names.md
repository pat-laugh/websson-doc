---
last_modif: 2017-05-10
---
# Names

A name starts with a letter or any non-Ascii char. After the first letter, there
can be digits. Hyphens and underscores can be put inside a name. They’re
considered separators; they can only be inside the name and cannot be put
consecutively. All names are case-sensitive.

## Keywords

Keywords are names that always have a value. There are two types: concrete and
binary template head. All keywords have aliases, the value of which are
equivalent. The following subsections show the keywords and their aliases.
All keywords can start with a capital letter. For instance, `true` can also be
written `True`. Most keywords have a single capital letter alias; there are no
single lowercase letter aliases.

### Concrete

| Keyword | Aliases    |
| ------- | ---------- |
| `null`  | `N`, `nil` |
| `false` | `F`        |
| `true`  | `T`        |

### Binary Template Head

| Keyword | Aliases | Size (bits) |
| ------- | ------- | ----------- |
| `bool`  | `B`     | 1  |
| `byte`  |         | 8  |
| `short` |         | 16 |
| `int`   | `I`     | 32 |
| `long`  | `L`     | 64 |
| `float` | `F`     | 32 |
| `double`| `D`     | 64 |
| `string`| `S`     | 0  |

## Entity

Entities are names that are equivalent to a value. There are two kinds of
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

## Keys

A key is a name that is associated with a value. Except in a dictionary, a key
must not conflict with a keyword or an entity.

### Explicit name

In cases where the same name as a keyword or entity must be used, the name can
be preceded with a `$`. This creates an explicit name.

For instance, this is valid:
```websson
$true = true
```

A key of the name "true" is associated with the keyword `true`. As said above,
in a dictionary, since there can only be key-values, all keys are implicitly
explicit.

## Namespace and scoped name

An entity within a namespace can be accessed by using the scope resolution
operator: `.`. Only a namespace may be followed by it.

```websson
!nspace { ?ent = 200 }
value = nspace.ent
```

Entities' names must only be unique within their namespace, and can be the same
as keywords or entities defined before.
