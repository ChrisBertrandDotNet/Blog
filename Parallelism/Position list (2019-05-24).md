# Position list, let's replace indexes !

Here I present a general concept in programming, and a practicle implementation in C#.  
[code](https://github.com/ChrisBertrandDotNet/CB-Helpers/blob/master/Source/CB.Parallelism/CB.Parallelism.PositionList.cs)

## Why list __indexes__ are a problem on parallel programming ?

Let's examine this C# code:

````C#
int index = list.IndexOf("c");
list[index] = "c2";
````

In a mono-thread program, that is fine.  
But what if a parallel thread inserts an item to the list, _before_ the one previously indexed by the variable ``index`` ?

|  Thread 1  |  Thread 2  | resulting list |
| :-------- | :--------- | :--------- |
| ``var list = new List<string>() { "b", "c" };`` | | ``{ "b", "c" }`` |
| ``int index = list.IndexOf("c"); // index ← 1`` | | ``{ "b", "c" }`` |
| | ``list.Insert(0, "a");`` | ``{ "a", "b", "c" }`` |
| ``list[index] = "c2"; // wrong index !`` | | ``{ "a", "c2", "c" }`` |

In that example, ``"b"`` will be replaced, not ``"c"``. In other words, in the end the list is ``{ "a", "c2", "c" }`` where the expected result was ``{ "a", "b", "c2" }``.

## Let's replace the concept of indexes by a concept of positions

Here I call _Position_ an object that points at an item in the list and is not affected by insertions/deletions of items.

Technically, a Position contains an index, but the list itself maintains this index in order to always point at the item.  
In fact, the list manages a _collection_ of positions and maintains their index.  
Every position is tied to one list only and can't be used on another list.

Using positions, we would adapt the previous code this way:

|  Thread 1  |  Thread 2  | resulting list |
| :-------- | :--------- | :--------- |
| ``var list = new PositionList<string>() { "b", "c" };`` | | ``{ "b", "c" }`` |
| ``Position position = list.GetFirstOccurenceOf("c");`` | | ``{ "b", "c" }`` |
| | ``list.InsertBefore(list.GetStartPosition(), "a");`` | ``{ "a", "b", "c" }`` |
| ``list[position] = "c2";`` | | ``{ "a", "b", "c2" }`` |

- ``list.IndexOf()`` becomes ``list.GetFirstOccurenceOf()``.
- In order to insert at the start of the list, we need to get this position first:  
``list.GetStartPosition()``.
- Unlike insertion in List which is always before the given index, my implementation requires the caller to tell where the new item is inserted: before _or_ after the given position:  
``InsertBefore()`` or ``InsertAfter()``.

## The proposed PositionList

I created a class around this concept. It is written in C#, but the concept remains valid in any programming language.  
In the given source code, you can find it in the namespace ``CB.Parallelism``, under the name ``PositionList``.

The source source is available [here](https://github.com/ChrisBertrandDotNet/CB-Helpers/blob/master/Source/CB.Parallelism/CB.Parallelism.PositionList.cs).

The biggest difference with a regular list is ``PositionList`` manages the positions: you have to request position creations, deletions and movements.

On the other hand, a position is similar to an index since:
1. It points at an existing item (except when the list is empty).
1. After the pointed item is removed, the position points at the next item in the list.





### Why a regular lock ?

Although I like optimization, I implemented concurrency using an ordinary lock (keyword ``lock`` in C#), which is not the most efficient technique available.

The first reason is this first version is not much optimized for I was focused on the _concept_.

The second reason is a simple lock object lets you manage your concurrent operations more precisely.  
For example, let's imagine a function do several operations you consider as atomic, you can't let parallel threads interfer. So you just have to add a lock around your function's body and that works fine.  
The locking object is available in this property: ``SyncRoot``.

### RelativePosition

In the concept of indexes, lists usually inserts before the given index. It could have been after, it is just a choice then a standard.

In ``PositionList``, several operations need you tell where it must apply: before _or_ after the given position.
For example ``Insert``,  ``InsertAndGetNewPosition``, and ``MoveItem``, 

That is what the enumeration ``RelativePosition`` is about.

It serves for rank (position) comparison too.

