# **Exercises with In-Depth Explanation**

<br>

## **1️⃣ Find the Middle of a Linked List in One Pass**
**Problem Statement:**  
Given a singly linked list, find the middle element of the list in one pass. If the list has an even number of nodes, return both middle elements.

### **Key Observations**
1. **Using Two Pointers (Slow and Fast):**  
   - The slow pointer moves **one step** at a time.
   - The fast pointer moves **two steps** at a time.
   - When the fast pointer reaches the end, the slow pointer will be at the middle.

2. **How It Works for Odd-Length Lists:**  
   - Example: **1 → 2 → 3 → 4 → 5**
   - Initial: slow = 1, fast = 1  
   - Step 1: slow = 2, fast = 3  
   - Step 2: slow = 3, fast = 5  
   - Step 3: fast reaches the end; **slow is at 3 (middle node)**.

3. **How It Works for Even-Length Lists:**  
   - Example: **1 → 2 → 3 → 4 → 5 → 6**
   - Initial: slow = 1, fast = 1  
   - Step 1: slow = 2, fast = 3  
   - Step 2: slow = 3, fast = 5  
   - Step 3: slow = 4, fast reaches the last node (6).  
   - Since the fast pointer reaches the **last node**, return **two middle nodes (3,4)**.


### **Code Implementation in Java**
```java
class Node {
    int value;
    Node next;
    
    Node(int value) {
        this.value = value;
        this.next = null;
    }
}

class LinkedList {
    Node head;

    public void printMiddle() {
        if (head == null) {
            throw new IllegalStateException("List is empty!");
        }

        Node slow = head;
        Node fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        // If the list has an even number of elements, return both middle nodes.
        if (fast == null) {
            System.out.println("Middle Nodes: " + slow.value + ", " + slow.next.value);
        } else {
            System.out.println("Middle Node: " + slow.value);
        }
    }

    public void append(int value) {
        if (head == null) {
            head = new Node(value);
            return;
        }
        Node current = head;
        while (current.next != null) {
            current = current.next;
        }
        current.next = new Node(value);
    }
}

// Test the function
public class Main {
    public static void main(String[] args) {
        LinkedList list = new LinkedList();
        list.append(1);
        list.append(2);
        list.append(3);
        list.append(4);
        list.append(5);
        list.printMiddle(); // Output: Middle Node: 3

        LinkedList list2 = new LinkedList();
        list2.append(1);
        list2.append(2);
        list2.append(3);
        list2.append(4);
        list2.append(5);
        list2.append(6);
        list2.printMiddle(); // Output: Middle Nodes: 3, 4
    }
}
```

### **Time & Space Complexity**
- **Time Complexity:** \(O(N)\) (Single pass)
- **Space Complexity:** \(O(1)\) (Only two pointers used)

---

## **2️⃣ Check If a Linked List Has a Loop**
**Problem Statement:**  
Detect if a given linked list has a loop (cycle).

### **Key Observations**
1. **Using Floyd’s Cycle Detection Algorithm (Tortoise & Hare Method)**  
   - Use two pointers:  
     - **Slow pointer** moves **one step** at a time.
     - **Fast pointer** moves **two steps** at a time.
   - If the fast pointer **meets** the slow pointer at some point, there is a loop.

2. **How It Works?**
   - Example:
     ```
     1 → 2 → 3 → 4 → 5
               ↑      ↓
               7 ← 6
     ```
   - Initially, slow = 1, fast = 1  
   - Step 1: slow = 2, fast = 3  
   - Step 2: slow = 3, fast = 5  
   - Step 3: slow = 4, fast = 7  
   - Step 4: slow = 5, fast = 4  
   - Step 5: slow = 6, fast = 6 (MEETING POINT → CYCLE DETECTED)



### **Code Implementation in Java**
```java
class LinkedList {
    Node head;

    public boolean hasLoop() {
        Node slow = head;
        Node fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;

            if (slow == fast) { // If they meet, there is a loop
                return true;
            }
        }
        return false;
    }

    public void append(int value) {
        if (head == null) {
            head = new Node(value);
            return;
        }
        Node current = head;
        while (current.next != null) {
            current = current.next;
        }
        current.next = new Node(value);
    }

    // Helper function to create a loop for testing
    public void createLoop(int pos) {
        Node temp = head;
        Node loopNode = null;
        int count = 0;

        while (temp.next != null) {
            if (count == pos) {
                loopNode = temp;
            }
            temp = temp.next;
            count++;
        }
        temp.next = loopNode; // Creating a loop
    }
}

// Test the function
public class Main {
    public static void main(String[] args) {
        LinkedList list = new LinkedList();
        list.append(1);
        list.append(2);
        list.append(3);
        list.append(4);
        list.append(5);
        list.append(6);

        list.createLoop(2); // Creating a loop at node 3

        System.out.println(list.hasLoop()); // Output: true

        LinkedList list2 = new LinkedList();
        list2.append(1);
        list2.append(2);
        list2.append(3);
        System.out.println(list2.hasLoop()); // Output: false
    }
}
```

### **Time & Space Complexity**
- **Time Complexity:** \(O(N)\) (Traverses each node once)
- **Space Complexity:** \(O(1)\) (Only two pointers used)

---

### **Conclusion**
✅ **Find the Middle of a Linked List:**  
- Used **slow and fast pointers** to find the middle node in **one pass**.
- If the list has an even number of elements, return **two middle nodes**.

✅ **Detect a Loop in a Linked List:**  
- Used **Floyd’s Cycle Detection Algorithm (Tortoise & Hare)**.
- If **slow** and **fast** pointers meet, a loop is present.
