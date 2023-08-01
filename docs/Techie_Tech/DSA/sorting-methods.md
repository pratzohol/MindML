---
title: "Sorting Methods"
tags:
    - Algorithms
---

# Sorting Methods

## 1. Selection Sort

```cpp
void selectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        swap(arr[i], arr[minIndex]);
    }
}
```

- Time Complexity -> $O(n^2)$
- Space Complexity -> $O(1)$

## 2. Bubble Sort

```cpp
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}
```

- Time Complexity -> $O(n^2)$
- Space Complexity -> $O(1)$

## 3. Insertion Sort

```cpp
void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

- Time Complexity -> $O(n^2)$
- Space Complexity -> $O(1)$

## 4. Merge Sort

```cpp
void merge(vector<int> &arr, int low, int mid, int high) {
    vector<int> temp; 
    int left = low;      
    int right = mid + 1;  

    while (left <= mid && right <= high) {
        if (arr[left] <= arr[right]) {
            temp.push_back(arr[left]);
            left++;
        }
        else {
            temp.push_back(arr[right]);
            right++;
        }
    }

    while (left <= mid) {
        temp.push_back(arr[left]);
        left++;
    }

    while (right <= high) {
        temp.push_back(arr[right]);
        right++;
    }

    for (int i = low; i <= high; i++) {
        arr[i] = temp[i - low];
    }
}
```

```cpp
void mergeSort(vector<int> &arr, int low, int high) {
    if (low >= high) return;
    int mid = (low + high) / 2 ;
    mergeSort(arr, low, mid);  
    mergeSort(arr, mid + 1, high); 
    merge(arr, low, mid, high); 
}
```

- Time Complexity -> $O(n*logn)$  
- Space Complexity -> $O(n)$
- Can be done in O(1) space complexity

## 5. Quick Sort

```cpp
int partition(vector<int> &arr, int low, int high) {
    int pivot = arr[low];
    int i = low;
    int j = high;

    while (i < j) {
        while (arr[i] <= pivot && i <= high - 1) {
            i++;
        }

        while (arr[j] > pivot && j >= low + 1) {
            j--;
        }
        if (i < j) swap(arr[i], arr[j]);
    }
    swap(arr[low], arr[j]);
    return j;
}
```
```cpp
void qs(vector<int> &arr, int low, int high) {
    if (low < high) {
        int pIndex = partition(arr, low, high);
        qs(arr, low, pIndex - 1);
        qs(arr, pIndex + 1, high);
    }
}
```
```cpp
vector<int> quickSort(vector<int> arr) {
    qs(arr, 0, arr.size() - 1);
    return arr;
}
```

- Avg. Time Complexity -> $O(n*logn)$
- Worst Time Complexity -> $O(n^2)$  
- Space Complexity -> $O(1)$
- Auxiliary Space Complexity -> $O(n)$ (for recursive calls on stack) (on avg., it will be $O(logn)$ but in worst case it will be $O(n)$)
