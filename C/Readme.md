## Programs on C
```c
1. Write a program to check if elements of an array are distinct or not.
#include <stdio.h>
int main()
{
    int n, i, j;
    int isDistinct = 1;
    printf("Enter the number of elements in the array: ");
    scanf("%d", &n);
    int arr[n];
    printf("Enter %d elements:\n", n);
    for (i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
    }
    for (i = 0; i < n - 1; i++)
    {
        for (j = i + 1; j < n; j++)
        {
            if (arr[i] == arr[j])
            {
                isDistinct = 0;
                break;
            }
        }
        if (!isDistinct)
            break;
    }
    if (isDistinct)
        printf("All elements are distinct\n");
    else
        printf("Array contains duplicate elements\n");

    return 0;
}

2. Program to access dynamically allocate a 2-D array using a pointer to an array and array of pointers.
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int rows = 3, cols = 4;
    int *arr1[3];
    for (int i = 0; i < rows; i++)
    {
        arr1[i] = (int *)malloc(cols * sizeof(int));
    }
    printf("Using array of pointers:\n");
    for (int i = 0; i < rows; i++)
    {
        for (int j = 0; j < cols; j++)
        {
            arr1[i][j] = i * cols + j;
            printf("%d ", arr1[i][j]);
        }
        printf("\n");
    }
    for (int i = 0; i < rows; i++)
    {
        free(arr1[i]);
    }
    int (*arr2)[4];
    arr2 = (int (*)[4])malloc(rows * sizeof(*arr2));
    printf("\nUsing pointer to an array:\n");
    for (int i = 0; i < rows; i++)
    {
        for (int j = 0; j < cols; j++)
        {
            arr2[i][j] = i * cols + j;
            printf("%d ", arr2[i][j]);
        }
        printf("\n");
    }
    free(arr2);
    return 0;
}

3. Write a C program to reverse order of words in a given string.
#include <stdio.h>
int main() {
    char str[100];
    int i = 0, start, end;
    printf("Enter a string: ");
    while ((str[i] = getchar()) != '\n') {
        i++;
    }
    str[i] = '\0';
    end = i - 1;
    printf("Reversed string: ");
    while (end >= 0) {
        while (end >= 0 && str[end] == ' ')
            end--;
        if (end < 0)
            break;
        start = end;
        while (start >= 0 && str[start] != ' ')
            start--;
        for (i = start + 1; i <= end; i++)
            putchar(str[i]);
        putchar(' ');
        end = start - 1;
    }
    printf("\n");
    return 0;
}

4. Write a program to partition an array such that all the negative numbers are on the left side of the array and positive numbers on the right side.
#include <stdio.h>
#include <stdlib.h>
void sortArray(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        for (int j = 0; j < n-i-1; j++) {
            if (arr[j] > arr[j+1]) {
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}
void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
}
int main()
{
    int n;
    printf("Enter number of elements: ");
    scanf("%d", &n);
    int arr[n];
    printf("Enter %d elements:\n", n);
    for (int i = 0; i < n; i++)
        scanf("%d", &arr[i]);
    printf("Original array:\n");
    printArray(arr, n);
    sortArray(arr, n);
    printf("Array after sorting (negatives left, positives right):\n");
    printArray(arr, n);

    return 0;
}

5. Write a program to rotate a matrix 90 degrees clockwise in C. 
#include <stdio.h>

#define N 3
void printMatrix(int mat[N][N]) {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            printf("%d ", mat[i][j]);
        }
        printf("\n");
    }
}
void rotate90Clockwise(int mat[N][N]) {
    for (int i = 0; i < N; i++) {
        for (int j = i; j < N; j++) {
            int temp = mat[i][j];
            mat[i][j] = mat[j][i];
            mat[j][i] = temp;
        }
    }
    for (int i = 0; i < N; i++) {
        for (int j = 0, k = N - 1; j < k; j++, k--) {
            int temp = mat[i][j];
            mat[i][j] = mat[i][k];
            mat[i][k] = temp;
        }
    }
}
int main() {
    int mat[N][N] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };
    printf("Original Matrix:\n");
    printMatrix(mat);
    rotate90Clockwise(mat);
    printf("\nMatrix After 90 Degree Rotation (Clockwise):\n");
    printMatrix(mat);
    return 0;
}




```
