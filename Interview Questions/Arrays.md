
# TOP 50 ARRAY INTERVIEW QUESTIONS WITH SOLUTIONS IN JAVA

## Basic Array Operations

### 1. How do you declare and initialize an array in Java?
```java
// Declaration
int[] numbers;            // Preferred way
int numbers[];            // Also valid

// Declaration and initialization
int[] numbers = new int[5];                  // Initialize with default values (0)
int[] numbers = {1, 2, 3, 4, 5};             // Initialize with specific values
int[] numbers = new int[]{1, 2, 3, 4, 5};    // Explicit way

// Declaration and initialization in separate statements
int[] numbers;
numbers = new int[5];
// OR
numbers = new int[]{1, 2, 3, 4, 5};
```

### 2. What is the difference between length and length() method in Java?
```java
// length is a property of arrays
int[] array = {1, 2, 3, 4, 5};
int arrayLength = array.length;  // Returns 5

// length() is a method of String class
String str = "Hello";
int strLength = str.length();    // Returns 5

// size() is a method of Collection classes
ArrayList<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
int listSize = list.size();      // Returns 2
```

### 3. How to find the length of an array in Java?
```java
int[] numbers = {1, 2, 3, 4, 5};
int length = numbers.length;  // Returns 5

// For multidimensional arrays
int[][] matrix = {{1, 2, 3}, {4, 5, 6}};
int rows = matrix.length;        // Returns 2
int columns = matrix[0].length;  // Returns 3
```

### 4. How do you iterate through an array in Java? Show different approaches.
```java
int[] numbers = {1, 2, 3, 4, 5};

// Using for loop with index
for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}

// Using enhanced for loop (for-each)
for (int num : numbers) {
    System.out.println(num);
}

// Using while loop
int i = 0;
while (i < numbers.length) {
    System.out.println(numbers[i]);
    i++;
}

// Using Java 8 Streams
Arrays.stream(numbers).forEach(System.out::println);

// Using Iterator from Arrays.asList (for non-primitive types)
Integer[] nums = {1, 2, 3, 4, 5};
Iterator<Integer> iterator = Arrays.asList(nums).iterator();
while (iterator.hasNext()) {
    System.out.println(iterator.next());
}
```

### 5. Explain how to check if two arrays are equal in Java.
```java
// Method 1: Using Arrays.equals() (for 1D arrays)
int[] array1 = {1, 2, 3, 4, 5};
int[] array2 = {1, 2, 3, 4, 5};
boolean isEqual = Arrays.equals(array1, array2);   // Returns true

// Method 2: Using Arrays.deepEquals() (for multidimensional arrays)
int[][] matrix1 = {{1, 2}, {3, 4}};
int[][] matrix2 = {{1, 2}, {3, 4}};
boolean isDeepEqual = Arrays.deepEquals(matrix1, matrix2);   // Returns true

// Method 3: Manual comparison
boolean areEqual = true;
if (array1.length != array2.length) {
    areEqual = false;
} else {
    for (int i = 0; i < array1.length; i++) {
        if (array1[i] != array2[i]) {
            areEqual = false;
            break;
        }
    }
}
```

### 6. How do you print all elements of an array in Java?
```java
int[] numbers = {1, 2, 3, 4, 5};

// Method 1: Using for loop
for (int i = 0; i < numbers.length; i++) {
    System.out.print(numbers[i] + " ");
}

// Method 2: Using enhanced for loop
for (int num : numbers) {
    System.out.print(num + " ");
}

// Method 3: Using Arrays.toString()
System.out.println(Arrays.toString(numbers));  // Output: [1, 2, 3, 4, 5]

// Method 4: Using Java 8 Streams
System.out.println(Arrays.stream(numbers)
                         .mapToObj(String::valueOf)
                         .collect(Collectors.joining(", ")));

// Method 5: For multidimensional arrays, use Arrays.deepToString()
int[][] matrix = {{1, 2}, {3, 4}};
System.out.println(Arrays.deepToString(matrix));  // Output: [[1, 2], [3, 4]]
```

### 7. What is the default value for array elements of different types?
```java
// Numeric primitive types (byte, short, int, long) default to 0
int[] nums = new int[3];
System.out.println(nums[0]);  // Output: 0

// float and double default to 0.0
double[] doubles = new double[3];
System.out.println(doubles[0]);  // Output: 0.0

// char defaults to '\u0000' (null character)
char[] chars = new char[3];
System.out.println((int)chars[0]);  // Output: 0

// boolean defaults to false
boolean[] bools = new boolean[3];
System.out.println(bools[0]);  // Output: false

// Reference types (objects) default to null
String[] strings = new String[3];
System.out.println(strings[0]);  // Output: null
```

### 8. How do you copy an array to another array in Java?
```java
int[] sourceArray = {1, 2, 3, 4, 5};
int[] targetArray;

// Method 1: Using System.arraycopy()
targetArray = new int[sourceArray.length];
System.arraycopy(sourceArray, 0, targetArray, 0, sourceArray.length);

// Method 2: Using Arrays.copyOf()
targetArray = Arrays.copyOf(sourceArray, sourceArray.length);

// Method 3: Using Arrays.copyOfRange()
targetArray = Arrays.copyOfRange(sourceArray, 0, sourceArray.length);

// Method 4: Using clone method
targetArray = sourceArray.clone();

// Method 5: Manual copy using a loop
targetArray = new int[sourceArray.length];
for (int i = 0; i < sourceArray.length; i++) {
    targetArray[i] = sourceArray[i];
}

// Method 6: Using Java 8 Streams (for non-primitive arrays)
Integer[] source = {1, 2, 3, 4, 5};
Integer[] target = Arrays.stream(source).toArray(Integer[]::new);
```

### 9. What is a deep copy vs shallow copy of an array?
```java
// Shallow Copy Example
// For primitive types, shallow and deep copies behave the same
int[] original = {1, 2, 3};
int[] shallowCopy = original.clone();
shallowCopy[0] = 10;  // Doesn't affect original array

// For reference types, shallow copy copies only the references
Person[] originalPeople = {new Person("Alice"), new Person("Bob")};
Person[] shallowCopyPeople = originalPeople.clone();
shallowCopyPeople[0].setName("Alicia");  // Also changes originalPeople[0].name

// Deep Copy Example
Person[] deepCopyPeople = new Person[originalPeople.length];
for (int i = 0; i < originalPeople.length; i++) {
    // Create a new object with the same property values
    deepCopyPeople[i] = new Person(originalPeople[i].getName());
}
deepCopyPeople[0].setName("Alicia");  // Doesn't affect originalPeople[0].name

// Person class for the example
class Person {
    private String name;
    
    public Person(String name) {
        this.name = name;
    }
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
}
```

### 10. How to convert an ArrayList to an array in Java?
```java
ArrayList<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.add(3);

// Method 1: Using toArray() with array constructor reference
Integer[] array = list.toArray(new Integer[0]);

// Method 2: Using toArray() with exact size
Integer[] exactArray = list.toArray(new Integer[list.size()]);

// Method 3: For primitive int array (Java 8+)
int[] primitiveArray = list.stream().mapToInt(Integer::intValue).toArray();

// Method 4: Manual conversion
int[] manual = new int[list.size()];
for (int i = 0; i < list.size(); i++) {
    manual[i] = list.get(i);
}

// Converting array back to ArrayList
Integer[] nums = {1, 2, 3};
ArrayList<Integer> newList = new ArrayList<>(Arrays.asList(nums));
```

## Searching and Sorting

### 11. Implement binary search on a sorted array.
```java
// Recursive Binary Search
public static int binarySearchRecursive(int[] arr, int target, int left, int right) {
    if (left > right) {
        return -1;  // Element not found
    }
    
    int mid = left + (right - left) / 2;  // Avoid overflow
    
    if (arr[mid] == target) {
        return mid;  // Found the element
    } else if (arr[mid] > target) {
        return binarySearchRecursive(arr, target, left, mid - 1);  // Search in left half
    } else {
        return binarySearchRecursive(arr, target, mid + 1, right);  // Search in right half
    }
}

// Iterative Binary Search
public static int binarySearchIterative(int[] arr, int target) {
    int left = 0;
    int right = arr.length - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (arr[mid] == target) {
            return mid;  // Found the element
        } else if (arr[mid] > target) {
            right = mid - 1;  // Search in left half
        } else {
            left = mid + 1;  // Search in right half
        }
    }
    
    return -1;  // Element not found
}

// Using Java's Arrays.binarySearch()
public static int binarySearchBuiltIn(int[] arr, int target) {
    return Arrays.binarySearch(arr, target);
    // Returns index if found, otherwise returns -(insertion point) - 1
}
```

### 12. Implement bubble sort algorithm.
```java
public static void bubbleSort(int[] arr) {
    int n = arr.length;
    boolean swapped;
    
    for (int i = 0; i < n - 1; i++) {
        swapped = false;
        
        // Last i elements are already in place
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j+1]
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = true;
            }
        }
        
        // If no swapping occurred in this pass, array is sorted
        if (!swapped) {
            break;
        }
    }
}
```

### 13. Implement insertion sort algorithm.
```java
public static void insertionSort(int[] arr) {
    int n = arr.length;
    
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        
        // Move elements of arr[0..i-1] that are greater than key
        // to one position ahead of their current position
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        
        arr[j + 1] = key;
    }
}
```

### 14. Implement merge sort algorithm.
```java
public static void mergeSort(int[] arr, int left, int right) {
    if (left < right) {
        // Find the middle point
        int mid = left + (right - left) / 2;
        
        // Sort first and second halves
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        
        // Merge the sorted halves
        merge(arr, left, mid, right);
    }
}

private static void merge(int[] arr, int left, int mid, int right) {
    // Sizes of two subarrays to be merged
    int n1 = mid - left + 1;
    int n2 = right - mid;
    
    // Create temporary arrays
    int[] L = new int[n1];
    int[] R = new int[n2];
    
    // Copy data to temporary arrays
    for (int i = 0; i < n1; i++) {
        L[i] = arr[left + i];
    }
    for (int j = 0; j < n2; j++) {
        R[j] = arr[mid + 1 + j];
    }
    
    // Merge the temporary arrays back
    int i = 0, j = 0;
    int k = left;
    
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }
    
    // Copy remaining elements of L[] if any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }
    
    // Copy remaining elements of R[] if any
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}
```

### 15. Implement quick sort algorithm.
```java
public static void quickSort(int[] arr, int low, int high) {
    if (low < high) {
        // Partition the array and get the pivot index
        int pivotIndex = partition(arr, low, high);
        
        // Sort the sub-arrays recursively
        quickSort(arr, low, pivotIndex - 1);
        quickSort(arr, pivotIndex + 1, high);
    }
}

private static int partition(int[] arr, int low, int high) {
    // Select the rightmost element as pivot
    int pivot = arr[high];
    
    // Index of smaller element
    int i = low - 1;
    
    for (int j = low; j < high; j++) {
        // If current element is smaller than or equal to pivot
        if (arr[j] <= pivot) {
            i++;
            
            // Swap arr[i] and arr[j]
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
    
    // Swap arr[i+1] and arr[high] (the pivot)
    int temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;
    
    return i + 1;
}
```

### 16. Find the kth largest element in an unsorted array.
```java
// Method 1: Using sorting
public static int findKthLargestBySorting(int[] nums, int k) {
    Arrays.sort(nums);
    return nums[nums.length - k];
}

// Method 2: Using a min-heap of size k
public static int findKthLargestByHeap(int[] nums, int k) {
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();
    
    for (int num : nums) {
        minHeap.add(num);
        
        // Keep only k largest elements in the heap
        if (minHeap.size() > k) {
            minHeap.poll();
        }
    }
    
    return minHeap.peek();
}

// Method 3: Using QuickSelect algorithm (average O(n) time complexity)
public static int findKthLargestByQuickSelect(int[] nums, int k) {
    return quickSelect(nums, 0, nums.length - 1, nums.length - k);
}

private static int quickSelect(int[] nums, int low, int high, int k) {
    if (low == high) {
        return nums[low];
    }
    
    int pivotIndex = partition(nums, low, high);
    
    if (k == pivotIndex) {
        return nums[k];
    } else if (k < pivotIndex) {
        return quickSelect(nums, low, pivotIndex - 1, k);
    } else {
        return quickSelect(nums, pivotIndex + 1, high, k);
    }
}

private static int partition(int[] nums, int low, int high) {
    int pivot = nums[high];
    int i = low;
    
    for (int j = low; j < high; j++) {
        if (nums[j] <= pivot) {
            swap(nums, i, j);
            i++;
        }
    }
    
    swap(nums, i, high);
    return i;
}

private static void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}
```

### 17. Search for an element in a rotated sorted array.
```java
public static int searchInRotatedArray(int[] nums, int target) {
    int left = 0;
    int right = nums.length - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (nums[mid] == target) {
            return mid;
        }
        
        // Check if the left side is sorted
        if (nums[left] <= nums[mid]) {
            // Check if target is in the left sorted portion
            if (nums[left] <= target && target < nums[mid]) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        } 
        // Otherwise, the right side is sorted
        else {
            // Check if target is in the right sorted portion
            if (nums[mid] < target && target <= nums[right]) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
    }
    
    return -1;  // Target not found
}
```

### 18. Find the smallest missing positive integer in an unsorted array.
```java
// Time Complexity: O(n), Space Complexity: O(1)
public static int firstMissingPositive(int[] nums) {
    int n = nums.length;
    
    // Step 1: Mark numbers <= 0 or > n as n+1
    for (int i = 0; i < n; i++) {
        if (nums[i] <= 0 || nums[i] > n) {
            nums[i] = n + 1;
        }
    }
    
    // Step 2: Mark indices corresponding to numbers in the array
    for (int i = 0; i < n; i++) {
        int num = Math.abs(nums[i]);
        if (num <= n) {
            // Mark the number as seen by making its position negative
            nums[num - 1] = -Math.abs(nums[num - 1]);
        }
    }
    
    // Step 3: Find the first index that doesn't have a negative value
    for (int i = 0; i < n; i++) {
        if (nums[i] > 0) {
            return i + 1;
        }
    }
    
    // If all numbers from 1 to n are present, return n+1
    return n + 1;
}
```

### 19. How to check if an array contains a specific value?
```java
// Method 1: Using a loop
public static boolean containsValue(int[] arr, int value) {
    for (int num : arr) {
        if (num == value) {
            return true;
        }
    }
    return false;
}

// Method 2: Using Java 8 Streams
public static boolean containsValueUsingStreams(int[] arr, int value) {
    return Arrays.stream(arr).anyMatch(num -> num == value);
}

// Method 3: Using Arrays.binarySearch() for sorted arrays
public static boolean containsValueBinarySearch(int[] sortedArr, int value) {
    return Arrays.binarySearch(sortedArr, value) >= 0;
}

// Method 4: Using Collections.contains() (for non-primitive arrays)
public static boolean containsValueUsingCollections(Integer[] arr, Integer value) {
    return Arrays.asList(arr).contains(value);
}
```

### 20. Find the peak element in an array.
```java
// Peak element: An element greater than its neighbors (or array boundary)
// If multiple peaks exist, return any one of them
public static int findPeakElement(int[] nums) {
    int left = 0;
    int right = nums.length - 1;
    
    while (left < right) {
        int mid = left + (right - left) / 2;
        
        // If mid element is greater than the next element, 
        // then mid element is in a decreasing sequence,
        // so the peak is on the left side (including mid)
        if (nums[mid] > nums[mid + 1]) {
            right = mid;
        } 
        // Otherwise, mid element is in an increasing sequence,
        // so the peak is on the right side (excluding mid)
        else {
            left = mid + 1;
        }
    }
    
    // At this point, left == right, return either one
    return left;
}
```

## Array Manipulation

### 21. How to find the maximum and minimum elements in an array?
```java
// Method 1: Using loops
public static int[] findMinMax(int[] arr) {
    if (arr == null || arr.length == 0) {
        throw new IllegalArgumentException("Array is empty or null");
    }
    
    int min = arr[0];
    int max = arr[0];
    
    for (int i = 1; i < arr.length; i++) {
        if (arr[i] < min) {
            min = arr[i];
        }
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    
    return new int[]{min, max};
}

// Method 2: Using Java 8 Streams
public static int[] findMinMaxUsingStreams(int[] arr) {
    if (arr == null || arr.length == 0) {
        throw new IllegalArgumentException("Array is empty or null");
    }
    
    IntSummaryStatistics stats = Arrays.stream(arr).summaryStatistics();
    return new int[]{stats.getMin(), stats.getMax()};
}

// Method 3: Using Collections
public static int[] findMinMaxUsingCollections(Integer[] arr) {
    if (arr == null || arr.length == 0) {
        throw new IllegalArgumentException("Array is empty or null");
    }
    
    int min = Collections.min(Arrays.asList(arr));
    int max = Collections.max(Arrays.asList(arr));
    
    return new int[]{min, max};
}
```

### 22. How to find the sum of all elements in an array?
```java
// Method 1: Using a loop
public static int sumArray(int[] arr) {
    int sum = 0;
    for (int num : arr) {
        sum += num;
    }
    return sum;
}

// Method 2: Using Java 8 Streams
public static int sumArrayUsingStreams(int[] arr) {
    return Arrays.stream(arr).sum();
}

// Method 3: Using recursion
public static int sumArrayRecursive(int[] arr, int n) {
    if (n <= 0) {
        return 0;
    }
    return sumArrayRecursive(arr, n - 1) + arr[n - 1];
}

// Method 4: Using Arrays.stream with reduce operation
public static int sumArrayUsingReduce(int[] arr) {
    return Arrays.stream(arr).reduce(0, Integer::sum);
}
```

### 23. How to remove duplicates from an array?
```java
// For primitive arrays
public static int[] removeDuplicates(int[] arr) {
    if (arr == null || arr.length == 0) {
        return arr;
    }
    
    // Use Set to store unique elements
    Set<Integer> set = new LinkedHashSet<>();
    for (int num : arr) {
        set.add(num);
    }
    
    // Convert Set back to array
    int[] result = new int[set.size()];
    int i = 0;
    for (int num : set) {
        result[i++] = num;
    }
    
    return result;
}

// For non-primitive arrays using Java 8 Streams
public static <T> T[] removeDuplicatesUsingStreams(T[] arr) {
    if (arr == null || arr.length == 0) {
        return arr;
    }
    
    @SuppressWarnings("unchecked")
    T[] result = (T[]) Arrays.stream(arr)
                            .distinct()
                            .toArray(size -> (T[]) Array.newInstance(arr.getClass().getComponentType(), size));
    
    return result;
}

// Remove duplicates in place (for sorted array)
public static int removeDuplicatesInPlace(int[] nums) {
    if (nums.length == 0) {
        return 0;
    }
    
    int uniqueIndex = 0;
    for (int i = 1; i < nums.length; i++) {
        if (nums[i] != nums[uniqueIndex]) {
            uniqueIndex++;
            nums[uniqueIndex] = nums[i];
        }
    }
    
    return uniqueIndex + 1;  // new length
}
```

### 24. How to reverse an array in-place?
```java
public static void reverseArray(int[] arr) {
    int left = 0;
    int right = arr.length - 1;
    
    while (left < right) {
        // Swap elements at left and right indices
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        
        // Move indices toward the center
        left++;
        right--;
    }
}

// Using Java 8 Streams (not in-place, creates a new array)
public static int[] reverseArrayUsingStreams(int[] arr) {
    return IntStream.rangeClosed(1, arr.length)
                    .map(i -> arr[arr.length - i])
                    .toArray();
}

// Using Collections (for non-primitive arrays, not in-place)
public static <T> T[] reverseArrayUsingCollections(T[] arr) {
    List<T> list = Arrays.asList(arr);
    Collections.reverse(list);
    return list.toArray(arr);
}
```

### 25. How to rotate an array by k positions?
```java
// Right rotation by k positions
public static void rotateRight(int[] nums, int k) {
    int n = nums.length;
    
    // Handle edge cases
    if (n == 0 || k % n == 0) {
        return;
    }
    
    // Normalize k
    k = k % n;
    
    // Method 1: Using extra space
    int[] temp = new int[n];
    
    // Copy elements to temp array with rotation
    for (int i = 0; i < n; i++) {
        temp[(i + k) % n] = nums[i];
    }
    
    // Copy back to original array
    System.arraycopy(temp, 0, nums, 0, n);
    
    /* 
    // Method 2: Using array reversal (in-place)
    // Reverse the entire array
    reverse(nums, 0, n - 1);
    // Reverse the first k elements
    reverse(nums, 0, k - 1);
    // Reverse the remaining elements
    reverse(nums, k, n - 1);
    */
}

// Left rotation by k positions
public static void rotateLeft(int[] nums, int k) {
    int n = nums.length;
    
    // Handle edge cases
    if (n == 0 || k % n == 0) {
        return;
    }
    
    // Normalize k
    k = k % n;
    
    // Left rotation by k is equivalent to right rotation by (n-k)
    rotateRight(nums, n - k);
}

private static void reverse(int[] nums, int start, int end) {
    while (start < end) {
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
    }
}
```

### 26. Find pairs in array whose sum equals a given number.
```java
// Method 1: Using HashMap (O(n) time complexity)
public static void findPairsWithSum(int[] arr, int targetSum) {
    Map<Integer, Integer> numMap = new HashMap<>();
    
    for (int num : arr) {
        int complement = targetSum - num;
        
        if (numMap.containsKey(complement)) {
            int count = numMap.get(complement);
            for (int i = 0; i < count; i++) {
                System.out.println("Pair found: " + complement + ", " + num);
            }
        }
        
        numMap.put(num, numMap.getOrDefault(num, 0) + 1);
    }
}

// Method 2: Using sorting and two pointers (O(n log n) time complexity)
public static void findPairsWithSumSorting(int[] arr, int targetSum) {
    Arrays.sort(arr);
    
    int left = 0;
    int right = arr.length - 1;
    
    while (left < right) {
        int currentSum = arr[left] + arr[right];
        
        if (currentSum == targetSum) {
            System.out.println("Pair found: " + arr[left] + ", " + arr[right]);
            left++;
            right--;
        } else if (currentSum < targetSum) {
            left++;
        } else {
            right--;
        }
    }
}
```

### 27. Find the majority element in an array (appears more than n/2 times).
```java
// Method 1: Using HashMap (O(n) time, O(n) space)
public static int majorityElementHashMap(int[] nums) {
    Map<Integer, Integer> countMap = new HashMap<>();
    
    for (int num : nums) {
        countMap.put(num, countMap.getOrDefault(num, 0) + 1);
    }
    
    int majorityThreshold = nums.length / 2;
    
    for (Map.Entry<Integer, Integer> entry : countMap.entrySet()) {
        if (entry.getValue() > majorityThreshold) {
            return entry.getKey();
        }
    }
    
    return -1;  // No majority element
}

// Method 2: Using Boyer-Moore Voting Algorithm (O(n) time, O(1) space)
public static int majorityElementBoyerMoore(int[] nums) {
    int count = 0;
    Integer candidate = null;
    
    for (int num : nums) {
        if (count == 0) {
            candidate = num;
        }
        
        count += (num == candidate) ? 1 : -1;
    }
    
    // Verify that the candidate is actually the majority element
    count = 0;
    for (int num : nums) {
        if (num == candidate) {
            count++;
        }
    }
    
    return (count > nums.length / 2) ? candidate : -1;
}
```

### 28. Move all zeros to the end of the array while maintaining the order of non-zero elements.
```java
public static void moveZeros(int[] nums) {
    // Index to place non-zero elements
    int nonZeroIndex = 0;
    
    // Move all non-zero elements to the front of the array
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] != 0) {
            nums[nonZeroIndex++] = nums[i];
        }
    }
    
    // Fill the remaining positions with zeros
    for (int i = nonZeroIndex; i < nums.length; i++) {
        nums[i] = 0;
    }
}

// Alternative approach using a single pass
public static void moveZerosOptimized(int[] nums) {
    int nonZeroIndex = 0;
    
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] != 0) {
            // Swap elements if they are not at the same position
            if (i != nonZeroIndex) {
                int temp = nums[nonZeroIndex];
                nums[nonZeroIndex] = nums[i];
                nums[i] = temp;
            }
            nonZeroIndex++;
        }
    }
}
```

### 29. Find the maximum subarray sum (Kadane's algorithm).
```java
// Kadane's Algorithm for maximum subarray sum
public static int maxSubArraySum(int[] nums) {
    if (nums == null || nums.length == 0) {
        return 0;
    }
    
    int maxEndingHere = nums[0];
    int maxSoFar = nums[0];
    
    for (int i = 1; i < nums.length; i++) {
        // Current maximum subarray either includes the current element
        // or starts a new subarray from the current element
        maxEndingHere = Math.max(nums[i], maxEndingHere + nums[i]);
        
        // Update the global maximum
        maxSoFar = Math.max(maxSoFar, maxEndingHere);
    }
    
    return maxSoFar;
}

// Extended Kadane's Algorithm to return the start and end indices
public static int[] maxSubArraySumWithIndices(int[] nums) {
    if (nums == null || nums.length == 0) {
        return new int[]{0, -1, -1};  // Sum, start index, end index
    }
    
    int maxEndingHere = nums[0];
    int maxSoFar = nums[0];
    int startTemp = 0;
    int start = 0;
    int end = 0;
    
    for (int i = 1; i < nums.length; i++) {
        // If starting a new subarray is better
        if (nums[i] > maxEndingHere + nums[i]) {
            maxEndingHere = nums[i];
            startTemp = i;
        } else {
            maxEndingHere = maxEndingHere + nums[i];
        }
        
        // Update the global maximum
        if (maxEndingHere > maxSoFar) {
            maxSoFar = maxEndingHere;
            start = startTemp;
            end = i;
        }
    }
    
    return new int[]{maxSoFar, start, end};
}
```

### 30. Merge two sorted arrays into a single sorted array.
```java
// Merge two sorted arrays
public static int[] mergeSortedArrays(int[] arr1, int[] arr2) {
    int n1 = arr1.length;
    int n2 = arr2.length;
    int[] result = new int[n1 + n2];
    
    int i = 0, j = 0, k = 0;
    
    // Compare elements from both arrays and add the smaller one to result
    while (i < n1 && j < n2) {
        if (arr1[i] <= arr2[j]) {
            result[k++] = arr1[i++];
        } else {
            result[k++] = arr2[j++];
        }
    }
    
    // Copy remaining elements from first array
    while (i < n1) {
        result[k++] = arr1[i++];
    }
    
    // Copy remaining elements from second array
    while (j < n2) {
        result[k++] = arr2[j++];
    }
    
    return result;
}

// Merge sorted arrays in-place (when second array has enough space)
public static void mergeSortedArraysInPlace(int[] nums1, int m, int[] nums2, int n) {
    // Start from the end and work backwards
    int i = m - 1;  // Last element in nums1
    int j = n - 1;  // Last element in nums2
    int k = m + n - 1;  // Last position in nums1
    
    while (j >= 0) {
        // If there are still elements in nums1 and the element in nums1 is larger
        if (i >= 0 && nums1[i] > nums2[j]) {
            nums1[k--] = nums1[i--];
        } else {
            nums1[k--] = nums2[j--];
        }
    }
}
```

## Multi-dimensional Arrays

### 31. How to declare and initialize a 2D array in Java?
```java
// Declaration
int[][] matrix;

// Declaration and initialization with default values
int[][] matrix = new int[3][4];  // 3 rows, 4 columns

// Declaration and initialization with specific values
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Creating jagged arrays (rows with different lengths)
int[][] jaggedArray = new int[3][];
jaggedArray[0] = new int[2];  // First row has 2 columns
jaggedArray[1] = new int[4];  // Second row has 4 columns
jaggedArray[2] = new int[3]; // Third row has 3 columns
// Initializing jagged array with values
int[][] jaggedArray = {
{1, 2},
{3, 4, 5, 6},
{7, 8, 9}
};


### 32. How to traverse a 2D matrix in spiral form?
```java
public static List<Integer> spiralOrder(int[][] matrix) {
    List<Integer> result = new ArrayList<>();
    
    if (matrix == null || matrix.length == 0) {
        return result;
    }
    
    int rows = matrix.length;
    int cols = matrix[0].length;
    
    int top = 0, bottom = rows - 1;
    int left = 0, right = cols - 1;
    
    while (top <= bottom && left <= right) {
        // Traverse right
        for (int j = left; j <= right; j++) {
            result.add(matrix[top][j]);
        }
        top++;
        
        // Traverse down
        for (int i = top; i <= bottom; i++) {
            result.add(matrix[i][right]);
        }
        right--;
        
        // Traverse left (if there are still rows left)
        if (top <= bottom) {
            for (int j = right; j >= left; j--) {
                result.add(matrix[bottom][j]);
            }
            bottom--;
        }
        
        // Traverse up (if there are still columns left)
        if (left <= right) {
            for (int i = bottom; i >= top; i--) {
                result.add(matrix[i][left]);
            }
            left++;
        }
    }
    
    return result;
}
```

### 33. Search in a row-wise and column-wise sorted matrix.
```java
public static boolean searchMatrix(int[][] matrix, int target) {
    if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
        return false;
    }
    
    int rows = matrix.length;
    int cols = matrix[0].length;
    
    // Start from the top-right corner
    int row = 0;
    int col = cols - 1;
    
    while (row < rows && col >= 0) {
        if (matrix[row][col] == target) {
            return true;
        } else if (matrix[row][col] > target) {
            // The current value is larger, move left to find smaller values
            col--;
        } else {
            // The current value is smaller, move down to find larger values
            row++;
        }
    }
    
    return false;
}
```

### 34. Rotate a matrix by 90 degrees.
```java
public static void rotateMatrix(int[][] matrix) {
    int n = matrix.length;
    
    // Transpose the matrix (swap rows with columns)
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {
            int temp = matrix[i][j];
            matrix[i][j] = matrix[j][i];
            matrix[j][i] = temp;
        }
    }
    
    // Reverse each row
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n / 2; j++) {
            int temp = matrix[i][j];
            matrix[i][j] = matrix[i][n - 1 - j];
            matrix[i][n - 1 - j] = temp;
        }
    }
}
```

### 35. Find the transpose of a matrix.
```java
public static int[][] transposeMatrix(int[][] matrix) {
    int rows = matrix.length;
    int cols = matrix[0].length;
    
    int[][] transpose = new int[cols][rows];
    
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            transpose[j][i] = matrix[i][j];
        }
    }
    
    return transpose;
}
```

### 36. Multiply two matrices.
```java
public static int[][] multiplyMatrices(int[][] A, int[][] B) {
    int rowsA = A.length;
    int colsA = A[0].length;
    int colsB = B[0].length;
    
    // Resulting matrix will be of size rowsA x colsB
    int[][] result = new int[rowsA][colsB];
    
    for (int i = 0; i < rowsA; i++) {
        for (int j = 0; j < colsB; j++) {
            for (int k = 0; k < colsA; k++) {
                result[i][j] += A[i][k] * B[k][j];
            }
        }
    }
    
    return result;
}
```

### 37. Print all elements of a matrix in diagonal order.
```java
public static int[] findDiagonalOrder(int[][] matrix) {
    if (matrix == null || matrix.length == 0) {
        return new int[0];
    }
    
    int rows = matrix.length;
    int cols = matrix[0].length;
    int[] result = new int[rows * cols];
    
    int row = 0, col = 0;
    int direction = 1; // 1 = moving up, -1 = moving down
    
    for (int i = 0; i < rows * cols; i++) {
        result[i] = matrix[row][col];
        
        // Move in current diagonal direction
        row -= direction;
        col += direction;
        
        // Check if we went out of bounds and adjust
        if (row >= rows) { row = rows - 1; col += 2; direction = -direction; }
        if (col >= cols) { col = cols - 1; row += 2; direction = -direction; }
        if (row < 0) { row = 0; direction = -direction; }
        if (col < 0) { col = 0; direction = -direction; }
    }
    
    return result;
}
```

### 38. Find the number of islands in a 2D grid.
```java
public static int numIslands(char[][] grid) {
    if (grid == null || grid.length == 0) {
        return 0;
    }
    
    int rows = grid.length;
    int cols = grid[0].length;
    int count = 0;
    
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            if (grid[i][j] == '1') {
                count++;
                dfs(grid, i, j);
            }
        }
    }
    
    return count;
}

private static void dfs(char[][] grid, int row, int col) {
    int rows = grid.length;
    int cols = grid[0].length;
    
    // Check boundary conditions or if it's already visited
    if (row < 0 || col < 0 || row >= rows || col >= cols || grid[row][col] != '1') {
        return;
    }
    
    // Mark as visited
    grid[row][col] = '0';
    
    // Check all 4 adjacent cells
    dfs(grid, row + 1, col);
    dfs(grid, row - 1, col);
    dfs(grid, row, col + 1);
    dfs(grid, row, col - 1);
}
```

### 39. Implement the game of life.
```java
public static void gameOfLife(int[][] board) {
    if (board == null || board.length == 0) {
        return;
    }
    
    int rows = board.length;
    int cols = board[0].length;
    
    // State transitions: 
    // 0 -> 0: remains 0, no change needed
    // 1 -> 1: remains 1, no change needed
    // 0 -> 1: use code 2 (will convert to 1 in the final pass)
    // 1 -> 0: use code 3 (will convert to 0 in the final pass)
    
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            int liveNeighbors = countLiveNeighbors(board, i, j);
            
            // Apply Game of Life rules
            if (board[i][j] == 1 && (liveNeighbors < 2 || liveNeighbors > 3)) {
                board[i][j] = 3; // 1 -> 0
            } else if (board[i][j] == 0 && liveNeighbors == 3) {
                board[i][j] = 2; // 0 -> 1
            }
        }
    }
    
    // Final state conversion
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            if (board[i][j] == 2) {
                board[i][j] = 1;
            } else if (board[i][j] == 3) {
                board[i][j] = 0;
            }
        }
    }
}

private static int countLiveNeighbors(int[][] board, int row, int col) {
    int rows = board.length;
    int cols = board[0].length;
    int count = 0;
    
    // Check all 8 neighbors
    for (int i = Math.max(0, row - 1); i <= Math.min(rows - 1, row + 1); i++) {
        for (int j = Math.max(0, col - 1); j <= Math.min(cols - 1, col + 1); j++) {
            // Skip the cell itself
            if (i == row && j == col) {
                continue;
            }
            
            // Count live neighbors (1 or 3, since 3 was originally 1)
            if (board[i][j] == 1 || board[i][j] == 3) {
                count++;
            }
        }
    }
    
    return count;
}
```

### 40. Find the path in a maze.
```java
public static boolean findPath(int[][] maze, int[] start, int[] destination) {
    if (maze == null || maze.length == 0 || start[0] == destination[0] && start[1] == destination[1]) {
        return true;
    }
    
    int rows = maze.length;
    int cols = maze[0].length;
    boolean[][] visited = new boolean[rows][cols];
    
    return dfs(maze, visited, start[0], start[1], destination[0], destination[1]);
}

private static boolean dfs(int[][] maze, boolean[][] visited, int row, int col, int destRow, int destCol) {
    int rows = maze.length;
    int cols = maze[0].length;
    
    // Check if out of bounds, wall, or already visited
    if (row < 0 || row >= rows || col < 0 || col >= cols || maze[row][col] == 1 || visited[row][col]) {
        return false;
    }
    
    // Check if destination reached
    if (row == destRow && col == destCol) {
        return true;
    }
    
    // Mark as visited
    visited[row][col] = true;
    
    // Check all 4 directions
    if (dfs(maze, visited, row + 1, col, destRow, destCol) ||
        dfs(maze, visited, row - 1, col, destRow, destCol) ||
        dfs(maze, visited, row, col + 1, destRow, destCol) ||
        dfs(maze, visited, row, col - 1, destRow, destCol)) {
        return true;
    }
    
    return false;
}
```

## Advanced Array Techniques

### 41. Implement Dutch national flag algorithm (sort an array of 0s, 1s, and 2s).
```java
public static void sortColors(int[] nums) {
    int low = 0;        // Boundary for 0s
    int mid = 0;        // Current element
    int high = nums.length - 1;  // Boundary for 2s
    
    while (mid <= high) {
        switch (nums[mid]) {
            case 0:
                // Swap with the low boundary
                swap(nums, low, mid);
                low++;
                mid++;
                break;
            case 1:
                // Just move forward
                mid++;
                break;
            case 2:
                // Swap with the high boundary
                swap(nums, mid, high);
                high--;
                break;
        }
    }
}

private static void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}
```

### 42. Trap rainwater problem.
```java
public static int trap(int[] height) {
    if (height == null || height.length < 3) {
        return 0;
    }
    
    int left = 0;
    int right = height.length - 1;
    int leftMax = 0;
    int rightMax = 0;
    int water = 0;
    
    while (left < right) {
        // Water trapped depends on the smaller side
        if (height[left] < height[right]) {
            // If current height is higher than leftMax, update leftMax
            if (height[left] >= leftMax) {
                leftMax = height[left];
            } else {
                // Add trapped water for this position
                water += leftMax - height[left];
            }
            left++;
        } else {
            // If current height is higher than rightMax, update rightMax
            if (height[right] >= rightMax) {
                rightMax = height[right];
            } else {
                // Add trapped water for this position
                water += rightMax - height[right];
            }
            right--;
        }
    }
    
    return water;
}
```

### 43. Find the longest consecutive sequence in an array.
```java
public static int longestConsecutive(int[] nums) {
    if (nums == null || nums.length == 0) {
        return 0;
    }
    
    // Add all elements to a HashSet for O(1) lookups
    Set<Integer> numSet = new HashSet<>();
    for (int num : nums) {
        numSet.add(num);
    }
    
    int longestStreak = 0;
    
    for (int num : numSet) {
        // Only start counting if it's the beginning of a sequence
        if (!numSet.contains(num - 1)) {
            int currentNum = num;
            int currentStreak = 1;
            
            // Count consecutive elements
            while (numSet.contains(currentNum + 1)) {
                currentNum++;
                currentStreak++;
            }
            
            longestStreak = Math.max(longestStreak, currentStreak);
        }
    }
    
    return longestStreak;
}
```

### 44. Find the next permutation of an array of integers.
```java
public static void nextPermutation(int[] nums) {
    if (nums == null || nums.length <= 1) {
        return;
    }
    
    int i = nums.length - 2;
    
    // Find the first pair of adjacent elements a[i] and a[i+1] where a[i] < a[i+1]
    while (i >= 0 && nums[i] >= nums[i + 1]) {
        i--;
    }
    
    if (i >= 0) {
        int j = nums.length - 1;
        
        // Find the rightmost element nums[j] such that nums[j] > nums[i]
        while (nums[j] <= nums[i]) {
            j--;
        }
        
        // Swap elements at indices i and j
        swap(nums, i, j);
    }
    
    // Reverse the subarray starting at index i+1
    reverse(nums, i + 1, nums.length - 1);
}

private static void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}

private static void reverse(int[] nums, int start, int end) {
    while (start < end) {
        swap(nums, start, end);
        start++;
        end--;
    }
}
```

### 45. Find the minimum number of jumps to reach the end of an array.
```java
public static int jump(int[] nums) {
    if (nums == null || nums.length <= 1) {
        return 0;
    }
    
    int jumps = 0;
    int currentEnd = 0;
    int farthest = 0;
    
    // Don't need to check the last element, we're trying to reach it
    for (int i = 0; i < nums.length - 1; i++) {
        // Update the farthest reachable position
        farthest = Math.max(farthest, i + nums[i]);
        
        // If we've reached the current jump's end, need to jump again
        if (i == currentEnd) {
            jumps++;
            currentEnd = farthest;
        }
    }
    
    return jumps;
}
```

### 46. Stock buy and sell to maximize profit.
```java
// Best time to buy and sell stock (one transaction)
public static int maxProfit(int[] prices) {
    if (prices == null || prices.length <= 1) {
        return 0;
    }
    
    int minPrice = prices[0];
    int maxProfit = 0;
    
    for (int i = 1; i < prices.length; i++) {
        // Update the max profit if selling today yields a better profit
        if (prices[i] > minPrice) {
            maxProfit = Math.max(maxProfit, prices[i] - minPrice);
        }
        
        // Update the minimum price seen so far
        minPrice = Math.min(minPrice, prices[i]);
    }
    
    return maxProfit;
}

// Best time to buy and sell stock (multiple transactions)
public static int maxProfitMultipleTransactions(int[] prices) {
    if (prices == null || prices.length <= 1) {
        return 0;
    }
    
    int totalProfit = 0;
    
    for (int i = 1; i < prices.length; i++) {
        // If price is higher than previous day, add the difference to profit
        if (prices[i] > prices[i - 1]) {
            totalProfit += prices[i] - prices[i - 1];
        }
    }
    
    return totalProfit;
}
```

### 47. Find the median of two sorted arrays.
```java
public static double findMedianSortedArrays(int[] nums1, int[] nums2) {
    // Ensure nums1 is the smaller array to optimize the binary search
    if (nums1.length > nums2.length) {
        return findMedianSortedArrays(nums2, nums1);
    }
    
    int x = nums1.length;
    int y = nums2.length;
    
    int low = 0;
    int high = x;
    
    while (low <= high) {
        int partitionX = (low + high) / 2;
        int partitionY = (x + y + 1) / 2 - partitionX;
        
        int maxX = (partitionX == 0) ? Integer.MIN_VALUE : nums1[partitionX - 1];
        int minX = (partitionX == x) ? Integer.MAX_VALUE : nums1[partitionX];
        
        int maxY = (partitionY == 0) ? Integer.MIN_VALUE : nums2[partitionY - 1];
        int minY = (partitionY == y) ? Integer.MAX_VALUE : nums2[partitionY];
        
        if (maxX <= minY && maxY <= minX) {
            // Found the right partition
            
            // If total length is odd
            if ((x + y) % 2 != 0) {
                return Math.max(maxX, maxY);
            }
            
            // If total length is even
            return (Math.max(maxX, maxY) + Math.min(minX, minY)) / 2.0;
        } else if (maxX > minY) {
            // Need to go left in X
            high = partitionX - 1;
        } else {
            // Need to go right in X
            low = partitionX + 1;
        }
    }
    
    throw new IllegalArgumentException("Input arrays are not sorted");
}
```

### 48. Find the equilibrium index of an array.
```java
public static int equilibriumIndex(int[] nums) {
    if (nums == null || nums.length == 0) {
        return -1;
    }
    
    int totalSum = 0;
    for (int num : nums) {
        totalSum += num;
    }
    
    int leftSum = 0;
    
    for (int i = 0; i < nums.length; i++) {
        // Subtract current element from total sum to get right sum
        totalSum -= nums[i];
        
        // Check if left sum equals right sum
        if (leftSum == totalSum) {
            return i;
        }
        
        // Add current element to left sum
        leftSum += nums[i];
    }
    
    return -1;  // No equilibrium index found
}
```

### 49. Count inversions in an array.
```java
public static int countInversions(int[] arr) {
    if (arr == null || arr.length <= 1) {
        return 0;
    }
    
    int[] temp = new int[arr.length];
    return mergeSort(arr, temp, 0, arr.length - 1);
}

private static int mergeSort(int[] arr, int[] temp, int left, int right) {
    int invCount = 0;
    
    if (left < right) {
        int mid = (left + right) / 2;
        
        // Count inversions in left subarray
        invCount += mergeSort(arr, temp, left, mid);
        
        // Count inversions in right subarray
        invCount += mergeSort(arr, temp, mid + 1, right);
        
        // Count inversions during merge
        invCount += merge(arr, temp, left, mid, right);
    }
    
    return invCount;
}

private static int merge(int[] arr, int[] temp, int left, int mid, int right) {
    int i = left;     // Index for left subarray
    int j = mid + 1;  // Index for right subarray
    int k = left;     // Index for merged array
    int invCount = 0;
    
    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) {
            temp[k++] = arr[i++];
        } else {
            temp[k++] = arr[j++];
            
            // Count inversions when element from right subarray is smaller
            invCount += (mid - i + 1);
        }
    }
    
    // Copy remaining elements from left subarray
    while (i <= mid) {
        temp[k++] = arr[i++];
    }
    
    // Copy remaining elements from right subarray
    while (j <= right) {
        temp[k++] = arr[j++];
    }
    
    // Copy from temp back to original array
    for (i = left; i <= right; i++) {
        arr[i] = temp[i];
    }
    
    return invCount;
}
```

### 50. Container with most water problem.
```java
public static int maxArea(int[] height) {
    if (height == null || height.length < 2) {
        return 0;
    }
    
    int maxArea = 0;
    int left = 0;
    int right = height.length - 1;
    
    while (left < right) {
        // Calculate area using the minimum height between left and right boundaries
        int h = Math.min(height[left], height[right]);
        int w = right - left;
        maxArea = Math.max(maxArea, h * w);
        
        // Move the pointer that points to the shorter line
        if (height[left] < height[right]) {
            left++;
        } else {
            right--;
        }
    }
    
    return maxArea;
}