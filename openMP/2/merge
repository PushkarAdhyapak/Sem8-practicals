#include <iostream>
#include <vector>
#include <cstdlib>  // For rand()
#include <ctime>    // For clock()
#include <omp.h>    // OpenMP

// Sequential Merge Sort
void mergeSortSequential(int* arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSortSequential(arr, left, mid);
        mergeSortSequential(arr, mid + 1, right);

        // Merge the sorted halves
        int temp[right - left + 1];
        int i = left, j = mid + 1, k = 0;

        while (i <= mid && j <= right) {
            if (arr[i] <= arr[j]) {
                temp[k++] = arr[i++];
            } else {
                temp[k++] = arr[j++];
            }
        }

        while (i <= mid) {
            temp[k++] = arr[i++];
        }

        while (j <= right) {
            temp[k++] = arr[j++];
        }

        for (int p = 0; p < k; p++) {
            arr[left + p] = temp[p];
        }
    }
}

// Parallel Merge Sort using OpenMP
void mergeSortParallel(int* arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;

        #pragma omp parallel sections
        {
            #pragma omp section
            mergeSortParallel(arr, left, mid);
            #pragma omp section
            mergeSortParallel(arr, mid + 1, right);
        }

        // Merge the sorted halves
        int temp[right - left + 1];
        int i = left, j = mid + 1, k = 0;

        while (i <= mid && j <= right) {
            if (arr[i] <= arr[j]) {
                temp[k++] = arr[i++];
            } else {
                temp[k++] = arr[j++];
            }
        }

        while (i <= mid) {
            temp[k++] = arr[i++];
        }

        while (j <= right) {
            temp[k++] = arr[j++];
        }

        for (int p = 0; p < k; p++) {
            arr[left + p] = temp[p];
        }
    }
}

int main() {
    const int size = 1000;
    int arr[size];
    for (int i = 0; i < size; i++) {
        arr[i] = rand() % 1000;  // Random numbers between 0 and 999
    }

    clock_t startSeqMerge = clock();
    mergeSortSequential(arr, 0, size - 1);
    clock_t endSeqMerge = clock();
    double timeSeqMerge = double(endSeqMerge - startSeqMerge) / CLOCKS_PER_SEC;

    clock_t startParMerge = clock();
    mergeSortParallel(arr, 0, size - 1);
    clock_t endParMerge = clock();
    double timeParMerge = double(endParMerge - startParMerge) / CLOCKS_PER_SEC;

    // Print execution times
    std::cout << "Sequential Merge Sort Time: " << timeSeqMerge << " seconds" << std::endl;
    std::cout << "Parallel Merge Sort Time: " << timeParMerge << " seconds" << std::endl;

    return 0;
}

