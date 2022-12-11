
java's varible type can be never changed

in java, types are verified **before** the code run, if there are type issue, code will not be compiled

all functions in java are methods, which must be in a class.

don't do all the things within a function, which will make debuging more difficult.

the `static` notation before the inner nested classes will make it can't access the function and varibles outside of it.

invariants: a condition that is guaranteed to be true during the code execution, usually used to avoid special cases and to reason the code better.

types of parameterized classes :
* Integer
* Double
* Character
* Boolean
* Long

two ways to copy an array:
* loop
* System.arraycopy()
    * five parameters: the array being copied, the index begin to copy, the array copy to, the index of it, and the number of elements to copied

the latter is simpler and more readable.

when create a 2D array, we can just specify the length of first dimension
```java
int[][] matrix;
matrix = new int[4][];
```

or we can specify both：
```java
matrix = new int[4][3];
```
it's not allowed to create a array of unknown type in java, so we should create an array of `Object` and then cast it.

test-driven development:
write test before and run the test, it will be red (wrong), and write the implementation until it turns green, then refactor it to be faster.

Every variable in java has a compile-time type(static type), which is specified at declaration and can be never changed, and a run-time type(dynamic type), which is specified at instantiation.

If we call a method of a object with:
* compile-time type X
* run-time type Y

and if Y override the method, then Y's method will be called, it is called **dynamic method selection**.

use inheritance (extends and implements) only when there is a **is-a** relationship rather than **has-a** relationship.

the rules of java say that all constructors must start with a call to one of the super class's constructors.

but if you don't, then java will do it automatically (no parameter one).

compiler allows assignments based on compile-time types.

Overriding only applies to non-static methods.

The variables in an interface are all public static final.


when `final` is used for a mutable object, it will be still changable, the influence of `final` is to make this object can't point to other object (the address can't change) , but the object it is pointing is changable itself.

when instantiating a nested class, we should use `parentClass.new` annotation.

You need to implement iterable interface to support enhanced `for` loop, `itreator()` method must return an object that implemented the Iterator interface.

the checked and unchecked exception:
![](https://s2.loli.net/2022/07/19/dZG2ci4wPSoI17V.png)

you cannot import code from default package, so it's a bad idea to write classes in default package in a big project.

four levels of access control of java:
![four levels of access control](https://s2.loli.net/2022/07/20/kw6juUMFQ9WOhGT.png)

a class in the top level can only be public or no access modifier notation.

the method in an interface without access modifier is **public** actually.

there is **no** subpackages, even one package is in the folder of another package, thry are instinctly **two** packages.

the sulotion of topological sort: perform a DFS traversal from every vertex with indegress 0, but don't clear markups in between traversals.

a summary of graph problems:
![summary of graph problems](https://s2.loli.net/2022/07/25/uXB9np67jVemxfQ.png)

quick sort is just partition sort.

b-tree: trees whose node can have more than one keys inside it, and each node can have multiple children.