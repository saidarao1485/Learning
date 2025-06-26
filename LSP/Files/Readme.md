#
##
```c
//Write a C program to create a new text file and write "Hello, World!" to it?
#include <stdio.h>
int main() {
    char filename[100];
    char text[1000];
    FILE *file;
    printf("Enter the file name: ");
    scanf("%[^\n]", filename);
    getchar(); 
    file = fopen(filename, "w");
    if (file == NULL) {
        printf("Error creating file.\n");
        return 1;
    }
    printf("Enter text to write to the file: ");
    scanf("%[^\n]", text);
    fprintf(file, "%s\n", text);
    printf("Text written to '%s' successfully\n", filename);
    fclose(file);
    return 0;
}
```
