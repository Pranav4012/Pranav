#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void generateSortedArray(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        arr[i] = rand() % 10000;  // Fill with random numbers up to 10000
    }

    // Bubble Sort to sort the array
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

int linearSearch(int arr[], int n, int target) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == target) {
            return i;  // Return index if target is found
        }
    }
    return -1;  // Return -1 if target is not found
}

int binarySearch(int arr[], int n, int target) {
    int left = 0, right = n - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) {
            return mid;  // Return index if target is found
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1;  // Return -1 if target is not found
}

int main() {
    int n, target;

    printf("Enter the number of elements (up to 10000): ");
    scanf("%d", &n);

    int *arr = (int *)malloc(n * sizeof(int));
    generateSortedArray(arr, n);

    printf("Enter the target value to search: ");
    scanf("%d", &target);

    // Linear Search
    clock_t start = clock();
    int result = linearSearch(arr, n, target);
    clock_t end = clock();
    double time_taken = (double)(end - start) / CLOCKS_PER_SEC;
    if (result == -1) {
        printf("Linear Search: Not found\n");
    } else {
        printf("Linear Search: Found at index %d\n", result);
    }
    printf("Time taken for Linear Search: %f seconds\n", time_taken);

    // Binary Search
    start = clock();
    result = binarySearch(arr, n, target);
    end = clock();
    time_taken = (double)(end - start) / CLOCKS_PER_SEC;
    if (result == -1) {
        printf("Binary Search: Not found\n");
    } else {
        printf("Binary Search: Found at index %d\n", result);
    }
    printf("Time taken for Binary Search: %f seconds\n", time_taken);

    free(arr);
    return 0;
}
