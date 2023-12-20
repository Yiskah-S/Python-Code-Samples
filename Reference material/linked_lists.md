| Big-O For Linked Lists & Arrays | Data Structure      | Access | Search | Insertion (Middle) | Deletion (Middle) | Add First | Add Last | Delete First | Delete Last |
|---------------------------------|---------------------|--------|--------|--------------------|-------------------|-----------|----------|--------------|-------------|
| 1                               | Unsorted Array      | O(1)   | O(n)   | O(n)               | O(n)              | O(n)      | O(1)     | O(1)         | O(n)        |
| 2                               | Sorted Array        | O(1)   | O(log n)| O(n)               | O(n)              | O(n)      | O(1)     | O(1)         | O(n)        |
| 3                               | Singly Linked List | O(n)   | O(n)   | O(n)               | O(n)              | O(1)      | O(n)     | O(1)         | O(n)        |
| 4                               | Doubly Linked List | O(n)   | O(n)   | O(n)               | O(n)              | O(1)      | O(1)     | O(1)         | O(1)        |


Python premade linked lists: https://www.geeksforgeeks.org/python-library-for-linked-list/

```python
class Node:
    def __init__(self, value):
        self.val = value
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
    
    def add_first(self, value):
        new_node = Node(value)
        new_node.next = self.head
        self.head = new_node

    def get_first(self):
        if self.head:
            return self.head.val
        else:
            return None

    def get_at_index(self, index):
        if index < 0:
            return None
        
        current = self.head
        current_index = 0
        
        while current:
            if current_index == index:
                return current.val
            current = current.next
            current_index += 1
        return None

    # def get_at_index(self, index):
    #     if index < 0:
    #         return None
        
    #     current = self.head
    #     current_index = 0
        
    #     while current:
    #         if current_index == index:
    #             return current.val
    #         current = current.next
    #         current_index += 1
    #     return None

    # def get_at_index(self, index):
    #     current_index = 0
    #     current = self.head

    #     while current_index < index and current:
    #         current_index += 1
    #         current = current.next

    #     if current_index == index and current:
    #         return current.val
    #     return None

    def add_last(self, value):
        if not self.head:
            self.add_first(value)
        else:
            new_node = Node(value)
            current = self.head
            while current.next:
                current = current.next
            current.next = new_node
            self.tail = new_node 

    def add_last(self, value):
        if not self.head:
            self.add_first(value)
        else:
            new_node = Node(value)
            new_node.prev = self.tail
            self.tail.next = new_node
            self.tail = new_node

    def remove(self, index):
        if not self.head:
            return 

        if index == 0:
            self.head = self.head.next
            return

        current = self.head
        current_index = 0
        while current.next and current_index < index - 1:
            current = current.next
            current_index += 1

        if current.next:
            current.next = current.next.next
```

```python
class Node:
    def __init__(self, value):
        self.val = value
        self.next = None
        self.prev = None

class LinkedList:
    def __init__(self):
        self.head = None
        self.tail = None
    
    def add_first(self, value):
        new_node = Node(value)
        new_node.next = self.head
        if self.head:
            self.head.prev = new_node
        self.head = new_node

    def get_first(self):
        if self.head:
            return self.head.val
        else:
            return None

    def get_at_index(self, index):
        if index < 0:
            return None
        
        current = self.head
        current_index = 0
        
        while current:
            if current_index == index:
                return current.val
            current = current.next
            current_index += 1
        return None

    def add_last(self, value):
        if not self.head:
            self.add_first(value)
        else:
            new_node = Node(value)
            new_node.prev = self.tail
            self.tail.next = new_node
            self.tail = new_node

    def remove(self, index):
        if not self.head:
            return 

        if index == 0:
            self.head = self.head.next
            if self.head:
                self.head.prev = None
            return

        current = self.head
        current_index = 0
        while current.next and current_index < index - 1:
            current = current.next
            current_index += 1

        if current.next:
            current.next = current.next.next
            if current.next:
                current.next.prev = current

```

Stacks
A stack is a data structure which stores a list of data and only provides access in a Last-In-First-Out (LIFO) order. 

A stack provides the following methods:

push(item) - This method adds an item to the top of the stack.
pop - This method removes and returns the item on the top of the stack.
is_empty - This method returns true if the stack is empty and false otherwise.
A stack might also implement a peek method which returns, but does not remove the item on top of the stack, and a size method which returns the number of items currently on the stack.


```python
class Stack:
  
    def __init__(self):
        self.store = LinkedList()

    def push(self, item):
        self.store.add_first(item)

    def pop(self):
      return self.store.remove_first()

    def is_empty(self):
        return self.store.length() == 0
```

Queues
A queue unlike a stack operates in a First-In-First-Out (FIFO) order. Like a line of people at a concert, the first element to enter the queue is the first element removed.

A Queue provides the following methods:

enqueue(item) - This method puts an item into the back of the queue.
dequeue - This method removes and returns the item at the front of the queue.
is_empty - This method returns true if the queue is empty and false otherwise.

```python
class Queue:
    def __init__(self):
        self.store = LinkedList()

    def enqueue(self, item):
        self.store.add_last(item)

    def dequeue(self):
        if self.is_empty():
            return None

        self.store.remove_first()

    def is_empty(self):
        return self.store.length() == 0
```