# 📌 **Queues**
## **1️⃣ Introduction to Queues**
### **What is a Queue?**
- A **Queue** is a **linear data structure** that follows the **FIFO (First In, First Out) principle**.
- This means the **first element added** is the **first one to be removed**.
- It works just like a queue in a bank – the first person in line is served first.

### **Why use a Queue?**
Queues are useful in scenarios where **order matters** and we need:
- **Task Scheduling** (e.g., CPU scheduling, print job queue).
- **Data Transfer Buffers** (e.g., I/O buffers, network request queues).
- **Breadth-First Search (BFS) Algorithm**.
- **Handling Requests in Order** (e.g., customer service systems).

---

## **2️⃣ Queue in Java**
Queues in Java can be implemented using:
1. **Arrays** (Fixed size, efficient but rigid).
2. **Linked List** (Dynamic size, efficient but uses extra memory).
3. **Java Collections Framework (`Queue<E>`)**.

---

## **3️⃣ Working of a Queue**
A queue supports **five primary operations**:
1. **enqueue(x)** → Adds an element `x` to the end of the queue.
2. **dequeue()** → Removes and returns the front element.
3. **peek()** → Returns the front element without removing it.
4. **isEmpty()** → Checks if the queue is empty.
5. **size()** → Returns the number of elements in the queue.

---

## **4️⃣ Implementing a Queue in Java**
### ✅ **(A) Queue Using an Array**
```java
class Queue {
    private int[] arr;
    private int front, rear, size, capacity;

    public Queue(int capacity) {
        this.capacity = capacity;
        arr = new int[capacity];
        front = size = 0;
        rear = -1;
    }

    // Enqueue operation
    public void enqueue(int item) {
        if (size == capacity) {
            System.out.println("Queue Overflow!");
            return;
        }
        arr[++rear] = item;
        size++;
    }

    // Dequeue operation
    public int dequeue() {
        if (size == 0) {
            System.out.println("Queue Underflow!");
            return -1;
        }
        int item = arr[front++];
        size--;
        return item;
    }

    // Peek at the front element
    public int peek() {
        return size == 0 ? -1 : arr[front];
    }

    // Check if queue is empty
    public boolean isEmpty() {
        return size == 0;
    }

    public static void main(String[] args) {
        Queue queue = new Queue(5);
        queue.enqueue(10);
        queue.enqueue(20);
        System.out.println(queue.dequeue()); // Output: 10
    }
}
```
### ✅ **(B) Queue Using Java Collections (`Queue<E>`)**
```java
import java.util.LinkedList;
import java.util.Queue;

public class QueueExample {
    public static void main(String[] args) {
        Queue<Integer> queue = new LinkedList<>();
        queue.add(10);
        queue.add(20);

        System.out.println(queue.poll()); // Output: 10
        System.out.println(queue.peek()); // Output: 20
    }
}
```
**Comparison:**
| Approach | Advantages | Disadvantages |
|----------|------------|--------------|
| **Array-based** | Faster access (`O(1)`) | Fixed size, not dynamic |
| **Collections-based** | Dynamic, built-in methods | Slightly slower due to overhead |

---

## **5️⃣ Queue Exercises**
### **Exercise 1: Reverse the First K Elements in a Queue**
#### 📌 **Problem Statement**
Reverse the order of the **first K elements** in a queue.

#### ✅ **Solution**
```java
import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;

public class QueueReverser {
    public static void reverse(Queue<Integer> queue, int k) {
        Stack<Integer> stack = new Stack<>();

        // Step 1: Push first K elements into the stack
        for (int i = 0; i < k; i++)
            stack.push(queue.poll());

        // Step 2: Enqueue elements back from the stack
        while (!stack.isEmpty())
            queue.add(stack.pop());

        // Step 3: Move remaining elements to the end
        for (int i = 0; i < queue.size() - k; i++)
            queue.add(queue.poll());
    }

    public static void main(String[] args) {
        Queue<Integer> queue = new LinkedList<>();
        queue.add(10);
        queue.add(20);
        queue.add(30);
        queue.add(40);
        queue.add(50);

        reverse(queue, 3);

        System.out.println(queue); // Output: [30, 20, 10, 40, 50]
    }
}
```

---

### **Exercise 2: Queue Using Linked List**
#### 📌 **Problem Statement**
Implement a queue using a linked list.

#### ✅ **Solution**
```java
class Node {
    int data;
    Node next;

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class LinkedListQueue {
    private Node front, rear;
    private int size;

    public LinkedListQueue() {
        this.front = this.rear = null;
        this.size = 0;
    }

    public void enqueue(int item) {
        Node newNode = new Node(item);
        if (rear == null) {
            front = rear = newNode;
        } else {
            rear.next = newNode;
            rear = newNode;
        }
        size++;
    }

    public int dequeue() {
        if (front == null) return -1;
        int item = front.data;
        front = front.next;
        if (front == null) rear = null;
        size--;
        return item;
    }

    public int peek() {
        return front == null ? -1 : front.data;
    }

    public boolean isEmpty() {
        return size == 0;
    }
}
```

---

### **Exercise 3: Stack Using Two Queues**
#### 📌 **Problem Statement**
Implement a **Stack using two Queues**.

#### ✅ **Solution**
```java
import java.util.LinkedList;
import java.util.Queue;

class StackWithTwoQueues {
    private Queue<Integer> queue1 = new LinkedList<>();
    private Queue<Integer> queue2 = new LinkedList<>();

    public void push(int x) {
        queue1.add(x);
    }

    public int pop() {
        if (queue1.isEmpty()) return -1;

        // Move all elements except last to queue2
        while (queue1.size() > 1) {
            queue2.add(queue1.poll());
        }

        int popped = queue1.poll();

        // Swap the queues
        Queue<Integer> temp = queue1;
        queue1 = queue2;
        queue2 = temp;

        return popped;
    }

    public int peek() {
        if (queue1.isEmpty()) return -1;
        for (int i = 0; i < queue1.size() - 1; i++) {
            queue2.add(queue1.poll());
        }
        int top = queue1.peek();
        queue2.add(queue1.poll());

        Queue<Integer> temp = queue1;
        queue1 = queue2;
        queue2 = temp;

        return top;
    }

    public boolean isEmpty() {
        return queue1.isEmpty();
    }
}
```

---

## **6️⃣ Summary & Cheat Sheet**
| Operation | Normal Queue | Circular Queue | Priority Queue |
|-----------|-------------|---------------|---------------|
| `enqueue()` | `O(1)` | `O(1)` | `O(log n)` |
| `dequeue()` | `O(1)` | `O(1)` | `O(log n)` |
| `peek()` | `O(1)` | `O(1)` | `O(1)` |
| `isEmpty()` | `O(1)` | `O(1)` | `O(1)` |
