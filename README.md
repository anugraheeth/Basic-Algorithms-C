# All major searching and sorting algorithms in C.

---

# Sorting and Searching Algorithms in C

This document explains various sorting and searching algorithms implemented in C. These are widely used in computing to organize data and quickly retrieve values.

---

## Table of Contents
- [Sorting Algorithms](#sorting-algorithms)
  - [1. Bubble Sort](#bubble-sort)
  - [2. Selection Sort](#selection-sort)
  - [3. Insertion Sort](#insertion-sort)
  - [4. Merge Sort](#merge-sort)
  - [5. Quick Sort](#quick-sort)
  - [6. Heap Sort](#heap-sort)
  - [7. Radix Sort](#radix-sort)
  - [8. Bucket Sort](#bucket-sort)
  - [9. Shell Sort](#shell-sort)
  - [10. Counting Sort](#counting-sort)
- [Searching Algorithms](#searching-algorithms)
  - [1. Linear Search](#linear-search)
  - [2. Binary Search](#binary-search)
  - [3. Jump Search](#jump-search)
  - [4. Exponential Search](#exponential-search)
  - [5. Interpolation Search](#interpolation-search)
  - [6. Fibonacci Search](#fibonacci-search)

---

## Sorting Algorithms

### 1. Bubble Sort

**Algorithm:**
Bubble Sort compares adjacent elements and swaps them if they are in the wrong order. The process repeats until the array is sorted.

**Time Complexity:**
- Best: O(n)
- Average: O(n^2)
- Worst: O(n^2)

**Code:**
```c
void bubbleSort(int arr[], int n) {
    int i, j, temp;
    for (i = 0; i < n-1; i++) {
        for (j = 0; j < n-i-1; j++) {
            if (arr[j] > arr[j+1]) {
                temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}
```

### 2. Selection Sort

**Algorithm:**
Selection Sort repeatedly finds the minimum element from the unsorted portion and places it at the beginning.

**Time Complexity:**
- Best: O(n^2)
- Average: O(n^2)
- Worst: O(n^2)

**Code:**
```c
void selectionSort(int arr[], int n) {
    int i, j, minIdx, temp;
    for (i = 0; i < n-1; i++) {
        minIdx = i;
        for (j = i+1; j < n; j++) {
            if (arr[j] < arr[minIdx]) {
                minIdx = j;
            }
        }
        temp = arr[minIdx];
        arr[minIdx] = arr[i];
        arr[i] = temp;
    }
}
```

### 3. Insertion Sort

**Algorithm:**
Insertion Sort builds the sorted array one item at a time, placing elements at their correct position by comparing them to the already sorted subarray.

**Time Complexity:**
- Best: O(n)
- Average: O(n^2)
- Worst: O(n^2)

**Code:**
```c
void insertionSort(int arr[], int n) {
    int i, key, j;
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}
```

### 4. Merge Sort

**Algorithm:**
Merge Sort divides the array into two halves, recursively sorts them, and then merges the two halves.

**Time Complexity:**
- Best: O(n log n)
- Average: O(n log n)
- Worst: O(n log n)

**Code:**
```c
void merge(int arr[], int l, int m, int r) {
    int n1 = m - l + 1;
    int n2 = r - m;
    int L[n1], R[n2];
    for (int i = 0; i < n1; i++) L[i] = arr[l + i];
    for (int j = 0; j < n2; j++) R[j] = arr[m + 1 + j];
    int i = 0, j = 0, k = l;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) arr[k++] = L[i++];
        else arr[k++] = R[j++];
    }
    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);
        merge(arr, l, m, r);
    }
}
```

### 5. Quick Sort

**Algorithm:**
Quick Sort selects a pivot element, partitions the array around it, and then recursively applies this process to the subarrays.

**Time Complexity:**
- Best: O(n log n)
- Average: O(n log n)
- Worst: O(n^2)

**Code:**
```c
int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
    int temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;
    return i + 1;
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```

### 6. Heap Sort

**Algorithm:**
Heap Sort uses a binary heap to organize the elements and repeatedly extracts the maximum element.

**Time Complexity:**
- Best: O(n log n)
- Average: O(n log n)
- Worst: O(n log n)

**Code:**
```c
void heapify(int arr[], int n, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < n && arr[left] > arr[largest])
        largest = left;

    if (right < n && arr[right] > arr[largest])
        largest = right;

    if (largest != i) {
        int swap = arr[i];
        arr[i] = arr[largest];
        arr[largest] = swap;
        heapify(arr, n, largest);
    }
}

void heapSort(int arr[], int n) {
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    for (int i = n - 1; i >= 0; i--) {
        int temp = arr[0];
        arr[0] = arr[i];
        arr[i] = temp;
        heapify(arr, i, 0);
    }
}
```

### 7. Radix Sort

**Algorithm:**
Radix Sort processes digits of each element starting from the least significant digit to the most significant digit.

**Time Complexity:**
- Best: O(nk)
- Average: O(nk)
- Worst: O(nk)

**Code:**
```c
int getMax(int arr[], int n) {
    int max = arr[0];
    for (int i = 1; i < n; i++)
        if (arr[i] > max)
            max = arr[i];
    return max;
}

void countSort(int arr[], int n, int exp) {
    int output[n];
    int count[10] = {0};

    for (int i = 0; i < n; i++)
        count[(arr[i] / exp) % 10]++;

    for (int i = 1; i < 10; i++)
        count[i] += count[i - 1];

    for (int i = n - 1; i >= 0; i--) {
        output[count[(arr[i] / exp) % 10] - 1] = arr[i];
        count[(arr[i] / exp) % 10]--;
    }

    for (int i = 0; i < n; i++)
        arr[i] = output[i];
}

void radixSort(int arr[], int n) {
    int max = getMax(arr, n);
    for (int exp = 1; max / exp > 0; exp *= 10)
        countSort(arr, n, exp);
}
```

### 8. Bucket Sort

**Algorithm:**
Bucket Sort divides the elements into different buckets, sorts each bucket, and then merges them.

**

Time Complexity:**
- Best: O(n+k)
- Average: O(n+k)
- Worst: O(n^2)

**Code:**
```c
void bucketSort(float arr[], int n) {
    vector<float> buckets[n];
    for (int i = 0; i < n; i++) {
        int idx = n * arr[i];
        buckets[idx].push_back(arr[i]);
    }
    for (int i = 0; i < n; i++)
        sort(buckets[i].begin(), buckets[i].end());

    int idx = 0;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < buckets[i].size(); j++)
            arr[idx++] = buckets[i][j];
}
```

### 9. Shell Sort

**Algorithm:**
Shell Sort is an optimized version of Insertion Sort, using a gap sequence to sort elements that are far apart.

**Time Complexity:**
- Best: O(n log n)
- Average: O(n(log n)^2)
- Worst: O(n(log n)^2)

**Code:**
```c
void shellSort(int arr[], int n) {
    for (int gap = n / 2; gap > 0; gap /= 2) {
        for (int i = gap; i < n; i++) {
            int temp = arr[i];
            int j;
            for (j = i; j >= gap && arr[j - gap] > temp; j -= gap) {
                arr[j] = arr[j - gap];
            }
            arr[j] = temp;
        }
    }
}
```

### 10. Counting Sort

**Algorithm:**
Counting Sort counts the occurrences of each value and uses this information to place elements in the sorted order.

**Time Complexity:**
- Best: O(n+k)
- Average: O(n+k)
- Worst: O(n+k)

**Code:**
```c
void countingSort(int arr[], int n) {
    int output[n];
    int max = arr[0];
    for (int i = 1; i < n; i++)
        if (arr[i] > max)
            max = arr[i];

    int count[max + 1];
    for (int i = 0; i <= max; i++)
        count[i] = 0;

    for (int i = 0; i < n; i++)
        count[arr[i]]++;

    for (int i = 1; i <= max; i++)
        count[i] += count[i - 1];

    for (int i = n - 1; i >= 0; i--) {
        output[count[arr[i]] - 1] = arr[i];
        count[arr[i]]--;
    }

    for (int i = 0; i < n; i++)
        arr[i] = output[i];
}
```

---

## Searching Algorithms

### 1. Linear Search

**Algorithm:**
Linear Search checks each element in the array until the desired element is found.

**Time Complexity:**
- Best: O(1)
- Average: O(n)
- Worst: O(n)

**Code:**
```c
int linearSearch(int arr[], int n, int x) {
    for (int i = 0; i < n; i++)
        if (arr[i] == x)
            return i;
    return -1;
}
```

### 2. Binary Search

**Algorithm:**
Binary Search divides the sorted array into two halves and repeatedly compares the middle element.

**Time Complexity:**
- Best: O(1)
- Average: O(log n)
- Worst: O(log n)

**Code:**
```c
int binarySearch(int arr[], int l, int r, int x) {
    if (r >= l) {
        int mid = l + (r - l) / 2;
        if (arr[mid] == x)
            return mid;
        if (arr[mid] > x)
            return binarySearch(arr, l, mid - 1, x);
        return binarySearch(arr, mid + 1, r, x);
    }
    return -1;
}
```

### 3. Jump Search

**Algorithm:**
Jump Search divides the array into blocks and jumps ahead, then does a linear search within the block.

**Time Complexity:**
- Best: O(1)
- Average: O(√n)
- Worst: O(√n)

**Code:**
```c
int jumpSearch(int arr[], int n, int x) {
    int step = sqrt(n);
    int prev = 0;
    while (arr[min(step, n)-1] < x) {
        prev = step;
        step += sqrt(n);
        if (prev >= n)
            return -1;
    }
    for (int i = prev; i < min(step, n); i++)
        if (arr[i] == x)
            return i;
    return -1;
}
```

### 4. Exponential Search

**Algorithm:**
Exponential Search finds a range where the target may lie, then uses binary search.

**Time Complexity:**
- Best: O(1)
- Average: O(log n)
- Worst: O(log n)

**Code:**
```c
int exponentialSearch(int arr[], int n, int x) {
    if (arr[0] == x)
        return 0;
    int i = 1;
    while (i < n && arr[i] <= x)
        i *= 2;
    return binarySearch(arr, i/2, min(i, n-1), x);
}
```

### 5. Interpolation Search

**Algorithm:**
Interpolation Search improves binary search by guessing the position based on the value to be searched.

**Time Complexity:**
- Best: O(1)
- Average: O(log log n)
- Worst: O(n)

**Code:**
```c
int interpolationSearch(int arr[], int n, int x) {
    int lo = 0, hi = (n - 1);
    while (lo <= hi && x >= arr[lo] && x <= arr[hi]) {
        if (lo == hi) {
            if (arr[lo] == x)
                return lo;
            return -1;
        }
        int pos = lo + (((double)(hi - lo) / (arr[hi] - arr[lo])) * (x - arr[lo]));
        if (arr[pos] == x)
            return pos;
        if (arr[pos] < x)
            lo = pos + 1;
        else
            hi = pos - 1;
    }
    return -1;
}
```

### 6. Fibonacci Search

**Algorithm:**
Fibonacci Search uses a Fibonacci sequence to divide the array and search for the target.

**Time Complexity:**
- Best: O(1)
- Average: O(log n)
- Worst: O(log n)

**Code:**
```c
int min(int x, int y) { return (x <= y) ? x : y; }

int fibonacciSearch(int arr[], int x, int n) {
    int fib2 = 0;
    int fib1 = 1;
    int fibM = fib2 + fib1;

    while (fibM < n) {
        fib2 = fib1;
        fib1 = fibM;
        fibM = fib2 + fib1;
    }

    int offset = -1;

    while (fibM > 1) {
        int i = min(offset + fib2, n - 1);
        if (arr[i] < x) {
            fibM = fib1;
            fib1 = fib2;
            fib2 = fibM - fib1;
            offset = i;
        } else if (arr[i] > x) {
            fibM = fib2;
            fib1 = fib1 - fib2;
            fib2 = fibM - fib1;
        } else
            return i;
    }

    if (fib1 && arr[offset + 1] == x)
        return offset + 1;

    return -1;
}
```

---

