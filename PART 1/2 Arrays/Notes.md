# Arrays in Java - Complete Guide

## Introduction to Arrays
An **array** is a collection of elements stored in contiguous memory locations. It allows multiple values of the same type to be stored together, making it easier to manage and process large amounts of data efficiently.

### Why Use Arrays?
- **Efficient Data Storage**: Stores multiple values in a single variable.
- **Faster Access**: Access elements using an index.
- **Better Memory Management**: Elements are stored in contiguous memory locations.
- **Fixed Size**: Once an array is created, its size cannot change.

---

## Understanding Arrays
### Declaration & Initialization
```java
// Declaring an array
int[] numbers = new int[5];

// Initializing an array
int[] values = {10, 20, 30, 40, 50};

// Accessing elements
System.out.println(values[0]); // Output: 10
```
**Explanation:**
- The first statement declares an integer array of size 5 but doesn't initialize it.
- The second initializes an array with values.
- The third prints the first element (index 0).

#### Expected Output:
```
10
```

---

### Array Operations
- **Insert elements** at a given index.
- **Remove elements** by shifting remaining elements.
- **Search for elements** using loops.
- **Resize dynamically** (for flexible arrays).

---

## Working with Arrays
### Inserting an Element
```java
public void insert(int[] arr, int value, int index) {
    for (int i = arr.length - 1; i > index; i--) {
        arr[i] = arr[i - 1]; // Shift elements right
    }
    arr[index] = value; // Insert new value
}
```
**Explanation:** Inserts a value at a specified index by shifting elements to the right to make space.

### Removing an Element
```java
public void removeAt(int[] arr, int index) {
    for (int i = index; i < arr.length - 1; i++) {
        arr[i] = arr[i + 1]; // Shift elements left
    }
    arr[arr.length - 1] = 0; // Optional: Reset last element
}
```
**Expected Output:** (For array `[10, 20, 30, 40, 50]`, removing index `2`)
```
10 20 40 50 0
```

### Searching for an Element
```java
public int indexOf(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) return i; // Return index if found
    }
    return -1; // Not found
}
```
**Expected Output:** (For array `[10, 20, 30, 40, 50]`, searching `30`)
```
2
```

---

## Dynamic Arrays
Since Java arrays have a fixed size, we use dynamic arrays to expand automatically.

```java
class DynamicArray {
    private int[] arr;
    private int count;

    public DynamicArray(int size) {
        arr = new int[size];
    }

    public void insert(int item) {
        if (count == arr.length) {
            int[] newArr = new int[count * 2]; // Resize array
            for (int i = 0; i < count; i++)
                newArr[i] = arr[i];
            arr = newArr;
        }
        arr[count++] = item;
    }

    public void print() {
        for (int i = 0; i < count; i++)
            System.out.print(arr[i] + " ");
        System.out.println();
    }
}
```
**Expected Output:**
```
10 20 30 40 50 60 70
```

## Using ArrayList for Dynamic Arrays
Java provides `ArrayList`, a resizable array implementation, which automatically adjusts its capacity as elements are added or removed.

### Why Use ArrayList?
- **Dynamic Resizing**: No need to define a fixed size.
- **Built-in Methods**: Provides easy insertions, deletions, and searches.
- **Type-Safety**: Supports generics to ensure type consistency.

### Creating and Using an ArrayList
```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<Integer> numbers = new ArrayList<>(); // Creating a dynamic array
        
        // Adding elements
        numbers.add(10);
        numbers.add(20);
        numbers.add(30);
        numbers.add(40);
        
        System.out.println(numbers); // Output: [10, 20, 30, 40]
        
        // Accessing elements
        System.out.println(numbers.get(2)); // Output: 30
        
        // Removing an element
        numbers.remove(1); // Removes element at index 1
        System.out.println(numbers); // Output: [10, 30, 40]
        
        // Finding the size
        System.out.println("Size: " + numbers.size()); // Output: 3
    }
}
```
**Explanation:**
- `ArrayList<Integer> numbers = new ArrayList<>();` → Creates a dynamic array.
- `numbers.add(value);` → Adds an element.
- `numbers.get(index);` → Retrieves an element at the specified index.
- `numbers.remove(index);` → Removes an element.
- `numbers.size();` → Returns the number of elements.

---

## Advanced ArrayList Operations
### Iterating Over an ArrayList
```java
ArrayList<String> names = new ArrayList<>();
names.add("Alice");
names.add("Bob");
names.add("Charlie");

// Using a for-each loop
for (String name : names) {
    System.out.println(name);
}
```
**Expected Output:**
```
Alice
Bob
Charlie
```

### Searching for an Element
```java
if (numbers.contains(30)) {
    System.out.println("30 is in the list");
}
```
**Expected Output:**
```
30 is in the list
```

### Sorting an ArrayList
```java
import java.util.Collections;

Collections.sort(numbers);
```
**Explanation:** `Collections.sort()` sorts the list in ascending order.

---

## Summary
- **Arrays have a fixed size**, while `ArrayList` is dynamic.
- **ArrayList** provides built-in methods for easy manipulation.
- **Common operations** include adding, removing, searching, and sorting elements.
- **Use `ArrayList`** when a resizable array is needed.

---

## Exercise - Extending the Array Class
### 1. Finding the Largest Number
```java
public int max() {
    int max = arr[0];
    for (int i = 1; i < count; i++) {
        if (arr[i] > max) max = arr[i]; // Compare elements
    }
    return max;
}
```
**Expected Output:** (For array `[10, 20, 30, 40, 50]`)
```
50
```

### 2. Finding Common Elements
```java
public List<Integer> intersect(int[] arr1, int[] arr2) {
    Set<Integer> set = new HashSet<>();
    List<Integer> common = new ArrayList<>();

    for (int num : arr1) set.add(num);
    for (int num : arr2) {
        if (set.contains(num)) common.add(num);
    }

    return common;
}
```
**Expected Output:** (For arrays `[10, 20, 30, 40]` and `[30, 40, 50, 60]`)
```
[30, 40]
```

### 3. Reversing an Array
```java
public void reverse() {
    for (int i = 0; i < count / 2; i++) {
        int temp = arr[i];
        arr[i] = arr[count - 1 - i]; // Swap elements
        arr[count - 1 - i] = temp;
    }
}
```
**Expected Output:** (For array `[10, 20, 30, 40, 50]`)
```
50 40 30 20 10
```

### 4. Insert at a Given Index
```java
public void insertAt(int item, int index) {
    if (index < 0 || index > count) throw new IllegalArgumentException();
    if (count == arr.length) resize();

    for (int i = count; i > index; i--) {
        arr[i] = arr[i - 1]; // Shift right
    }
    arr[index] = item; // Insert element
    count++;
}
```
**Expected Output:** (For array `[10, 20, 30, 40, 50]`, inserting `25` at index `2`)
```
10 20 25 30 40 50
```

---

## Summary
- **Arrays are fixed-size** but allow fast access.
- **Dynamic arrays** automatically resize.
- **Common operations** include inserting, removing, searching, and reversing.
- **Extending the array class** adds custom functionalities like max(), intersect(), reverse(), and insertAt().

This guide provides a complete understanding of arrays in Java with practical examples and exercises. 🚀

