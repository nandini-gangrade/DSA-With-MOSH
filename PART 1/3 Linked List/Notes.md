# 📌 **Linked Lists**

## 1️⃣ **Introduction to Linked Lists**

### 🔹 What are Linked Lists?  
A **Linked List** is a **linear data structure** where elements (nodes) are connected through pointers instead of contiguous memory locations like an array.  
Each node in a linked list contains:  
1. **Data** - The actual value stored in the node.  
2. **Pointer** (Reference) - A link to the next node in the list.

A **Singly Linked List** has a pointer to the next node.  
A **Doubly Linked List** has two pointers (next and previous).  
A **Circular Linked List** connects back to the head.

### 🔹 Why do we need Linked Lists?  
- Arrays have a **fixed size** (static memory allocation).  
- **Insertion & Deletion in Arrays is costly** (O(N) shifting required).  
- Linked Lists provide **dynamic memory allocation** (grows as needed).  
- Inserting and deleting elements in a Linked List is **efficient** (O(1) at the start).  

### 🔹 How Linked Lists Work Internally? (Node Structure)  
A **Node** in a singly linked list looks like this:

```java
class Node {
    int data;   // Stores data
    Node next;  // Pointer to the next node

    public Node(int data) {
        this.data = data;
        this.next = null; // Initially, next is null
    }
}
```

### 🔹 Visual Representation of a Singly Linked List  
Example: A Linked List with values **10 → 20 → 30 → 40**  

```
[10 | * ] --> [20 | * ] --> [30 | * ] --> [40 | null]
```
Here, `*` represents a pointer to the next node, and `null` represents the end of the list.

---

## 2️⃣ **Understanding Linked Lists**  

### 🔹 **Types of Linked Lists**  

#### 📌 **Singly Linked List**  
- Each node has **data** and a **next** pointer.  
- Traversal is **one-way** (only forward).  
- **Efficient for insertion and deletion** at the head.

#### 📌 **Doubly Linked List**  
- Each node has **data, next, and previous pointers**.  
- Traversal is **bidirectional** (forward and backward).  
- Requires **extra memory** for storing the previous pointer.  

#### 📌 **Circular Linked List**  
- The **last node** points back to the first node.  
- Can be **Singly or Doubly Linked**.  
- Used in scheduling applications (e.g., CPU scheduling).  

### 🔹 **Use Cases and Advantages/Disadvantages**  
| Feature | Singly LL | Doubly LL | Circular LL |
|---------|----------|----------|------------|
| Memory Usage | Low | High | Medium |
| Traversal | One-way | Two-way | Circular |
| Deletion at Tail | O(N) | O(1) | O(1) |
| Applications | Stacks, Queues | Undo Operations | CPU Scheduling |

---

## 3️⃣ **Working with Linked Lists (Operations with Code)**  

### 📌 **Creating a Linked List (LinkedList Class)**  

```java
class LinkedList {
    private Node head; // Head of the list

    private class Node {
        int data;
        Node next;

        public Node(int data) {
            this.data = data;
            this.next = null;
        }
    }
}
```

---

### 📌 **Adding Elements**  

#### **1️⃣ Adding a Node at the End (`addLast()`)**  

```java
public void addLast(int data) {
    Node newNode = new Node(data);
    if (head == null) {
        head = newNode; // If list is empty, set newNode as head
        return;
    }

    Node current = head;
    while (current.next != null) {
        current = current.next; // Traverse to the last node
    }
    current.next = newNode; // Set the last node's next to newNode
}
```

✅ **Time Complexity**: **O(N)** (Traversing till last node)  
✅ **Example Usage & Output**:  

```java
LinkedList list = new LinkedList();
list.addLast(10);
list.addLast(20);
list.addLast(30);
```

```
Output: 10 → 20 → 30
```

---

#### **2️⃣ Adding a Node at the Beginning (`addFirst()`)**  

```java
public void addFirst(int data) {
    Node newNode = new Node(data);
    newNode.next = head; // New node points to current head
    head = newNode; // Update head to new node
}
```

✅ **Time Complexity**: **O(1)** (Constant time insertion)  
✅ **Example Usage & Output**:  

```java
list.addFirst(5);
```

```
Output: 5 → 10 → 20 → 30
```

---

### 📌 **Searching Elements**  

#### **3️⃣ Get Index of a Value (`indexOf()`)**  

```java
public int indexOf(int value) {
    Node current = head;
    int index = 0;
    
    while (current != null) {
        if (current.data == value) return index;
        current = current.next;
        index++;
    }
    return -1; // If value not found
}
```

✅ **Time Complexity**: **O(N)**  
✅ **Example Usage & Output**:  

```java
System.out.println(list.indexOf(20));
```

```
Output: 2
```

---

### 📌 **Removing Elements**  

#### **4️⃣ Remove First Node (`removeFirst()`)**  

```java
public void removeFirst() {
    if (head == null) return;
    head = head.next; // Move head pointer to the next node
}
```

✅ **Time Complexity**: **O(1)**  

#### **5️⃣ Remove Last Node (`removeLast()`)**  

```java
public void removeLast() {
    if (head == null) return;
    if (head.next == null) { 
        head = null;
        return;
    }

    Node current = head;
    while (current.next.next != null) {
        current = current.next; // Traverse to second last node
    }
    current.next = null; // Remove last node
}
```

✅ **Time Complexity**: **O(N)**  

---

You're absolutely right! Here is the **complete** version of the notes, covering all the **Advanced Topics & Exercises**, **Comparison of Linked Lists vs. Arrays**, and **Summary & Cheat Sheets** in depth.  

---

# 📌 **Linked Lists - Complete Notes with Explanation & Code**  

---

## 4️⃣ **Advanced Topics & Exercises**  

### 🔹 **Reversing a Linked List (`reverse()`)**  
Reversing a Linked List means modifying the links between the nodes so that the **last node becomes the first**, and the **first node becomes the last**.  

#### ✅ **Algorithm:**
1. Maintain **three pointers**: `prev`, `current`, and `next`.  
2. Traverse the list while **reversing the `next` pointers**.  
3. Update the `head` to point to the last node.  

#### ✅ **Code Implementation:**
```java
public void reverse() {
    Node prev = null, current = head, next = null;

    while (current != null) {
        next = current.next;  // Store the next node
        current.next = prev;  // Reverse the link
        prev = current;       // Move prev forward
        current = next;       // Move current forward
    }
    head = prev;  // Update head to the last node
}
```

#### ✅ **Time Complexity:** **O(N)** (as we visit each node once)  
#### ✅ **Example Usage & Output:**
```java
LinkedList list = new LinkedList();
list.addLast(10);
list.addLast(20);
list.addLast(30);
list.reverse();
```
```
Output: 30 → 20 → 10
```

---

### 🔹 **Finding Kth Node from the End (`getKthFromEnd(k)`)**  
We find the **k-th node from the end** using **two pointers**:
1. Move **first pointer** `k` steps ahead.
2. Move **second pointer** along with the first pointer.
3. When the first pointer reaches the end, the second pointer is at the `k-th` node from the end.

#### ✅ **Code Implementation:**
```java
public int getKthFromEnd(int k) {
    Node first = head, second = head;
    
    // Move first k steps ahead
    for (int i = 0; i < k; i++) {
        if (first == null) return -1; // If k is greater than list size
        first = first.next;
    }

    // Move both pointers until first reaches the end
    while (first != null) {
        first = first.next;
        second = second.next;
    }
    
    return second.data;
}
```

#### ✅ **Time Complexity:** **O(N)**  
#### ✅ **Example Usage & Output:**
```java
System.out.println(list.getKthFromEnd(2));
```
```
Output: 20
```

---

### 🔹 **Detecting a Loop (`hasLoop()`) - Using Floyd’s Cycle Detection**  
A loop in a Linked List means that a node’s `next` pointer connects back to a **previous** node, forming a cycle.  
To detect a loop, we use **Floyd’s Cycle Detection Algorithm** (Two-pointer technique).  

#### ✅ **Algorithm:**
1. Use **two pointers**: `slow` (moves one step) and `fast` (moves two steps).  
2. If they ever **meet**, a loop exists.  
3. If `fast` reaches `null`, there is **no loop**.  

#### ✅ **Code Implementation:**
```java
public boolean hasLoop() {
    Node slow = head, fast = head;
    
    while (fast != null && fast.next != null) {
        slow = slow.next;       // Move slow one step
        fast = fast.next.next;  // Move fast two steps
        
        if (slow == fast) return true; // Loop detected
    }
    return false;
}
```

#### ✅ **Time Complexity:** **O(N)**  
#### ✅ **Example Usage & Output:**
```java
System.out.println(list.hasLoop());
```
```
Output: false (if no loop)
```

---

### 🔹 **Finding the Middle Node (`printMiddle()`)**  
To find the **middle node**, we use **two pointers**:  
1. **Slow pointer** moves one step at a time.  
2. **Fast pointer** moves two steps at a time.  
3. When `fast` reaches the end, `slow` is at the middle.  

#### ✅ **Code Implementation:**
```java
public void printMiddle() {
    Node slow = head, fast = head;
    
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    
    System.out.println("Middle Node: " + slow.data);
}
```

#### ✅ **Time Complexity:** **O(N)**  
#### ✅ **Example Usage & Output:**
```java
list.printMiddle();
```
```
Output: Middle Node: 20
```

---

## 5️⃣ **Comparison: Linked Lists vs. Arrays**  

### 🔹 **When to Use Which?**

| Feature | Arrays | Linked Lists |
|---------|--------|-------------|
| Memory Allocation | Fixed (Static) | Dynamic (Grows as needed) |
| Access Time | O(1) (Direct Indexing) | O(N) (Sequential Access) |
| Insertion/Deletion | O(N) (Shifting Needed) | O(1) (At Head) |
| Extra Memory | No Extra Pointers | Requires Extra Memory for Pointers |
| Data Storage | Contiguous Blocks | Non-contiguous Nodes |

| Feature | Arrays | Linked Lists |
|---------|--------|-------------|
| **Memory Allocation** | Fixed (Contiguous) | Dynamic (Non-Contiguous) |
| **Access Time** | O(1) (Direct Indexing) | O(N) (Sequential) |
| **Insertion/Deletion** | O(N) (Shifting Needed) | O(1) (At Head) |
| **Extra Memory** | No Extra Pointers | Requires Extra Memory for Pointers |
| **Traversal** | Forward only | Forward & Backward (Doubly LL) |
| **Sorting** | Easy | Harder |

### 🔹 **Pros & Cons**  
✅ **Linked Lists are better for:**
- **Dynamic memory allocation** (no fixed size).  
- **Frequent insertions and deletions** (O(1) at head).  

❌ **Arrays are better for:**
- **Fast access** (O(1) direct indexing).  
- **Better cache locality** (continuous memory allocation).  

---

## 6️⃣ **Summary & Cheat Sheet**  

### ✅ **Key Operations and Their Complexities**  
| Operation | Singly Linked List |
|-----------|-------------------|
| **Insert at Head (`addFirst`)** | O(1) |
| **Insert at Tail (`addLast`)** | O(N) |
| **Remove Head (`removeFirst`)** | O(1) |
| **Remove Tail (`removeLast`)** | O(N) |
| **Search (`indexOf`)** | O(N) |
| **Reverse (`reverse`)** | O(N) |
| **Find Middle (`printMiddle`)** | O(N) |
| **Find Kth from End (`getKthFromEnd`)** | O(N) |
| **Detect Loop (`hasLoop`)** | O(N) |

---

### ✅ **Quick Recap**
1. **Linked List is a dynamic data structure** where nodes are linked via pointers.  
2. **Three types:** **Singly, Doubly, Circular** Linked List.  
3. **Key operations:** Insertion, Deletion, Searching, Reversal, Loop Detection.  
4. **Arrays vs. Linked Lists:** Choose based on access time vs. insertion efficiency.  
5. **Common interview problems:**  
   - Reverse a Linked List  
   - Find K-th Node from End  
   - Detect a Loop in a Linked List  

---

## 🎯 **Final Notes**
- **Use Linked Lists when** you need **efficient insertions/deletions**.  
- **Use Arrays when** you need **fast random access**.  
- **Master key Linked List algorithms** (Reversal, Middle Node, Cycle Detection) for **coding interviews**.
