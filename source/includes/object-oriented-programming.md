---
title: Classes and Objects
---

# Classes and object

## Precusor: namedtuple

```
from collections import namedtuple

Car = namedtuple('car', ['color','brand'])              # takes 2 arguments. Name and fields
print(Car._fields)                                      # ('color', 'brand')

myfirstcar = Car("red", "mini")
print(myfirstcar)                                       # car(color='red', brand='mini')
print(my_car.color)                                     # red, accessible by name
print(my_car[1])                                        # mini, index calls works as well.
print(*my_car)                                          # red mini
```

A "class" that churns out immutable tuples of fixed length. It is pre-built with `__repr__` and the instance elements are accessible by index calls of field names.

You can extend the benefits of namedTuples with inheritance.

Quote: "namedtuples are a memory-efficient shortcut to defining an immutable class in Python manually".

## Data classes

```
from dataclasses import fields          # note plural

Position = make_dataclass('Position', ['name', 'lat', 'lon'])   # single line syntax

Position.fields()                                       # (Field(name='name',type='typing.Any',repr=True...)

from dataclasses import make_dataclass

@dataclass                                              # the @dataclass decorator makes type hints mandatory
class Position:
    name: str
    lon: float = 0.0
    lat: float = field(default=0.0, repr=False)


home = Position("home")                                 # Position(name='home', lon=0.0, lat=0.0)
```

[Built-in module](https://docs.python.org/3/library/dataclasses.html#dataclasses.field) in the python standard library. It is a class decorator that pre-initializes with `__init__`, `__eq___` and `__repr__`/`__str__`.


## Class

```
from dataclasses import dataclass, fields

RANKS = '2 3 4 5 6 7 8 9 10 J Q K A'.split()
SUITS = '♣ ♢ ♡ ♠'.split()

@dataclass(order=True)
class PlayingCard:
    # init=False, this field is generated in __post_inti__()
    sort_index: int = field(init=False, repr=False)
    rank: str
    suit: str

    def __post_init__(self):
        self.sort_index = (RANKS.index(self.rank) * len(SUITS) + SUITS.index(self.suit))

    def __str__(self):  # used in Deck.__repr__
        return f'{self.suit}{self.rank}'
```

Create a class of **PlayingCards**, this class consists of 52 unique cards, with 13 ranks and 4 suits.

The `dataclassses` module helps to create helpful [dunder methods](#). In this example, adding the `@dataclass` decorators allows comparison of cards. Generates `__lt__` , `__le__` , `__gt__` , `__ge__`.
4 suits and 13 rau

When specifying default types that are outside of the basic data types (_int_,_str_), you can use the `typing` module. Especially for mutable arguments, like list, use the _default_factory_ parameter to define a default value.

```
from dataclasses import dataclass, field
from typing import List

def make_french_deck():
    return [PlayingCard(r, s) for s in SUITS for r in RANKS]

@dataclass
class Deck:
    # NOT List[PlayingCard] = make_french_deck()
    cards: List[PlayingCard] = field(default_factory=make_french_deck)

    def __str__(self):
        cards = ', '.join(f'{c!s}' for c in self.cards)                 # !s calls __str__ in PlayingCards
        return f'{self.__class__.__name__}({cards})'


Deck()
# Deck(cards=[PlayingCard(rank='2', suit='♣'), PlayingCard(rank='3', suit='♣'), PlayingCard(rank='4', suit='♣') ...)

print(Deck())
# Deck(♣2, ♣3, ♣4, ♣5, ♣6, ♣7, ♣8 ...)

from random import sample

hand = Deck(sample(make_french_deck(),k=5))
print(hand)                                     # Deck(♣Q, ♢K, ♣J, ♡2, ♢A)

```

