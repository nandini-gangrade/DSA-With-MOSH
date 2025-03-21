# 📌 **Stacks**
## **1️⃣ Introduction to Stacks**
### **What is a Stack?**
- A **Stack** is a **linear data structure** that follows the **LIFO (Last In, First Out) principle**.
- This means the last element inserted is the **first one to be removed**.
- It works just like a stack of plates – you can only remove the topmost plate first before accessing the ones below.

### **Why use a Stack?**
Stacks are used when **order matters** and we need:
- **Undo/Redo functionality** (e.g., text editors, browser history).
- **Expression evaluation** (e.g., balanced parentheses `(([]))` check).
- **Function calls in recursion** (i.e., call stack).
- **Reversing elements** (e.g., reversing a string).
- **Backtracking algorithms** (e.g., solving mazes, DFS traversal).

---

## **2️⃣ Working of Stacks**
A stack supports **four primary operations**:
1. **push(x)** → Adds an element `x` to the top of the stack.
2. **pop()** → Removes and returns the top element.
3. **peek()** → Returns the top element without removing it.
4. **isEmpty()** → Checks if the stack is empty.

---

## **3️⃣ Implementing a Stack in Java**
### ✅ **(A) Stack Using an Array**
```java
class Stack {
    private int[] arr;
    private int top;
    private int capacity;

    public Stack(int size) {
        arr = new int[size];
        capacity = size;
        top = -1;
    }

    // Push an element onto the stack
    public void push(int item) {
        if (top == capacity - 1) {
            System.out.println("Stack Overflow!");
            return;
        }
        arr[++top] = item;
    }

    // Pop an element from the stack
    public int pop() {
        if (top == -1) {
            System.out.println("Stack Underflow!");
            return -1;
        }
        return arr[top--];
    }

    // Peek at the top element
    public int peek() {
        if (top == -1) {
            System.out.println("Stack is empty!");
            return -1;
        }
        return arr[top];
    }

    // Check if stack is empty
    public boolean isEmpty() {
        return top == -1;
    }

    public static void main(String[] args) {
        Stack stack = new Stack(5);
        stack.push(10);
        stack.push(20);
        stack.push(30);
        System.out.println(stack.pop()); // Output: 30
        System.out.println(stack.peek()); // Output: 20
    }
}
```
### ✅ **(B) Stack Using Java Collections (`Stack<E>`)**
```java
import java.util.Stack;

public class StackExample {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();
        stack.push(10);
        stack.push(20);
        stack.push(30);

        System.out.println(stack.pop()); // Output: 30
        System.out.println(stack.peek()); // Output: 20
    }
}
```
**Comparison:**
| Approach | Advantages | Disadvantages |
|----------|------------|--------------|
| **Array-based** | Faster access (`O(1)`) | Fixed size, not dynamic |
| **Collections-based** | Dynamic, in-built methods | Slightly slower due to additional overhead |

---

## **4️⃣ Stacks Exercises**
### **Exercise 1: Reverse a String Using a Stack**
#### 📌 **Problem Statement**
Reverse a given string using a stack.

#### ✅ **Solution**
```java
import java.util.Stack;

public class ReverseString {
    public static String reverse(String str) {
        Stack<Character> stack = new Stack<>();
        for (char ch : str.toCharArray()) {
            stack.push(ch);
        }

        StringBuilder reversed = new StringBuilder();
        while (!stack.isEmpty()) {
            reversed.append(stack.pop());
        }

        return reversed.toString();
    }

    public static void main(String[] args) {
        String result = reverse("hello");
        System.out.println(result); // Output: olleh
    }
}
```

---

### **Exercise 2: Balanced Expression Using Stack**
#### 📌 **Problem Statement**
Check if an expression contains balanced parentheses.

#### ✅ **Solution**
```java
import java.util.Stack;

public class BalancedExpression {
    public static boolean isBalanced(String expression) {
        Stack<Character> stack = new Stack<>();
        for (char ch : expression.toCharArray()) {
            if (ch == '(' || ch == '[' || ch == '{')
                stack.push(ch);
            else if (ch == ')' && !stack.isEmpty() && stack.peek() == '(')
                stack.pop();
            else if (ch == ']' && !stack.isEmpty() && stack.peek() == '[')
                stack.pop();
            else if (ch == '}' && !stack.isEmpty() && stack.peek() == '{')
                stack.pop();
            else
                return false;
        }
        return stack.isEmpty();
    }

    public static void main(String[] args) {
        System.out.println(isBalanced("{[()]}")); // Output: true
        System.out.println(isBalanced("{[(])}")); // Output: false
    }
}
```

---

### **Exercise 3: Implement Two Stacks in One Array**
#### 📌 **Problem Statement**
Design two stacks using a single array efficiently.

#### ✅ **Solution**
```java
class TwoStacks {
    private int[] arr;
    private int top1, top2, size;

    public TwoStacks(int n) {
        size = n;
        arr = new int[n];
        top1 = -1;
        top2 = size;
    }

    public void push1(int x) {
        if (top1 < top2 - 1) {
            arr[++top1] = x;
        } else {
            System.out.println("Stack Overflow!");
        }
    }

    public void push2(int x) {
        if (top1 < top2 - 1) {
            arr[--top2] = x;
        } else {
            System.out.println("Stack Overflow!");
        }
    }

    public int pop1() {
        return top1 >= 0 ? arr[top1--] : -1;
    }

    public int pop2() {
        return top2 < size ? arr[top2++] : -1;
    }

    public boolean isEmpty1() {
        return top1 == -1;
    }

    public boolean isEmpty2() {
        return top2 == size;
    }

    public static void main(String[] args) {
        TwoStacks ts = new TwoStacks(10);
        ts.push1(1);
        ts.push2(9);
        System.out.println(ts.pop1()); // Output: 1
        System.out.println(ts.pop2()); // Output: 9
    }
}
```

---

### **Exercise 4: Design MinStack (Stack with min in O(1))**
#### 📌 **Problem Statement**
Design a stack that supports retrieving the **minimum element in constant time**.

#### ✅ **Solution**
```java
import java.util.Stack;

class MinStack {
    private Stack<Integer> stack = new Stack<>();
    private Stack<Integer> minStack = new Stack<>();

    public void push(int value) {
        stack.push(value);
        if (minStack.isEmpty() || value <= minStack.peek())
            minStack.push(value);
    }

    public void pop() {
        if (stack.pop().equals(minStack.peek()))
            minStack.pop();
    }

    public int min() {
        return minStack.peek();
    }

    public static void main(String[] args) {
        MinStack stack = new MinStack();
        stack.push(5);
        stack.push(2);
        stack.push(10);
        stack.push(1);
        System.out.println(stack.min()); // Output: 1
        stack.pop();
        System.out.println(stack.min()); // Output: 2
    }
}
```

---

## **5️⃣ Summary & Cheat Sheet**
| Operation | Normal Stack | MinStack |
|-----------|-------------|----------|
| `push()` | `O(1)` | `O(1)` |
| `pop()` | `O(1)` | `O(1)` |
| `min()` | `O(n)` | `O(1)` |

---

