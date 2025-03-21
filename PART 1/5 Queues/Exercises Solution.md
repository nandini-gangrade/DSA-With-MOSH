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
