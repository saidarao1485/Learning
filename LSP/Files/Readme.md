# Programs on Files
```c
1. Write a C program to create a new text file and write "Hello, World!" to it?
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
2. Develop a C program to open an existing text file and display its contents?
#include <stdio.h>
#include <stdlib.h>
int main() {
    char filename[100];
    char ch;
    FILE *file;
    printf("Enter the name of the file to open: ");
    scanf("%[^\n]s", filename);
    file = fopen(filename, "r");
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }
    printf("Contents of '%s':\n", filename);
    while ((ch = fgetc(file)) != EOF) {
        putchar(ch);
    }
    fclose(file);
    return 0;
}

```
