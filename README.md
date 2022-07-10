# Data structures and algorithms 

## Introduction to Data Structures 

A data structure organizes and stores data.  
There are many data structures, and they differ from each other in the way they organize and store the data.  
* Arrays organize data sequentially, and they place each value in its own slot. We can get to a slot using an index. 
* A tree is a hierarchical data structure, or some would say an abstract data type (it's a little bit of a gray area when it comes to trees). Trees have the notion of parents and children. 

Each data structure has strengths and weaknesses. They all do some things well - and other things, not so well. Because, if there were a 'super data structure' out there, that did every thing fantastically well, we would only need that one data structure, and everybody will be using it.  
* Arrays are great for random access, when we know the index of the item we want to access. But they are not so great, when we don't know the index - cause then we'd have to search the entire data set to find what we're looking for. 

> The fact is, there aren't just two sides to any issue, there's almost always a range of responses, and "it depends" is almost always the right answer in any big question. - Linus Torvalds 

So just like in this, also 'what is the best data structure ?' question also depends... on what data we want to store, how will our application access the data, the operations that will be performed on them (most on the data).... so, as a developer we'll have to decide which data structure to use, based on our application's specific needs.  

## Introduction to Algorithms 

An algorithm describes the steps we have to perform to accomplish a specific task. There can be more than one algorithm when accomplishing the same task.  
It is normal for an algorithm to make assumptions, mostly about the data.  
An algorithm is not the implementation. An algorithm describes the steps we have to perform - and an implementation is the code we write to actually perform those (if we're talking about programming). There can be many implementations for the same algorithm.  

* There can be many algorithms for the same task
* There can be many implementations for the same algorithm

## The Big-O Notation 

When we want to know, which implementation - of which algorithm performed the best, or performed the tasks fastest, we could just - log the start time - run the implementation 1 - and log the end time, and do the same thing for the next implementation. But that is not accurate in practise, because of hardware.  
Think about, we're running an implementation on a desktop computer - and again on a super computer, or else - we're comparing running time with a computer built in 2008 and 2015. The running time will sure vary, no matter whether the implementation was good or bad.  
So we need a more objective measure than just discreet running time. So, what we can do is - look at the number of steps that needs to be performed for a specific algorithm. We call this the time-complexity. There are two types of time-complexity, 
1. The time-complexity: the number of steps involved to run an algorithm (/implementation). 
2. The memory-complexity: the amount of memory that takes to run an algorithm (/implementation). 

In these days, the memory is very cheap (compared to time) - so the memory-complexity is not such an issue, so we really focus on the time-complexity.  
When we look at these, we should focus on the 'worst case', because - looking at the best case does not help, because it's very rare that we'd have the best case.  
We could take the average case, but that's not going to tell us the absolute-worst time-complexity. So, if we want to know what the upper-bound is, or what the absolute-worst time we can expect from this algorithm, it's much more helpful to look at the worst case and compare the worst case scenarios between two algorithms.  

| Big-O            |              |
|------------------|--------------|
| O(1)             | Constant     |
| O(logn)          | Logarithmic  |
| O(n)             | Linear       |
| O(nlogn)         | n log-star n |
| O(n<sup>2</sup>) | Quadratic    |

## Arrays

<code>int[] intArray = new int[7];</code>  

* Arrays are not a dynamic data structure, which means - once we create an instance of an array, we cannot change its size, so we need to specify the size of the array.  
* Arrays are stored as a single contiguous block in memory, which means - the elements of an array are not scattered throughout the memory. All of them are stored as one contiguous block. That's why we need to give the length of the array when we initialize it. That tells JVM how much memory it has to allocate for that array. It is also the reason why they cannot be resized.  
* Every element in an array, occupies the same amount of space in memory. When we're working with primitive data types, the data values get stored in the array. But when we're working with any non-primitive data (objects), what get stored in the array is a variable as an object reference.  
* If an array starts at memory address x, and the size of each element in the array is y, we can calculate the memory address of the <i>i<sup>th</sup></i> element by using the following expression: <code>x + i * y</code>  
* If we know the index of an element, the time to retrieve the element will be the same, no matter where it is in the array.  

![Array Big-O](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/1-array-big-o.png "Array Big-O")   

# Data Structures 

## Abstract Data Types 

An abstract data type isn't a concrete data structure. It doesn't dictate how the data is organized.  

Take a look at arrays. With arrays, we know the data is stored as a contiguous block - and all the elements occupy the same amount of memory.  
But abstract data types such as List don't do that. Lists are more of a conceptual idea. They dictate the operations we can perform on the dataset. 

In Java, a concrete data structure is usually a class (array might be an exception to that). But when it comes to an abstract data type, normally they are interfaces - they specify behavior.  

So, any data structure can be used to implement an abstract data type. As long as we have a class that implements the interface for the abstract data type, any class can behave like that abstract data type.  
In case of lists, any class that implement the List interface is a list. So, we can have a class that uses an array to implement the List interface.  

# List 

List is an abstract data type, it's not a concrete data type. Normally when it comes to abstract data types - there is an interface involved, and List is no exception.  

The data structures we'll discuss as Lists - all implement the [java.util.List](https://docs.oracle.com/javase/8/docs/api/java/util/List.html) interface.  

Classes that implement the List interface - represents an ordered collection, also known as a sequence.  
**AbstractList, AbstractSequentialList, ArrayList, AttributeList, CopyOnWriteArrayList, LinkedList, RoleList, RoleUnresolvedList, Stack, Vector** are popular implementations of List interface.  
If we ever want to implement our own List, we could use either AbstractList or AbstractSequentialList rather than implementing List interface itself. By extending one of the abstract lists because they are skeletal implementations of the List interface, so all we have to do is to override the specific methods that we want to implement.  

## ArrayList 

This is the go-to class when we want to store a collection of objects that we would want to iterate over sequentially.  
[JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html)

It is a **resizable-array** implementation of the List interface. This array is called the **backing array**.  

So, just like with arrays - if we know the indecies of our data, it would take constant time to access them. So, we would be able to easily iterate over an ArrayList, because all we do is iterating the index from 0 to the length of the list.  

But, we want to add a lot of items to an existing list, this will be slow - if the size of the list isn't large enough to accomodate the new items - in other words, if the backing array is already full, and if we want to add more items to the list, then we have to resize the backing array. Likewise, to remove items - we will have to shift the remaining items to remove the empty space.  

We can ensure that the backing array is large enough for our usage, by specifying the capacity of the ArrayList.  
There is an overloaded constructor for that. 

```java
ArrayList(int initialCapacity)
// Constructs an empty list with the specified initial capacity.
```

When it comes to ArrayLists, it's important to understand the difference between capacity and size.  
Capacity is the maximum numebr of items that the list can hold - before it has to resize the backing array.  
Size is the actual number of items in the ArrayList.  

If we don't mention the initial capacity, it's going to create a backing array with the capacity of 10. So, if we would have more than 10 items in the list, we'd be better off specifying the capacity.  

## Vector 

The Vector class is essentially a thread-safe ArrayList, but Vector actually came first. It has been in Java since JDK 1.0. ArrayList was only added to Java on JDK 1.2. Before ArrayList, Vector was the go-to list implementation.  
The reason why they added the ArrayList implementation that took over most uses of Vector - lies within the documentation.  
[JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/util/Vector.html)  

In the ArrayList Java documentation there is a highlighted note that says: **Note that this implementation is not synchronized.**  
And in the Vector documentation, it says: **Unlike the new collection implementations, Vector is synchronized.**  
This means, Vector is thread-safe. So, it's okay to use it from different threads without having **us** to synchronize the code. But ArrayList is not thread-safe. So, if we only read from an ArrayList, then it's safe to use from multiple threads - no data will be clobbered. But if we use ArrayList with multiple threads, and one or more of those threads is writing to the ArrayList by adding,deleting,setting, or changing objects in the list, then we can run into a conflict. 

So, if we want thread-safety - we can use Vector. The reason why ArrayList was introduced is that, the synchronization has an overhead involved. So back then, when there was only Vector as a List implementation backed by an array, we were forced to use a synchronized class - even if we didn't need.  

## Linked List 

A Linked List is a sequential list of objects. In linked lists, each item of the list is aware of another item in the list, because each item in the list contains a link to the next item in the list. So, we have to store some extra information with each item.  

* Each item is refered to as a Node. 
* The first Node in the list is called the Head Node. 
* And the last item in the list always points to null. 

So, we need to have a Node class - that has a field for what ever the object it's holding. And it also has to have a field `next` to refer to the next Node in the list.  

In the Linked List implementation, there should be a `head` field that points to the first item in the list. With the reference to the head, we can traverse the entire list.  

We always need to add new elements to the front of a linked list, because we only store a reference to the head. So, if we ever want to insert an item anywhere other than the front, we'd have to traverse the list to get there.  
And one of the best advantages in linked list is, if we add elements in the front - we can do it in constant time-complexity.  
To do that we can perform these steps: 
1. Create a new node with the given data. 
2. Assign the current `head` to the new node's `next` field. 
3. Assign `head` to the new node. 

There is a LinkedList implementation in [java.util.LinkedList](https://docs.oracle.com/javase/7/docs/api/java/util/LinkedList.html). It is a doubly-linked list implementation that implements List and Deque interfaces.  
This class uses generics - so, we can use this class with any type of objects.  
The implementation contains its own Node class, so we don't have to write it ourselves.  

This implementation is not synchronized. If we ever use it with multiple threads, we'd have to synchronize it ourselves.  

**Important**: 
* The `add()` method of the List interface - adds items at the end of the List. 
* To iterate, we can use an Iterator using `list.iterator()` and use its `hasNext()`, `next()` and other methods. 

Whenever we want to use a linked list in Java, we could use the LinkedList class - as long as we don't mind the extra memory overhead due to the next and previous fields.  

There's another linked list type called **Circular Linked List**. This is a variation on the singly linked list. In this variation - the last node in the list doesn't point to null. Instead it loops back and points to the head of the list.  
An advantage of this is, we can traverse the entire list - starting from any node.  

# Stack 

A stack is an abstract (conceptual) data type - because, instead of dictating how we store the items, stacks dictate what operations we can do on the items.  

**LIFO** - Last in First out  
The last element we add to a stack is the first element we can remove from that stack. So, there is no random access. We are only allowed to remove the last added item.  

The call stack of Java is an example for stacks. The last method that we called is always the first one that got taken off the call stack. 

We can perform three operations on a stack:
* push - adds an item as the top item on the stack 
* pop - removes the top item on the stack 
* peek - gets the top item on the stack without popping it 

A stack can be backed by any data structure. But the ideal data structure for backing a stack is a linked list.  
With a singly linked list - we always work with the item at the front of the list.  
The last element we added get set to the head (or in this case the top). And whenever we remove an item, we always remove the head. So, we can perform all the operations in constant time.  

![Stack](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/50-stack.png "Stack")

The Stack implementation of Java - [java.util.Stack](https://docs.oracle.com/javase/7/docs/api/java/util/Stack.html)  
We could use this stack at any time for our purposes in Java.  

But, in this Java doc for the class Stack, it says **A more complete and consistent set of LIFO stack operations is provided by the Deque interface and its implementations, which should be used in preference to this class.**  
So it says, instead of using this class, we should use a class that implements the Deque interface.  

If we want a stack in our Java application, we could `Deque<Integer> stack = new ArrayDeque<Integer>();`. 
It is an implementation of the Deque interface that is backed by an array.  
Also, the LinkedList class of Java also implements the Deque interface. So, we could use that - if we don't want the resizing overhead.  

But, there are other methods in these implementations. Because they implement Deque, they have `push()`, `pop()` and `peek()` methods. But they also allow random access and other operations that should not be allowed in a stack.  
So, we could either - use one of those implementations and limit ourselves to using only the methods for a stack, to make it behave like a stack. Or, we could create our own Stack class, that is backed by one of those implementations. All we need to implement in our class is those methods we want to expose, and the implementation would be very simple.  

Array and LinkedList implementations of a stack: [\src\DataStructures\Stack](\src\DataStructures\Stack)  

Note that this LinkedList is a doubly-linked list. If memory is an issue, we'd have to implement our own singly-linked list class. 

# Queues 

Queues are an abstract data type, just like stacks - they dictate how we can access the data. And just like with stacks, we use other data structures to implement them.  

Unlike stacks, queues enforce a **FIFO - First in First out** behaviour. They are called queues, because they are like line-ups. 

We can perform three operations on a queue: 
* enqueue - adds an item to the end of the queue 
* dequeue - removes the first item in the queue 
* peek - gets the item at the front of the queue without removing it 

Just like with stacks, we can implement them with either arrays or linked lists.  
We also need to keep references to the front and the back of the queue.  
When we enqueue items, we add them to the back. And when we dequeue items, we remove them from the front. Peek returns the front item - without removing it.  

The time complexity would be similar to stacks. It would depend on what we back the queue with. 

Circular and non-circular array-backed implementations of a queue: [\src\DataStructures\Queue](\src\DataStructures\Queue)  

There is a Queue interface in the java.util package. [Java Documentation for java.util.Queue](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html)  
If we ever want to implement our own queue, we could use the [java.util.AbstractQueue](https://docs.oracle.com/javase/8/docs/api/java/util/AbstractQueue.html) class.  
There are several implementations of this interface in the JDK.  
The [java.util.LinkedList](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html) class implements this [java.util.Queue](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html) interface. So we can easily use an LinkedList to back our own Queue implementations.  

The [java.util.Concurrent.ArrayBlockingQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ArrayBlockingQueue.html)
is a bounded blocking queue that is backed by an array.  
Being **bounded** means, the backing array does not get resized. Once created - the capacity cannot be changed, attempts to put an element into a full queue will result in the operation blocking. Which means, if a thread tries to put an element to a queue with no space, that thread will be blocked until some other thread takes out an element and leaves some space. The same thing goes with removing. If a thread requests an element from an empty queue, it's going to block that thread until another thread to come along and add something to the queue.  
This implementation is meant to be used when there are more than one thread is accessing the queue. Often used in producer-consumer scenarios.  

The [java.util.Concurrent.ConcurrentLinkedDeque](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentLinkedDeque.html) is an unbounded thread-safe queue based on linked-nodes.  
This implementation is using an efficient non-blocking algorithm, so it doesn't block.  
Note that, the `size()` method does not take constant time. Because, this implementation of a queue can be accessed by multiple threads, determining the number of elements requires a traversal of the elements.  

The [java.util.Deque](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html) is a conceptual data type that supports insertion and removal at both ends.  
Deque is short for **double-ended queue** and it's usually pronounced deque (_dek_).  
The [java.util.LinkedList](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html) class implements this [Deque](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html) interface.  

Java has an  [java.util.ArrayDeque](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayDeque.html) class, which is a resizable array implementation of the [Deque](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html) interface. So it has no capacity restrictions.  

# Hash Tables 

Hash Table is an abstract data type. So it doesn't dictate how we store the data. We can back a hash table with whatever we want.  
Hash tables consist of key-value pairs. They provide fast-direct access to values using keys.  
When we add an item, we provide the key and the value. And when we want to retrieve the item, we need to provide the key - with that the hash table can very quickly retrieve the value. Hash tables are optimized for retrieval (when we know the key).  

Just like with arrays, we can think of array's index as the key. But with hash tables, the key doesn't have to be an integer. It can be any object.  

Associative arrays in PHP, dictionaries in Python and Maps in Java are types of hash tables. 

## Hashing 

Since a key can be any type of objects, under the covers - those keys are being converted to integers.  
One common way of backing a hash table is to use an array. And for an array, we have to have integer indices.  
To convert keys to integers we use hashing. Hashing maps keys of any data type to an integer. So essentially, a hash function maps keys to int.  

In Java, the hash function is `hashCode()` in the [java.lang.Object](https://docs.oracle.com/javase/7/docs/api/java/lang/Object.html) class. So, every class in Java has a `hashCode()` method. It is usually overridden.  

It is possible for a hash function to produce the same hash for two (or more) different value. That is known as a collision. There are strategies for dealing with collisions.  

## Load Factor 

The load factor tells us how full a hash table is. For example, if we are backing a hash table with an array, the load factor will tell us how full the backing array is.  

Load factor = number of items / capacity  
Load factor = size / capacity  

This is a balancing factor. We don't want the load factor to be too high - which means the array is almost full, or it to be too low - which means most of the space is unoccupied.  
Load factor being high - array being almost full means, there is a higher likelihood of collisions.  

Load factor can play a role in determining the time complexity for retrieval.  

![Hash Table](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/51-hash-table.png "Hash Table")  
![Hash Table](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/52-hash-table.png "Hash Table")  

## Linear Probing 

Check out [\src\DataStructures\HashTable\SimpleHashTable.java](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/src/DataStructures/HashTable/SimpleHashTable.java). It is an implementation that uses a very simple hashing function. We just use the modulo operator on the length of the backing array by the length of the key. That would give us an integer that's in the range of backing array's indices.  
But this could easily run into collisions. If more than one key has the same length, they get the same hash. To handle collisions in this, all we do is printing out a message to the console.  

To handle or prevent collisions in hashing, there are more sensible strategies that we could use. One of those is called **Open Addressing**. With open addressing, if a value already exists within a given index - taken by hashing a key (a different key), we just figure out a way to address another slot for the value.  

One way to do that is with **Linear Probing**. When we discover that a position for a hashed-key value is already occupied, we increment the hashed value by one. And then we check the resulting index.  
This is called a linear probing, because every time we increment the index - and that happens in a linear fashion, and every increment of the index is called a probe.  
Meaning, if we have to increment the index by one to find another position - we call it 'using one probe'. If we have to increment 3 times (by 3) to find another empty position, we call it 'using three probes'. The lower the number of probes - the better.  

In the [src\DataStructures\HashTable\LinearProbedSimpleHashTable.java](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/blob/main/src/DataStructures/HashTable/LinearProbedSimpleHashTable.java), linear probing technique is added to the previous [\src\DataStructures\HashTable\SimpleHashTable.java](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/blob/main/src/DataStructures/HashTable/SimpleHashTable.java).

### Rehashing 

That implementation still has a problem. After we have added a few items, and there are more than two elements that hashes to the same hashed index, we'd be putting those elements by linear probing more than once.  
For example, think we have elements X, Y, and Z - that has the same hashed index. So, we put X and then linear probe to add Y, and then again we linear probe to add Z.  
And, when we remove elements, if we remove one of the elements that were probed, that element would be set to null. And think, we remove Y. Then it would be set to null. Then, when we try to remove or get Z - we would not find it in the hash table. Because linear probed element in the middle does not exist now, it will stop probing from there.  

To get around this, there is a approac - to rehash the entire hash table. We need to rehash the table either at each add, or at each remove. The choice is ours - where we want to take this huge performance hit.  

The [src\DataStructures\HashTable\RehashedLinearProbedSimpleHashTable.java](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/blob/main/src/DataStructures/HashTable/RehashedLinearProbedSimpleHashTable.java) class is just as the [src\DataStructures\HashTable\LinearProbedSimpleHashTable.java](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/blob/main/src/DataStructures/HashTable/LinearProbedSimpleHashTable.java) - but it rehashes the table at each removal. 

There is another variation of linear probing called **quardratic probing**. With that, instead of incrementing the hashed value by one, we increment it by some constant sqares. For example, we start our probing with incrementing by 1<sup>2</sup>, and then we increment by 2<sup>2</sup>, then 3<sup>2</sup>...  

## Chaining 

This is an alternative strategy to linear probing to deal with collisions. With this, instead of storing the values directly in the backing array, we store linked lists at each array position.  
When we go to add an element, and the key that we use has a hashed value that collides with the hashed value of another element in the hash table, that would not make any trouble. Because at each position in the array, there is a linked list. So, we can just add the second element to that linked list.  

The drawback with this approach is, at each get or removal, we have to search the entire linked list for the element with the key we're interested in. But, with a good hashing function and a good load factor, these linked lists will typically be short.  

When we use this approach, we need to initialize each array position with a linked list. We could do that either in the constructor for the hash table, or at each add call.  
Also, some implement this technique - backed by an Object array. If we get a collision, we store a linked list at that index. Otherwise, we can just store the value.  

The [src\DataStructures\HashTable\ChainedHashTable.java](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/blob/main/src/DataStructures/HashTable/ChainedHashTable.java) class is an implementation of a hash table that uses chaining instead of linear probing.  

In reality, most of the time - linear probing would be faster than chaining. And without having to use linked lists, we also don't get the redundant memory usage. But chaining is much simpler to implement than linear probing.  

## JDK implementations 

[java.util.Map](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) is the primary interface of Hash Tables in the JDK.  
**An object that maps keys to values. A map cannot contain duplicate keys; each key can map to at most one value.**  
This doesn't mean that there cannot be collisions. This tells, for only one key - there can be one value. That makes sense, because otherwise we will not be able to identify which value should we return for that key.  

[java.util.HashMap](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html) is a concrete implementation of [Map](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) interface.  
It permits constant time on all basic operations - unless it has to resize the backing array, or rehash the table. But it also allows us to set the load factor that we want - an when that load factor is exceeded, the hash table is resized. The default load factor is 0.75.  

This implementation is not synchronized. If we want to use if for multiple threads, we can wrap it using the `Collections.synchronizedMap()` method.  

One subclass of [HashMap](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html) is [java.util.LinkedHashMap](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashMap.html).  
**Hash table and linked list implementation** of the Map interface, with predictable iteration order. This implementation differs from HashMap in that it maintains a doubly-linked list running through all of its entries. This linked list defines the iteration ordering, which is normally the order in which keys were inserted into the map.  
It is still backed by an array. But it also put all of its entries to a linked list. This is also not synchronized, we can use `synchronizedMap()` just as before to synchronize it.  

In this implementation, there is a `removeEldestEntry(Map.Entry)` method. With that, we can remove the oldest entry from the map - every time we add a new one.  
This is useful, when we use the map instance as a chache. In that case, we wouldn't want the map to keep growing - because for a cache, it's to provide instance access for things we used recently. That's why we would want to remove the oldest (the one that's been in the list for the longest) entry.  

There is also a [java.util.Hashtable](https://docs.oracle.com/javase/8/docs/api/java/util/Hashtable.html) class. This differs from HashMap in a couple of ways.  
First of all, with this - we cannot add null keys or values. But HashMap allows to add null values.  
This is also a synchronized implementation. This falls to the same situation as it was with Vector and ArrayList.  

But, if we ever want a synchronized implementation, we could wrap any other implementations with the `Collections.synchronizedMap()` method.  
Or, there is also a [java.util.Concurrent.ConcurrentHashMap](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentHashMap.html) class. This is a synchronized implementation, and it supports full concurrenct of retrievals and high expected concurrency for updates.  

There is a lot of support in the JDK for Hash Tables. So, if we want to use a hash table in our application, under specific circumtances - there sure will be a suitable implementation already in the JDK.  

Check out [Bucket Sorting](/Sorting.md), it is a important sorting algorithm in hash tables. 

# Trees 

Some say trees are data structures - and others say they are abstract data types. It's a little bit of a gray area when it comes to trees - because they do dictate how to organize the data.  
We can write trees using Tree and TreeNode classes - but we can also back certain tree types with arrays.  

![Tree](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/55-trees.png "Tree")

* Trees are hierachical data structres.  
* Every circle in this tree is called a node.  
* These nodes can have any number of children. But, each node can have one and only one parent.  
* There is a special node in every tree - called the root. The root node does not have a parent. Every tree can have one and only one root node.  
* Each pointing arrows is called an edge. They always point from the parent to the child.  
* A leaf node has no children.  
* A tree with only one node (the root node) is called a singleton tree.  
* Every tree consists of one or more sub trees.  
* Trees cannot have cyclic paths.  
* The depth of a node is the number of edges from the node to the root.  
* The height of a node is the number of edges on the longest path from the node to a leaf. The height of a tree - is the height of its root node.  
* A level of a tree contains all the nodes that are at the same depth.  
* We say a node is an ancestor of another node - if it's in that node's path. A node can have multiple ancestors, and its ancestors are all the nodes from that node to the root.  

Trees are ideal when things can contain other things or when things can descend from other things. Any hierachical structure would be good to implement with trees. Java's class hierachy is a tree - or the file system in HDDs.  

# Binary Tree 

![Binary Tree](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/56-binary-tree.png "Binary Tree")

A binary tree is a tree in which every node has 0, 1 or 2 children. And because a node can possibly have two children, when we talk about nodes - we refer to the two children as the left child and the right child.  

![Complete Binary Tree](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/57-full-binary-tree.png "Complete Binary Tree")  

A binary tree is called - complete, if every level except the last level has two children. So, in the last level of the tree - all the nodes must be as left as possible.  

![Full Binary Tree](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/58-full-binary-tree.png "Full Binary Tree")  

A full binary tree is a complete tree as well, but in a full binary tree - every node other than the leaves, has to have two children. It's okay to have incomplete binary trees.  

# Binary Search Tree   

In practice, we only use binary search trees. The reason they are very popular is - we can perform insertions, deletions and retrievals in O(logn) time.  
They also have faster searching than unsorted arrays do, but equivalent time complexity to sorted arrays.  
With BSTs, every node that is left from a parent node is lower than the parent node. And everything that is right to a parent node is greater than the parent node.  

![Binary Search Tree](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/59-binary-search-tree.png "Binary Search Tree")  

![Binary Tree](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/56-binary-tree.png "Binary Tree")  

Some implementations dictate that duplicate values are not allowed.  
If we ever want to store duplicates - one way to do that is to store duplicates either in the left sub tree, or the right sub tree. We have to choose one and stick with it.  
Another approach is to have a counter with each node. So, rather than adding a seperate node for duplicate values, we can just increment the counter.  

We can get the minimum value of a BST just by taking the leftmost node. And the maximum value from the rightmost node.  

![Binary Search Tree](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/60-binary-search-tree.png "Binary Search Tree")  

The order in which we insert the elements is going to influence the ultimate ordering of the nodes in the tree.  

We put the first element at the root, and then insert subsequent elements in their sorted order. If we had used a different order of insertion - or if we had shuffled the data set before insertion, we will end up with a different tree.  

If we insert sorted data into a BST, we'd end up with either fully left leaning tree or a fully right leaning tree - depending on the ascending or descending ordering.  
That is not a good thing. It would essentially be a linked list.  
Ideally, when we build a binary search tree - we must try to keep it as balanced as possible. There are types of BSTs that are self-balanced. Most popular ones are AVL trees and Red-Black trees.  

There are 4 ways to traverse a tree.  
![Binary Search Tree](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/61-bst.png "Binary Search Tree")  
![Binary Search Tree](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/62-bst.png "Binary Search Tree")

1. Level order : 25, 20, 27, 15, 22, 26, 30, 29, 32  
2. Pre-order : 25, 20, 15, 22, 27, 26, 30, 29, 32 
3. In-order : 15, 20, 22, 25, 26, 27, 29, 30, 32 
4. Post-order : 15, 22, 20, 26, 29, 32, 30, 27, 25 

![Binary Search Tree](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/63-bst.png "Binary Search Tree")

For deleting nodes, there are three possible cases:  
1. Node is a leaf.  
This case is really easy. All we need to do is null out the node - from the parent node. 
2. Node has only one child.  
In this case, all we do is - we replace the node we're deleting with its only child. 
3. Node has two children.  
![Binary Search Tree](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/64-bst.png "Binary Search Tree")  

There are not a lot of tree implementations in the JDK. The one that we'll probably use is [java.util.TreeMap](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) class.  
It takes key-value pairs. It says, **it is a Red-Black tree based NavigableMap implementation. The map is sorted according to the natural ordering of its keys, or by a Comparator provided at map creation time, depending on which constructor is used.**   
Red-Black trees are self-balancing trees. That does not mean they are always perfectly balanced. But they are the best available and highly used tree structure these days because - they have a good tradeoff between balancing a tree to a good enough degree and performance.  

So, if we use a TreeMap, we'll be using a red-black tree in the background. It guarantees O(logn) time for `containsKey()`, `get()`, `put()` and `remove()` - and that's because red black trees are BSTs.  

**Note that this implementation is not synchronized.** If we do need synchronization the map should be wrapped using the `Collections.synchronizedSortedMap()` method.  

There is also a [java.util.TreeSet](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html) class. In sets, the data structure cannot contain duplicate elements, and it is an abstract data type. This is an implementation that is based on TreeMap.  

# Heaps 

A heap is a special type of binary tree. Even though, the word 'heap' is commonly used in memory management, that is not what we're talking about in here.  

A heap is a complete binary tree - that satisfies the heap property.  
So, every level of the tree must be full - except, potentially the last level. And, if the last level is not complete - the existing leaves must all be as far to the left as possible.  
The **heap property** depends on whether we're talking about a **max heap** or a **min heap**.  

* Max heap: every parent has to have a value - greater than or equal to its children. 
* Min heap: every parent has to have a value - that is less than or equal to its children. 

![Heap](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/65-heap.png "Heap")  

Because heaps are complete, we don't need to create our own structure to implement the backing tree. We can use arrays.  

### Heapify 

When we add an element to an existing tree, we add it to the first available spot at the bottom level. But, once we've done that, the tree might no longer meet the heap property. So, we need to fix the tree, and that is the process called **heapifying**.  
We have to do this after inserting a node, and also after deleting a node.  

![Heap](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/66-heap.png "Heap")  
This is a heap!  

### Heaps as Arrays 

![Heap](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/67-heap.png "Heap")  

![Heap](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/69-heap.png "Heap")  

![Heap](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/68-heap.png "Heap")  

![Heap](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/70-heap.png "Heap")  

![Heap](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/71-heap.png "Heap")  

![Heap](https://github.com/dilshankarunarathne/data-structures-and-algorithms-note/raw/main/assets/72-heap.png "Heap")  

# Priority Queues 

Queues are usually FIFO. Items are removed from the queue, in the order that they were added. But what if we want to change that slightly and, if we always want to access the highest priority item. When we add an item - we assign it a priority, and when we remove an item, the highest priority item is the one that's removed. So, it's not FIFO anymore.  
For example, think of a queue at a hospital. Usually it's FIFO, but if there's an emergency - someone with high priority gets to go first.  

So, a heap is an ideal data strucutre for this. The value with the highest priority will always be placed at the root, so when we want to remove the highest priority item from a **max heap**, we can just remove the root.  

When it comes to priority queues, the common operations are:  
`insert` with priority, remove the highest priority item - which is called `poll` and `peek` which will return the item with the highest priority without removing it from the heap.  

Java has a [java.util.PriorityQueue](https://docs.oracle.com/javase/7/docs/api/java/util/PriorityQueue.html) class. This is an unbounded priority queue, based on a priority heap - so there is no limit on the number of items.  
What is interesting about this priority queue class is - it's actually a min heap. So, if we use an <Integer> PriorityQueue, the lower our number - the higher priority it has.  
It's also an array implementation, so that array is automatically resized.  
It is also not synchronized. If we want to use it with multiple threads, we should use a java.uti.PriorityBlockingQueue instead.  
We can use PriorityQueue with any type of object, as long as that class implements the Comparable interface. Or, we can pass a Comparator when we construct the PriorityQueue. If we wanted a max heaped priority queue, we can provide a Comparator with the constructor.  

Check out Heap Sort algorithm: [Sorting.md](Sorting.md)


### Notes on Sets: [Sets.md](Sets.md)  

# Sorting and Searching Algorithms 

### Notes on Sorting Algorithms: [Sorting.md](Sorting.md)  

### Notes on Searching Algorithms: [Searching.md](Sorting.md)  

