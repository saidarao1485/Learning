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

3. Implement a C program to create a new directory named "Test" in the current directory?
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <sys/types.h>
int main()
{
    const char *dirname = "Test";
    if (mkdir(dirname, 0755) == 0)
    {
        printf("Directory '%s' created successfully.\n", dirname);
    }
    else
    {
        perror("Error creating directory");
    }
    return 0;
}

4. Write a C program to check if a file named "sample.txt" exists in the current directory?
#include <stdio.h>
int main()
{
    FILE *file;
    file = fopen("file.txt", "r");
    if (file)
    {
        printf("The file 'file.txt' exists in the current directory\n");
        fclose(file);
    }
    else
    {
        printf("The file 'file.txt' does NOT exist in the current directory\n");
    }
    return 0;
}

5. Develop a C program to rename a file from "oldname.txt" to "newname.txt"?
#include <stdio.h>
int main()
{
    char oldname[100], newname[100];
    printf("Enter the current filename: ");
    scanf("%s", oldname);
    printf("Enter the new filename: ");
    scanf("%s", newname);
    if (rename(oldname, newname) == 0)
    {
        printf("File renamed successfully from '%s' to '%s'\n", oldname, newname);
    }
    else
    {
        perror("Error renaming file");
    }
    return 0;
}

6. Implement a C program to delete a file named "delete_me.txt"?
#include <stdio.h>
int main()
{
    const char *filename = "delete_me.txt";
    if (remove(filename) == 0)
    {
        printf("File '%s' deleted successfully\n", filename);
    }
    else
    {
        perror("Error deleting file");
    }
    return 0;
}

7. Write a C program to copy the contents of one file to another?
#include <stdio.h>
int main()
{
    FILE *sourceFile, *destFile;
    char sourceName[100], destName[100];
    int ch;
    printf("Enter the source file name: ");
    scanf("%s", sourceName);
    printf("Enter the destination file name: ");
    scanf("%s", destName);
    sourceFile = fopen(sourceName, "r");
    if (sourceFile == NULL)
    {
        perror("Error opening source file");
        return 1;
    }
    destFile = fopen(destName, "w");
    if (destFile == NULL)
    {
        perror("Error opening destination file");
        fclose(sourceFile);
        return 1;
    }
    while ((ch = fgetc(sourceFile)) != EOF)
    {
        fputc(ch, destFile);
    }
    printf("Content copied successfully from '%s' to '%s'\n", sourceName, destName);
    fclose(sourceFile);
    fclose(destFile);
    return 0;
}

8. Develop a C program to move a file from one directory to another?
#include <stdio.h>
int main()
{
    char source[256];
    char destination[256];
    printf("Enter source file path: ");
    scanf("%s", source);
    printf("Enter destination file path: ");
    scanf("%s", destination);
    if (rename(source, destination) == 0)
    {
        printf("File moved successfully.\n");
    }
    else
    {
        perror("Error moving file");
    }
    return 0;
}

9. Implement a C program to list all files in the current directory?
/*#include <stdlib.h>
int main() {
    system("ls");
    return 0;
}*/
#include <stdio.h>
#include <dirent.h>
int main()
{
    struct dirent *entry;
    DIR *dir = opendir(".");
    if (dir == NULL)
    {
        perror("Unable to open current directory");
        return 1;
    }
    printf("Files in current directory:\n");
    while ((entry = readdir(dir)) != NULL)
    {
        if (entry->d_name[0] != '.')
        {
            printf("%s\n", entry->d_name);
        }
    }
    closedir(dir);
    return 0;
}

10. Write a C program to get the size of a file named "file.txt"?
#include <stdio.h>
int main()
{
    FILE *file = fopen("file.txt", "rb");
    if (file == NULL) {
        perror("Error opening file");
        return 1;
    }
    long size = 0;
    int ch;
    while ((ch = fgetc(file)) != EOF)
    {
        size++;
    }
    fclose(file);
    printf("Size of 'file.txt': %ld bytes\n", size);
    return 0;
}






```
