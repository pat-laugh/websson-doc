---
last_modif: 2017-05-26
---
# Entities

An entity is a name that is defined to be equivalent to a value. There are two
types of entities: abstract and concrete. They represent abstract and concrete
values.

After having been defined, they are used by writing their name, like for
keywords.

## Concrete entity

A concrete entity is defined by using `?` followed by a name. A concrete value
must then be assigned to the entity. A concrete value is anything that can be
used by itself.

```websson
//assign a number to entity
?age = 38
//assign a string to entity
?name: First Last
//assign a list to entity
?list = [0, 1, 2, 3]
```

## Abstract entity

An abstract entity is defined by using `!` followed by a name. The type of the
abstract value assigned to the entity depends on what follows. An abstract value
is anything that must be related to something to create a concrete whole.

### Template head

A template consists of a template head and a template body. It's useful to put a
template head inside an entity to avoid repetition.

```websson
!Person<name, age>
person1 = Person(:First Last, 38)
person2 = Person(:Second Third, 38)
```

### Namespace

A namespace groups entities together. Any type of entity can be defined in it.
It is declared by following the entity name with braces.

```websson
!nspace
{
	!Person<name, age>
	?age = 38
}
person1 = nspace.Person(:First Last, nspace.age)
```

### Enum

An enum is like a namespace, except only names are allowed, which are assigned
increasing number values, starting at 0. It is declared by following the entity
name with square brackets.

```websson
!Color [ Red, Green, Blue ]
color = Color.Red
```

The enum Color would be equivalent to a namespace defined like this:
```websson
!Color { ?Red = 0, ?Green = 1, ?Blue = 2 }
```