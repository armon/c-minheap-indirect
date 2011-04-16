# README

This is a very simple library for implementing a Min-Heap or Priority Queue
in plain C. It should be very understandable, and is a useful reference for
people who are learning C or want to understand the binary heap data structure.

What is somewhat interesting about this implementation is that it uses
an indirection table instead of a plain array as most implementations do.
The implications of this are that resizing (growing or shrinking) are very cheap.

In fact, we make use of the low level mmap() utility to map in and out individual
pages of virtual memory, and avoid the overhead of using malloc(). We have a small
table (a few pages maximum), which serves as an index into the other pages we have
allocated, and jump through this to get to the actual data. Because of this, growing
the table requires simply mapping in a new page and adding it to the table, and
shrinking requires only that we unmap the page. If this does not make sense, I highly
recommend reading about virtual memory to get an understand of how memory really
works in modern operating systems.

A typical implementation would use a simple array, which when it runs out of space
"doubles" in some sense. There are various approaches, not necessarily a simple double,
thinks like the next Fibonacci number, next prime, etc.

# Using the library

To use the library you only need to include the heap.h header, and
link against the heap.c file. There is nothing fancy required.

# Testing the library

Included in the project is a file main.c which serves as a simple test file.
We randomly generate a large number of keys (variable, default to 10M), and
insert them into our heap. We then extract the keys and verify they are ordered.
To test this, just run `make` and then run the test program.


