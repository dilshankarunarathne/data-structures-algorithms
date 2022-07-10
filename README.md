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

### Notes on Stacks: [Stacks.md](Stacks.md)  

### Notes on Queues: [Queues.md](Queues.md)  

### Notes on Hash Tables: [HashTables.md](HashTables.md)  

### Notes on Trees: [Trees.md](Trees.md)  

### Notes on Heaps: [Heaps.md](Heaps.md)  

### Notes on Sets: [Sets.md](Sets.md)  

# Sorting and Searching Algorithms 

### Notes on Sorting Algorithms: [Sorting.md](Sorting.md)  

### Notes on Searching Algorithms: [Searching.md](Sorting.md)  

