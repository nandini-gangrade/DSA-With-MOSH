# 📌 **Queues - Detailed Notes**
## **1️⃣ Introduction to Queues**
### **What is a Queue?**
A **Queue** is a **linear data structure** that follows the **FIFO (First In, First Out) principle**.  
The element **inserted first** is the **first one to be removed**.

### **Applications of Queues**
- **Task Scheduling** (CPU scheduling, print job queue).
- **Data Transfer Buffers** (I/O buffers, network request queues).
- **Breadth-First Search (BFS) Algorithm**.
- **Handling Requests in Order** (customer service, ticket booking).

---

## **2️⃣ Queue Implementation in Java**
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

    public void enqueue(int item) {
        if (size == capacity) {
            System.out.println("Queue Overflow!");
            return;
        }
        arr[++rear] = item;
        size++;
    }

    public int dequeue() {
        if (size == 0) {
            System.out.println("Queue Underflow!");
            return -1;
        }
        int item = arr[front++];
        size--;
        return item;
    }

    public int peek() {
        return size == 0 ? -1 : arr[front];
    }

    public boolean isEmpty() {
        return size == 0;
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

**Complexity Analysis:**
| Operation | Array Queue | Linked List Queue |
|-----------|------------|------------------|
| Enqueue (`enqueue(x)`) | `O(1)` | `O(1)` |
| Dequeue (`dequeue()`) | `O(1)` | `O(1)` |
| Peek (`peek()`) | `O(1)` | `O(1)` |
| Space Complexity | `O(n)` | `O(n)` |

---

## **3️⃣ Circular Queue (Using Circular Arrays)**
A **circular queue** uses a **circular array** where the **last position connects to the first**, solving the **wasted space issue** in a normal queue.

#### ✅ **Implementation in Java**
```java
class CircularQueue {
    private int[] arr;
    private int front, rear, size, capacity;

    public CircularQueue(int capacity) {
        this.capacity = capacity;
        arr = new int[capacity];
        front = size = 0;
        rear = capacity - 1;
    }

    public void enqueue(int item) {
        if (size == capacity) {
            System.out.println("Queue is Full");
            return;
        }
        rear = (rear + 1) % capacity;
        arr[rear] = item;
        size++;
    }

    public int dequeue() {
        if (size == 0) {
            System.out.println("Queue is Empty");
            return -1;
        }
        int item = arr[front];
        front = (front + 1) % capacity;
        size--;
        return item;
    }

    public int peek() {
        return (size == 0) ? -1 : arr[front];
    }

    public boolean isEmpty() {
        return size == 0;
    }
}
```

---

## **4️⃣ Queue Using Two Stacks**
A **queue can be implemented using two stacks** (`stack1` for enqueue, `stack2` for dequeue).

#### ✅ **Implementation**
```java
import java.util.Stack;

class QueueUsingTwoStacks {
    private Stack<Integer> stack1 = new Stack<>();
    private Stack<Integer> stack2 = new Stack<>();

    public void enqueue(int x) {
        stack1.push(x);
    }

    public int dequeue() {
        if (stack2.isEmpty()) {
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }
        return stack2.isEmpty() ? -1 : stack2.pop();
    }

    public boolean isEmpty() {
        return stack1.isEmpty() && stack2.isEmpty();
    }
}
```

**Complexity Analysis:**
| Operation | Time Complexity |
|-----------|---------------|
| Enqueue (`enqueue(x)`) | `O(1)` |
| Dequeue (`dequeue()`) | `O(n)` (worst case) |

---

## **5️⃣ Priority Queue**
A **priority queue** is a queue where elements are **processed based on priority**, not FIFO.

### ✅ **Implementation Using Java's PriorityQueue**
```java
import java.util.PriorityQueue;

public class PriorityQueueExample {
    public static void main(String[] args) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        pq.add(10);
        pq.add(5);
        pq.add(20);

        System.out.println(pq.poll()); // Output: 5 (smallest element)
    }
}
```

**Complexity Analysis:**
| Operation | Time Complexity |
|-----------|---------------|
| Enqueue (`add(x)`) | `O(log n)` |
| Dequeue (`poll()`) | `O(log n)` |
| Peek (`peek()`) | `O(1)` |

---

## **6️⃣ Priority Queue Implementation Using Core Java**
```java
import java.util.Arrays;

class PriorityQueue {
    private int[] arr;
    private int size;

    public PriorityQueue(int capacity) {
        arr = new int[capacity];
        size = 0;
    }

    public void enqueue(int item) {
        arr[size++] = item;
        Arrays.sort(arr, 0, size);
    }

    public int dequeue() {
        return size == 0 ? -1 : arr[--size];
    }

    public int peek() {
        return size == 0 ? -1 : arr[size - 1];
    }
}
```

---

## **7️⃣ Exercises**
### **Exercise 1: Reverse the First K Elements in a Queue**
```java
import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;

public class QueueReverser {
    public static void reverse(Queue<Integer> queue, int k) {
        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < k; i++)
            stack.push(queue.poll());

        while (!stack.isEmpty())
            queue.add(stack.pop());

        for (int i = 0; i < queue.size() - k; i++)
            queue.add(queue.poll());
    }
}
```

---

## **8️⃣ Summary & Comparison**
| Operation | Array Queue | Linked List Queue | Circular Queue | Priority Queue |
|-----------|------------|------------------|---------------|---------------|
| Enqueue (`enqueue(x)`) | `O(1)` | `O(1)` | `O(1)` | `O(log n)` |
| Dequeue (`dequeue()`) | `O(1)` | `O(1)` | `O(1)` | `O(log n)` |
| Peek (`peek()`) | `O(1)` | `O(1)` | `O(1)` | `O(1)` |
| Space Complexity | `O(n)` | `O(n)` | `O(n)` | `O(n)` |
