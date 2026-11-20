# Task 3 – Constructors in derived and member classes

## Constructor and destructor order
For a derived object, virtual bases are constructed first (by the most-derived constructor), then direct non-virtual bases in base-list order, then member objects in their declaration order, then the derived constructor body. Destruction reverses this: derived destructor body, members in reverse declaration order, then base destructors in reverse base order.

`Person` owns an `Address` value member; `Student` owns a `Course` value member. The constructor initializer lists pass values to both base and member constructors.

## Complete the Code
`complete_code.cpp` completes TODO 1 with:
```cpp
: Person(n, a), regNo(r), home(c, p)
```
Expected output:
```text
192311001 Kavya (19) Salem-636001
```

## Alternative: Address pointer
Using `Address* home = new Address(...)` adds a heap allocation and pointer storage. The class must define ownership, allocate in the constructor, deep-copy in the copy constructor/assignment (or delete copying), and `delete home` in the destructor. A value member is simpler and automatically manages its lifetime.

## Required experiment
Swap initializer-list order while leaving member declarations unchanged. `-Wall -Wextra -Wreorder` may warn that actual initialisation follows declaration order, not list order. Record compiler version, warning and `sizeof` measurements after removing/adding virtual inheritance where applicable.
