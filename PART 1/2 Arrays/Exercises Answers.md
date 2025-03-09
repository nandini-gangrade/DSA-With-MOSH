# **📌 Array Exercises**

<br>

### **1️⃣ Find the Largest Number in an Array**
**Time Complexity: O(N)**  

```java
public class FindMax {
    public static int max(int[] arr) {
        int max = arr[0];
        for (int num : arr) {
            if (num > max) max = num;
        }
        return max;
    }

    public static void main(String[] args) {
        int[] arr = {10, 20, 5, 40, 30};
        System.out.println("Max: " + max(arr));  // Output: 40
    }
}
```

<br>


### **2️⃣ Find Common Elements Between Two Arrays**
**Time Complexity: O(N)** using HashSet  

```java
import java.util.*;

public class FindIntersection {
    public static List<Integer> intersect(int[] arr1, int[] arr2) {
        Set<Integer> set = new HashSet<>();
        List<Integer> common = new ArrayList<>();

        for (int num : arr1) set.add(num);
        for (int num : arr2) {
            if (set.contains(num)) common.add(num);
        }

        return common;
    }

    public static void main(String[] args) {
        int[] arr1 = {10, 20, 30, 40};
        int[] arr2 = {20, 40, 50};

        System.out.println("Common Elements: " + intersect(arr1, arr2));  
        // Output: [20, 40]
    }
}
```

<br>

### **3️⃣ Reverse an Array**
**Time Complexity: O(N)**  

```java
public class ReverseArray {
    public static void reverse(int[] arr) {
        for (int i = 0; i < arr.length / 2; i++) {
            int temp = arr[i];
            arr[i] = arr[arr.length - 1 - i];
            arr[arr.length - 1 - i] = temp;
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4};
        reverse(arr);
        for (int num : arr) System.out.print(num + " ");  // Output: 4 3 2 1
    }
}
```

<br>

### **4️⃣ Insert an Item at a Given Index**
**Time Complexity: O(N)**  

```java
public class InsertAt {
    public static void insertAt(int[] arr, int item, int index) {
        for (int i = arr.length - 1; i > index; i--) {
            arr[i] = arr[i - 1];
        }
        arr[index] = item;
    }

    public static void main(String[] args) {
        int[] arr = {10, 20, 30, 40, 50};
        insertAt(arr, 25, 2);
        for (int num : arr) System.out.print(num + " ");  
        // Output: 10 20 25 30 40
    }
}
```
