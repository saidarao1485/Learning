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




```
