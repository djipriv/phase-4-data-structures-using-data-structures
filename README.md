# Using Data Structures

## Learning Goals

- Define "Data Structure"
- Evaluate the properties of common data structures (arrays and hashes)
- Establish a general process to build data structures
- Identify when to use different data structures

## Introduction

What is a data structure? In essence, a data structure is a tool for organizing
a collection data so that we can interact with it efficiently. All data
structures share the following characteristics:

- They store **collections of values**
- They also store the **relationship between those values**
- They provide **methods for interacting with those values**

Consider a data structure you've been using for quite some time: an **array**.
Arrays are a common data structure that are built in to most programming
languages. In Ruby and JavaScript, arrays have the following characteristics:

- They stores a collection of values of any data type
- They stores those values in an indexed list
- They provide many methods for interacting with those values, like:
  - accessing elements at a particular index position
  - adding elements
  - removing elements
  - and iterating through every element

## Why Do We Need Different Data Structures?

While built-in data structures like arrays and hashes are useful in many
scenarios, it's also beneficial to be able to create custom data structures that
can be used to help solve specific problems **more efficiently** than using
built-in data structures. Different data structures excel in different
situations.

For example, imagine a problem where you needed to add and remove elements from
the beginning of a list. If we tried solving this problem using an array, our
solution wouldn't be particularly efficient, since adding/removing elements from
the beginning of an array has a Big O runtime of O(n), because adding/removing
elements from the beginning of an array causes every other element in the array
to be re-indexed. We can solve these kinds of problems using another data
structure that you'll learn about later in this section, a **linked list**,
which has a O(1) runtime for adding/removing elements from the beginning of the
list.

In fact, you've already interacted a lot of different data structures besides
just arrays and hashes!

For example, any time you've interacted with the DOM in JavaScript, you've been
interacting with a special data structure known as a **tree**; and
[`querySelector`][] is a **tree traversal method** for efficiently finding a
child element within the DOM tree.

[`queryselector`]: https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector

React also uses its own custom data structure, the [React fiber tree][fiber],
which allows it to efficiently perform updates to the DOM based on changes to
state (and also is the reason you need to provide a special `key` prop for lists
of elements).

[fiber]: https://github.com/acdlite/React-fiber-architecture#what-is-a-fiber

Another place you've seen a common data structure in action is the
[call stack][], which uses a **stack** data structure to keep track of all the
currently running functions in a program and make sure they're executed in the
correct order.

[call stack]: https://en.wikipedia.org/wiki/Call_stack

In the rest of lessons in this section, we'll show you how to build some of
these common data structures, including linked lists, stacks, and binary search
trees, and identify when to use them to solve specific problems.

## Building Custom Data Structures

To get a sense of what the general process of building data structures is like,
let's build out our very own version of the `Array` data structure in Ruby. As a
reminder, every data structure we make needs a way to do the following things:

- Store **collections of values**
- Store the **relationship between those values**
- Provide **methods for interacting with those values**

To start off, every data structure we'll build will be defined as a class. For
our array implementation, we'll call our class `MyArray` to differentiate it
from the built-in `Array` class:

```rb
class MyArray
end
```

Each data structure will also use **another data structure** in order to store
the collection of values and help establish the relationships between them. To
build our custom `MyArray` class, let's use a `Hash` as the underlying data
structure, along with a `length` attribute to keep track of how many elements
are in the array:

```rb
class MyArray
  attr_reader :hash
  attr_accessor :length

  def initialize
    @hash = {}
    @length = 0
  end

end
```

Our data structures also need to provide **methods** for interacting with the
data. Here's how we could implement `push` and `pop` for this class:

```rb
class MyArray
  attr_reader :hash
  attr_accessor :length

  def initialize
    @hash = {}
    @length = 0
  end

  def push(value)
    self.hash[self.length] = value
    self.length += 1
  end

  def pop
    self.length -= 1
    self.hash.delete(self.length)
  end
end

arr = MyArray.new
arr.push(1)
arr.push(2)
puts arr.pop
# => 2
```

We've now defined our very own custom data structure! While it's highly unlikely
that you'll need to build your own _array_ class in the future, understanding
this general approach to building data structures will help when you need to
create other data structures that aren't provided by your programming language,
such as a linked list.

Another advantage of building custom data structures like this for solving
algorithm problems is that it makes it easier to understand the Big O runtime.

For example, in the code above, we can safely say that the `push` and `pop`
operations have a O(1) runtime, since accessing and deleting elements from a
hash has a O(1) runtime. You can refer to this [Big O Cheat Sheet][cheatsheet]
for more details on common runtimes.

> If you'd like to explore this further, try adding a `shift` and `unshift`
> method to the array class. How does adding/removing elements from the
> beginning instead of the end of the list affect the runtime of those methods?

## Conclusion

In this lesson, we defined a "data structure" as a tool that stores a
**collection of values** along with the **relationship between those values**
and provides **methods for interacting with those values**.

Different data structures are more efficient at solving different problems, so
the more data structures you familiarize yourself with, the more tools you'll
have at your disposal to tackle different kinds of problems as efficiently as
possible.

In general, building a data structure involves creating a class definition;
using an auxiliary data structure to store values; and writing different methods
for interacting with those values.

In the coming lessons, we'll explore several common data structures by providing
instructions on how to build them, and then giving problems to practice using
those data structures in different scenarios.

## Resources

- [Big O Cheat Sheet][cheatsheet]

[cheatsheet]: https://www.bigocheatsheet.com/
