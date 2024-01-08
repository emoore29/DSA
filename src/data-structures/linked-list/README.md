# Linked List

In computer science, a **linked list** is a linear collection
of data elements, in which linear order is not given by
their physical placement in memory. Instead, each
element points to the next. It is a data structure
consisting of a group of nodes which together represent
a sequence. Under the simplest form, each node is
composed of data and a reference (in other words,
a link) to the next node in the sequence.

This structure allows for efficient insertion or removal of elements
from any position in the sequence during iteration.
More complex variants add additional links, allowing
efficient insertion or removal from arbitrary element
references.

A drawback of linked lists is that access
time is linear (and difficult to pipeline).

Faster access, such as random access, is not feasible. Arrays
have better cache locality as compared to linked lists.

![Linked List](./images/linked-list.jpeg)

_Made with [okso.app](https://okso.app)_

- Can only start at the beginning and go down the list from node to node until you get to the one you want.
- Can update more easily than arrays because data doesn't need to be stored all together in physical memory. Arrays have a fixed size, so resizing them can be inefficient.
- In a linked list, adding or removing elements usually involves updating a few pointers, while in an array, these operations may require shifting a large number of elements.
- Do not require contiguous memory allocation, unlike arrays. This allows them to efficiently use scattered or fragmented memory space.

* Slower random access times (see point one) and increased memory overhead due to the storage of pointers.

## Pseudocode for Basic Operations

### Insert

```text
Add(value)
  Pre: value is the value to add to the list
  Post: value has been placed at the tail of the list
  n ← node(value)
  if head = ø
    head ← n // if there is no head, the head and tail become the new node
    tail ← n
  else
    tail.next ← n // updates the link between the old tail and the new one (points to new node)
    tail ← n // makes the tail the new node
  end if
end Add
```

```text
Prepend(value)
 Pre: value is the value to add to the list
 Post: value has been placed at the head of the list
 n ← node(value)
 n.next ← head // n.next links the new node to the current head.
 head ← n // then we assign n as the new head, and it points to the old head
 if tail = ø
   tail ← n // if there is only one value in the list, then n is also the tail
 end
end Prepend
```

### Search

```text
Contains(head, value) // head is the access point
  Pre: head is the head node in the list
       value is the value to search for
  Post: the item is either in the linked list, true; otherwise false
  n ← head
  while n != ø and n.value != value // if n is null, we've exited the list. each node is an object with the value and the "next" (pointer)
    n ← n.next // assigns n.next to n, each loop, until n = the value we're looking for or is null (we've reached the end of the list)
  end while
  if n = ø // if n = null, we've reached the end of the list without finding it, so we return false
    return false
  end if
  return true // if n is not null, then we've found the value in the list, so we return true
end Contains
```

### Delete

```text
Remove(head, value)
  Pre: head is the head node in the list
       value is the value to remove from the list
  Post: value is removed from the list, true, otherwise false
  if head = ø // nothing to remove, list is empty
    return false
  end if
  n ← head // assign n to the head
  if n.value = value
    if head = tail // remove both head and tail because there's just one value in the list and we want to delete it.
      head ← ø
      tail ← ø
    else
      head ← head.next // replace old head with the next value, which is basically deleting the old head.
    end if
    return true
  end if
  while n.next != ø and n.next.value != value // searching through list, checking the next value
    n ← n.next
  end while // we end the while loop when either n.next = null (return false) or n.next.value == the value we want to delete.
  if n.next != ø
    if n.next = tail
      tail ← n
      tail.next = null
    else
      n.next ← n.next.next
    end if
    return true
  end if
  return false
end Remove
```

### Traverse

```text
Traverse(head)
  Pre: head is the head node in the list
  Post: the items in the list have been traversed
  n ← head
  while n != ø
    yield n.value
    n ← n.next
  end while
end Traverse
```

### Traverse in Reverse

// A -> B -> C -> D
// We traverse a, b, c until we get to the value before the tail (C). Then we yield D. Then we assign current to prev (so C). Then we loop again, and go from a to B, which is before C. Then yield C. Then we assign current to prev (so B).Then loop again, going to A, which is before B. Then we yield B. Then we assign current to prev (so A). A = head, so we break out of the loop.

```text
ReverseTraversal(head, tail)
  Pre: head and tail belong to the same list
  Post: the items in the list have been traversed in reverse order
  if tail != ø
    curr ← tail
    while curr != head
      prev ← head
      while prev.next != curr
        prev ← prev.next
      end while
      yield curr.value
      curr ← prev
    end while
   yield curr.value
  end if
end ReverseTraversal
```

## Complexities

### Time Complexity

| Access | Search | Insertion | Deletion |
| :----: | :----: | :-------: | :------: |
|  O(n)  |  O(n)  |   O(1)    |   O(n)   |

### Space Complexity

O(n)

## References

- [Wikipedia](https://en.wikipedia.org/wiki/Linked_list)
- [YouTube](https://www.youtube.com/watch?v=njTh_OwMljA&index=2&t=1s&list=PLLXdhg_r2hKA7DPDsunoDZ-Z769jWn4R8)
