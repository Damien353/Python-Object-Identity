# Understanding Python: Object Identity, Mutability, and Function Behavior

## Introduction

In Python, understanding how different types of objects behave, how they interact with memory, and how they are passed to functions is crucial for writing clean, efficient, and bug-free code. Whether you’re working with mutable or immutable objects, the way Python handles them under the hood can impact your program’s logic and performance. In this post, we’ll walk through key concepts such as object identity, mutability, immutability, and how Python treats these objects when passed to functions.

---

## ID and Type

Every object in Python has an **identity** (retrieved using `id()`) and a **type** (retrieved using `type()`). The `id()` function returns a unique identifier for the object (its memory address in CPython), and `type()` tells you what kind of object you're dealing with.

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(id(a))      # Unique ID (memory address) of a
print(id(b))      # Unique ID of b, different from a
print(type(a))    # Outputs: <class 'list'>
```
Output:

```python
139926795932424
139926795932672
<class 'list'>
```

Even though a and b have the same content, they are two distinct objects in memory.

🔁 Mutable Objects
Mutable objects can be changed after creation. Common examples:

list

dict

set

When you pass a mutable object to a function, any changes made inside the function affect the original object.

Example:
```python
def add_element(lst):
    lst.append(4)

my_list = [1, 2, 3]
add_element(my_list)
print(my_list)
```
Output:
```python
[1, 2, 3, 4]
```
The original list was modified in-place.

🔒 Immutable Objects
Immutable objects cannot be changed once created. Examples include:

int

str

tuple

Operations that “modify” immutable objects actually return new objects.

Example:

```python

a = 5
b = a
a += 1
print(a)
print(b)
```
Output:
```python
6
5
```
Modifying a does not affect b, because a new int object was created for a + 1.

📌 Why It Matters
Python handles mutable and immutable objects differently:

Immutable objects are hashable and can be used as keys in dictionaries.

Mutable objects are not hashable and cannot be used in sets or as dictionary keys.

```python
d = {}
d[(1, 2)] = "Tuple as key"
# d[[1, 2]] = "List as key"  # ❌ Raises TypeError: unhashable type: 'list'
```
Mutability also impacts memory efficiency, debugging, and code predictability.

🧪 Function Arguments & Object Behavior
In Python, arguments are passed by assignment (sometimes described as "pass-by-object-reference"). This means:

The reference to the object is passed.

Whether the function can modify the object depends on mutability.

🔁 Mutable example:
```python
def modify_list(lst):
    lst.append(10)

my_list = [1, 2, 3]
modify_list(my_list)
print(my_list)
```
Output:
```python
[1, 2, 3, 10]
```
The list is modified inside the function.

🔒 Immutable example:
```python
def modify_number(n):
    n += 5

x = 10
modify_number(x)
print(x)
```
Output:
```python
10
```
The number x is unchanged because integers are immutable. The n += 5 creates a new object, and the original x stays the same.

✅ Conclusion
Understanding the difference between mutable and immutable objects in Python helps you:

Avoid subtle bugs

Write predictable, maintainable code

Use functions more effectively

Make informed choices about data structures

Mastering how Python handles memory, identity, and object references is a major step in becoming a proficient Python developer.