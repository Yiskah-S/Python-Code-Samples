| #   | Data Structure          | Access By Key | Search | Insertion (Middle) | Deletion (Middle) | Add First | Add Last |
| --- | ----------------------- | ------------- | ------ | ------------------ | ----------------- | --------- | -------- |
| 1   | Unsorted Array          | O(1)          | O(n)   | O(n)               | O(n)              | O(n)      | O(1)     |
| 2   | Sorted Array            | O(1)          | O(log n)| O(n)               | O(n)              | O(n)      | O(1)     |
| 3   | Doubly Linked List      | O(n)          | O(n)   | O(n)               | O(n)              | O(1)      | O(1)     |
| 4   | Binary Tree (balanced)  | O(log n)      | O(log n)| O(log n)           | O(log n)          | NA        | NA       |
| 5   | Binary Tree (unbalanced)| O(n)          | O(n)   | O(n)               | O(n)              | NA        | NA       |
| 6   | Hash Table*             | O(1)          | O(1)   | O(1)               | O(1)              | NA        | NA       |


Binary search trees have a non-linear structure. Whereas each node in a (singly) linked list maintains a pointer to one other node in a linked list, each node in a binary search tree has pointers to two other nodes in the data structure. We refer to these pointers as the child nodes of the original parent node. We label each of the parent node's two children as the left and right children or pointers. Collectively, we can refer to a parent node's children as siblings. The parent node can be thought of as similar to the prev pointer in a doubly linked list; however, unlike a linked list, tree nodes do not generally maintain a pointer to their parent/previous node.

A binary search tree's left and right child nodes are required to maintain special properties. The left child must have a key that is less than the key of its parent node. The right child must have a key that is greater than or equal to that of its parent node.

The topmost node in a tree is known as the root. The root has no parent node. Nodes with no children are called leaves.

```python
class TreeNode:
    def __init__(self, key, val = None):
        if val is None:
            val = key

        self.key = key
        self.value = val
        self.left = None
        self.right = None

class Tree:
    def __init__(self):
        self.root = None
    
    # iterative find
    def find(self, key):
        current = self.root
        while current:
            if key == current.key:
                return current.value
            elif key < current.key:
                current = current.left
            else:
                current = current.right
        return None

    # recursive find
    def find_helper(self, current, key):
        # base case - reached a leaf
        if not current:
            return None
        # base case - found what we are looking for
        elif key == current.key:
            return current.value
        # recursive case - key is less than current root's key
        elif key < current.key:
            # call find on left subtree
            return self.find_helper(current.left, key)
        # recursive case - key must be greater than current root's key
        # call find on right subtree
        return self.find_helper(current.right, key)

    def find(self, key):
        return self.find_helper(self.root, key)

    # iterative insert
    # def add(self, key, value = None):
    #     new_node = TreeNode(key, value)
    #     if not self.root:
    #         self.root = new_node
    #         return

    #     current = self.root
    #     while current:
    #         if key < current.key:
    #             if current.left is None:
    #                 current.left = new_node
    #                 return
    #             else:
    #                 current = current.left
    #         else:
    #             if current.right is None:
    #                 current.right = new_node
    #                 return
    #             else:
    #                 current = current.right

    # recursive insert
    def add(self, key, value=None):
        new_node = TreeNode(key, value)
        if not self.root:
            self.root = new_node
        else:
            self.add_helper(self.root, key, value)

    def add_helper(self, current_node, key, value):
        if key < current_node.key:
            if current_node.left is None:
                current_node.left = TreeNode(key, value)
            else:
                self.add_helper(current_node.left, key, value)
        else:
            if current_node.right is None:
                current_node.right = TreeNode(key, value)
            else:
                self.add_helper(current_node.right, key, value)

    def add(self, key, value=None):
        def add_recursive(current_node, key, value):
            if not current_node:
                return TreeNode(key, value)
            if key < current_node.key:
                current_node.left = add_recursive(current_node.left, key, value)
            else:
                current_node.right = add_recursive(current_node.right, key, value)
            return current_node

        self.root = add_recursive(self.root, key, value)


# helper function handles the recursion
    def add_helper(self, current_node, new_node):

        # if new node should be in left subtree (less than current node)
        if new_node.key < current_node.key: 
            # if current node is a leaf
            if not current_node.left:
                # make new node left child of current node
                current_node.left = new_node
                return
            # Otherwise, recurse through left subtree of current node
            self.add_helper(current_node.left, new_node)
        # if new node should be in right subtree 
        # (greater than or equal to current node)
        else:
            # if current node is a leaf
            if not current_node.right:
                # make new node right child of current node
                current_node.right = new_node
                return
            # Otherwise, recurse through right subtree of current node
            self.add_helper(current_node.right, new_node)

    def add(self, key, value = None):
        # If tree is empty
        if not self.root:
            # Make new node the root
            self.root = TreeNode(key, value)
        # Otherwise, initiate tree traversal by calling add on root
        else:
            new_node = TreeNode(key, value)
            self.add_helper(self.root, new_node)

    # recursive delete
    def delete(self, key):
        def delete_recursive(current_node, key):
            if not current_node:
                return None
            if key == current_node.key:
                # Case 1: No children
                if not current_node.left and not current_node.right:
                    return None
                # Case 2: Only 1 child
                if not current_node.left:
                    return current_node.right
                if not current_node.right:
                    return current_node.left
                # Case 3: 2 children
                # Find the minimum value in the right subtree
                # Replace current node's key and value with the successor's key and value
                # Delete the successor from the right subtree
                successor = self.find_min(current_node.right)
                current_node.key = successor.key
                current_node.value = successor.value
                current_node.right = delete_recursive(current_node.right, successor.key)
            elif key < current_node.key:
                current_node.left = delete_recursive(current_node.left, key)
            else:
                current_node.right = delete_recursive(current_node.right, key)
            return current_node

        self.root = delete_recursive(self.root, key)

    # # Helper function to find the minimum node in a tree
    # def min_node(self, root):
    #     # minimum node will be in last leaf in left subtree
    #     # traverse left subtree
    #     while root.left:
    #         # continue traversal, by replacing root with left subtree
    #         root = root.left
    #     # return the key and the value of minimum node
    #     return root.key, root.value

    # # Recursive helper function
    # def delete_helper(self, current_root, key):
    #     #if key is less than current node's
    #     if key < current_root.key:
    #         #call delete on left subtree
    #         current_root.left = self.delete_helper(current_root.left, key)
    #     #if key is greater than current node's
    #     elif key > current_root.key:
    #         #call delete on right subtree
    #         current_root.right = self.delete_helper(current_root.right, key)
    #     #if we found the node to delete
    #     else:
    #         #if node doesn't have a left subtree
    #         if not current_root.left:
    #             #return the right subtree
    #             return current_root.right
    #         #if node doesn't have a right subtree
    #         elif not current_root.right:
    #             # return right subtree
    #             return current_root.left
    #         # if node has both left and right subtrees
    #         # find the minimum node in the right subtree, and replace the deleted node with it
    #         current_root.key, current_root.value = self.min_node(current_root.right)
    #         # delete the minimum node in the right subtree
    #         current_root.right = self.delete_helper(current_root.right, current_root.key)
    #     # return the current node
    #     return current_root

    # def delete(self, key):
    #     # if the tree is empty
    #     if not self.root:
    #         # exit the function
    #         return

    #     # call our recursive helper on the root
    #     self.root = self.delete_helper(self.root, key)

    
```



Pre-order Pre-order traversal processes nodes in the order they were inserted. For this reason, if we need to save a tree data structure to disk, or send it across the network and maintain the structure, pre-order traversals can be useful.
In-Order: In-order traversal processes the left most node and end with the right most node; it processes nodes from smallest key to largest key. Thus, it is useful if we need to print or otherwise visit all the nodes of a tree in order.
Post-Order: Post-order traversal processes all of the root node's descendants before processing the root itself. Therefore post-order is useful if we need to delete all the nodes in a BST.


Generally depth first traversals are much more common with trees.

Pre-order Pre-order traversal processes nodes in the order they were inserted. For this reason, if we need to save a tree data structure to disk, or send it across the network and maintain the structure, pre-order traversals can be useful.
In-Order: In-order traversal processes the left most node and end with the right most node; it processes nodes from smallest key to largest key. Thus, it is useful if we need to print or otherwise visit all the nodes of a tree in order.
Post-Order: Post-order traversal processes all of the root node's descendants before processing the root itself. Therefore post-order is useful if we need to delete all the nodes in a BST.

Serialization Big O
Serialization algorithms are O(n) in both time and space complexity. Both breadth first search and depth first search algorithms visit each node in the array exactly once, giving O(n) time complexity where n is the number of nodes in the tree. They also both create an array to store each explored node giving O(n) space complexity.

If we were to just perform a traversal using either breadth first or depth first search without storing the explored nodes in an array or other auxiliary data structure, the space complexity would be slightly different.

With depth first search algorithms, we need to consider how many recursive calls would be on the call stack at any given time. The maximum number of recursive calls would be the height of the tree since depth first search algorithms go as deep as they can into the tree before turning back and exploring other subtrees. So we can say the space complexity is O(h) where h is the height of the tree.

With breadth first search, we need to consider the maximum number of nodes that would be in our queue at any given time. Since breadth first search adds all the nodes in a level to the queue before starting to pop them off, the space complexity would be O(b) where b is the breadth (the number of nodes on the level with the greatest number of nodes) of the tree.

https://learn-2.galvanize.com/cohorts/3646/blocks/1277/content_files/03-Binary-Search-Trees/03-Binary-Search-Trees-Traversal.md

![Binary Tree](/images/binary_tree.png)


For the above Binary Search Tree

Pre-Order: [50, 25, 10, 30, 75, 60, 100]
In-Order: [10, 25, 30, 50, 60, 75, 100]
Post-Order: [10, 30, 25, 60, 100, 75, 50]


![In-order](/images/in_order.png)


```python
from collections import deque

class TreeNode:

    def __init__(self, key, value=None, left=None, right=None):
        if not value:
            value = key
        self.key = key
        self.val = value
        self.left = left
        self.right = right

    def __repr__(self):
        return f"TreeNode {self.val}"


class Tree:

    def __init__(self):
        self.root = None
    
    # Breadth First Search
    def bfs(self):
        if not self.root:
            return []
        
        queue = deque()
        result = []
        
        queue.append(self.root)
        
        while queue:
            current_node = queue.popleft()
            result.append(current_node.val)
            
            if current_node.left:
                queue.append(current_node.left)
            if current_node.right:
                queue.append(current_node.right)
        return result
```
Preorder Traversal
```python
# recursive helper
    def preorder_helper(self, current_node, values):
        # if the tree is empty
        if not current_node:
            # return the list of values
            return values

        # Append current node to list of values
        values.append(current_node.val)
        # call helper function on the left child
        self.preorder_helper(current_node.left, values)     
        # call helper function on the right child   
        self.preorder_helper(current_node.right, values)

        return values

    def preorder(self):
        # create an empty list to hold the node's values
        values = []
        # call helper function on root
        return self.preorder_helper(self.root, values)
```
Inorder Traversal
```python
    # recursive helper
    def inorder_helper(self, current_node, values):
        # if the tree is empty
        if not current_node:
            # return the list of values
            return values

        # call helper function on the left child
        self.inorder_helper(current_node.left, values)
        # Append current node to list of values
        values.append(current_node.val)     
        # call helper function on the right child   
        self.inorder_helper(current_node.right, values)

        return values

    def inorder(self):
        # create an empty list to hold the node's values
        values = []
        # call helper function on root
        return self.inorder_helper(self.root, values)
```

Postorder Traversal
```python

    # recursive helper
    def postorder_helper(self, current_node, values):
        # if the tree is empty
        if not current_node:
            # return the list of values
            return values

        # call helper function on the left child
        self.postorder_helper(current_node.left, values)     
        # call helper function on the right child   
        self.postorder_helper(current_node.right, values)
        # Append current node to list of values
        values.append(current_node.val)

        return values

    def postorder(self):
        # create an empty list to hold the node's values
        values = []
        # call helper function on root
        return self.postorder_helper(self.root, values)
```

```python
class TreeNode:
    def __init__(self, key, val = None):
        if val == None:
            val = key

        self.key = key
        self.value = val
        self.left = None
        self.right = None

class Tree:
    def __init__(self):
        self.root = None
    

    def height(self):
        def height_helper(current_node):
            if not current_node:
                return 0
            left_height = height_helper(current_node.left)
            right_height = height_helper(current_node.right)
            return max(left_height, right_height) + 1

        return height_helper(self.root)


    # def height_helper(self, current_node):
    #     if not current_node:
    #         return 0

    #     return max(self.height_helper(current_node.left), self.height_helper(current_node.right)) + 1
    
    # def height(self):
    #     return self.height_helper(self.root)
```

```python


https://adaacademy.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=ceac4982-192f-44a7-88a8-ad91016c972b
https://docs.google.com/presentation/d/1M1tDoYMERJKwHBOp8LEmGDLwpg1kDqtGEpsGgrvPoIU/edit?usp=sharing
https://adaacademy.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=d9746397-8a10-43be-b1cc-aaaf00720b31
https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-006-introduction-to-algorithms-fall-2011/lecture-videos/lecture-5-binary-search-trees-bst-sort/
https://www.freecodecamp.org/news/binary-tree-algorithms-for-javascript-beginners/
https://www.geeksforgeeks.org/self-balancing-binary-search-trees-comparisons/
https://blog.devgenius.io/dfs-depth-first-search-traversal-techniques-short-and-sweet-1e4c134babcf