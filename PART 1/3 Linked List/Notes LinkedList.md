# 📌 **Linked List in Java using `LinkedList` Collection**
Java provides a built-in **LinkedList** class in **`java.util`** package that makes it easy to perform linked list operations without manually creating nodes.

## 🔹 **Key Features of `LinkedList` in Java**
- **Implements `List` and `Deque` interfaces** (so it can be used as a queue or stack).
- **Dynamic size** (grows as needed).
- **Efficient insertions and deletions** compared to arrays.
- **Slower random access** than arrays (O(N) vs O(1)).

---

## 1️⃣ **Creating a Linked List**
### ✅ **Code Implementation:**
```java
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        // Creating a LinkedList of Integers
        LinkedList<Integer> list = new LinkedList<>();

        // Adding elements
        list.add(10);
        list.add(20);
        list.add(30);

        System.out.println("LinkedList: " + list);
    }
}
```
### ✅ **Output:**
```
LinkedList: [10, 20, 30]
```
---

## 2️⃣ **Adding Elements to a Linked List**
### 🔹 **Adding at the end (`add()`)**
```java
list.add(40);  // Appends 40 at the end
```

### 🔹 **Adding at the beginning (`addFirst()`)**
```java
list.addFirst(5);  // Adds 5 at the beginning
```

### 🔹 **Adding at a specific index (`add(index, value)`)**
```java
list.add(2, 25);  // Adds 25 at index 2
```

### ✅ **Complete Example:**
```java
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        LinkedList<Integer> list = new LinkedList<>();

        list.add(10);
        list.add(20);
        list.add(30);
        list.addFirst(5);
        list.add(2, 25);
        
        System.out.println("LinkedList after additions: " + list);
    }
}
```
### ✅ **Output:**
```
LinkedList after additions: [5, 10, 25, 20, 30]
```

---

## 3️⃣ **Searching Elements**
### 🔹 **Checking if an element exists (`contains()`)**
```java
System.out.println(list.contains(20));  // true
```

### 🔹 **Finding index of an element (`indexOf()`)**
```java
System.out.println(list.indexOf(25));  // 2
```

### ✅ **Example:**
```java
System.out.println("Index of 25: " + list.indexOf(25));  // 2
System.out.println("Does list contain 50? " + list.contains(50));  // false
```

### ✅ **Output:**
```
Index of 25: 2
Does list contain 50? false
```

---

## 4️⃣ **Removing Elements**
### 🔹 **Removing First Element (`removeFirst()`)**
```java
list.removeFirst();
```

### 🔹 **Removing Last Element (`removeLast()`)**
```java
list.removeLast();
```

### 🔹 **Removing by Value (`remove(value)`)**
```java
list.remove(Integer.valueOf(20));
```

### ✅ **Complete Example:**
```java
list.removeFirst();   // Removes 5
list.removeLast();    // Removes 30
list.remove(Integer.valueOf(20)); // Removes 20
System.out.println("LinkedList after deletions: " + list);
```
### ✅ **Output:**
```
LinkedList after deletions: [10, 25]
```

---

## 5️⃣ **Utility Methods**
### 🔹 **Getting the Size (`size()`)**
```java
System.out.println("Size: " + list.size());
```
### 🔹 **Converting to Array (`toArray()`)**
```java
Object[] array = list.toArray();
System.out.println("Array: " + Arrays.toString(array));
```

### ✅ **Example & Output:**
```java
System.out.println("Size: " + list.size());  
```
```
Size: 2
```

---

## 6️⃣ **Reversing a Linked List**
Java’s `Collections.reverse()` method can be used to reverse a LinkedList.

### ✅ **Example:**
```java
import java.util.Collections;

Collections.reverse(list);
System.out.println("Reversed LinkedList: " + list);
```

### ✅ **Output:**
```
Reversed LinkedList: [25, 10]
```

---

## 7️⃣ **Finding Kth Node from End**
Since we can't access elements directly, we can use `size()`.

### ✅ **Code Implementation:**
```java
public static int getKthFromEnd(LinkedList<Integer> list, int k) {
    return list.get(list.size() - k);
}
```
```java
System.out.println(getKthFromEnd(list, 2));  // 10
```
### ✅ **Output:**
```
10
```

---

## 8️⃣ **Detecting a Loop in a Linked List**
The `LinkedList` class does not have direct looping, but we can **simulate** it by using a `HashSet`.

### ✅ **Code Implementation:**
```java
import java.util.HashSet;

public static boolean hasLoop(LinkedList<Integer> list) {
    HashSet<Integer> set = new HashSet<>();
    for (int item : list) {
        if (!set.add(item)) return true;  // If duplicate found, loop exists
    }
    return false;
}
```

### ✅ **Output:**
```
false (No loop)
```

---

## 9️⃣ **Finding the Middle Node**
We use `size()` to find the **middle index**.

### ✅ **Code Implementation:**
```java
public static int getMiddle(LinkedList<Integer> list) {
    return list.get(list.size() / 2);
}
```
```java
System.out.println(getMiddle(list));  // 25
```

---

## 🔟 **Comparison: Linked Lists vs. Arrays**
| Feature | LinkedList | ArrayList |
|---------|-----------|-----------|
| **Insertion (Head/Tail)** | O(1) | O(N) |
| **Random Access** | O(N) | O(1) |
| **Memory Usage** | More (Extra pointers) | Less |
| **Traversal** | Slower | Faster |
| **Sorting** | Slower | Faster |

---

## 🎯 **Final Summary**
- `LinkedList` in Java **makes operations easier** than manual implementation.
- **Use LinkedList when:** Frequent insertions/deletions are needed.
- **Use ArrayList when:** Fast **random access** is needed.
