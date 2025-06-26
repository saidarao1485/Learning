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

11. Develop a C program to check if a directory named "Test" exists in the current directory?
#include <stdio.h>
#include <dirent.h>
int main()
{
    DIR *dir = opendir("Test");
    if (dir)
    {
        printf("Directory 'Test' exists\n");
        closedir(dir);
    }
    else
    {
        printf("Directory 'Test' does NOT exist\n");
    }
    return 0;
}

12. Implement a C program to create a new directory named "Backup" in the parent directory?
#include <stdio.h>
#include <sys/stat.h>
#include <sys/types.h>
int main()
{
    const char *dirPath = "../Backup";
    if (mkdir(dirPath, 0755) == 0)
    {
        printf("Directory 'Backup' created successfully in the parent directory\n");
    }
    else
    {
        perror("Error creating directory");
        return 1;
    }
    return 0;
}

13. Write a C program to recursively list all files and directories in a given directory?
#include <stdio.h>
#include <dirent.h>
#include <string.h>
#include <sys/stat.h>
void listFiles(const char *path)
{
    struct dirent *entry;
    DIR *dir = opendir(path);
    if (dir == NULL) {
        perror("Unable to open directory");
        return;
    }
    while ((entry = readdir(dir)) != NULL)
    {
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;
        char fullPath[512];
        snprintf(fullPath, sizeof(fullPath), "%s/%s", path, entry->d_name);
        printf("%s\n", fullPath);

        struct stat info;
        if (stat(fullPath, &info) == 0 && S_ISDIR(info.st_mode)) {
            listFiles(fullPath);
        }
    }
    closedir(dir);
}
int main()
{
    char path[256];
    printf("Enter directory path: ");
    scanf("%s", path);
    listFiles(path);
    return 0;
}

14. Develop a C program to delete all files in a directory named "Temp"?
#include <stdio.h>
#include <dirent.h>
#include <string.h>
#include <unistd.h>
#include <sys/stat.h>
#include <errno.h>
int main()
{
    DIR *dir;
    struct dirent *entry;
    char path[512];
    dir = opendir("Temp");
    if (dir == NULL)
    {
        if (mkdir("Temp", 0777) == -1)
        {
            perror("Failed to create Temp directory");
            return 1;
        }
        else
        {
            printf("Temp directory was missing, so it has been created.\n");
            return 0; // Nothing to delete, so exit
        }
    }
    while ((entry = readdir(dir)) != NULL)
    {
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;

        snprintf(path, sizeof(path), "Temp/%s", entry->d_name);
        if (remove(path) == 0)
        {
            printf("Deleted: %s\n", path);
        }
        else
        {
            perror("Failed to delete");
        }
    }
    closedir(dir);
    return 0;
}

15. Implement a C program to count the number of lines in a file named "file.txt"?
#include <stdio.h>
int main()
{
    FILE *file = fopen("file.txt", "r");
    if (file == NULL)
    {
        perror("Error opening file");
        return 1;
    }
    int ch;
    int lines = 0;
    while ((ch = fgetc(file)) != EOF)
    {
        if (ch == '\n')
	{
            lines++;
    }
    }
    fclose(file);
    printf("Number of lines in file.txt: %d\n", lines);
    return 0;
}

16. Write a C program to append "Goodbye!" to the end of an existing file named "message.txt"?
#include <stdio.h>
int main()
{
    FILE *file = fopen("file.txt", "a");
    if (file == NULL)
    {
        perror("Error opening file");
        return 1;
    }
    fprintf(file, "Goodbye!\n");
    fclose(file);
    printf("Text appended to file.txt successfully\n");
    return 0;
}

17. Implement a C program to change the permissions of a file named "file.txt" to read-only?
#include <stdio.h>
#include <sys/stat.h>
int main()
{
    const char *filename = "file.txt";
    if (chmod(filename, 0444) == 0) 
    {
        printf("Permissions changed to read-only for %s\n", filename);
    }
    else
    {
        perror("Error changing permissions");
        return 1;
    }
    return 0;
}

18. Write a C program to change the ownership of a file named "file.txt" to the user "user1"?
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pwd.h>
#include <sys/types.h>
#include <sys/stat.h>
int main()
{
    const char *filename = "file.txt";
    const char *username = "user1";
    struct passwd *pw = getpwnam(username);
    if (pw == NULL)
    {
        fprintf(stderr, "User '%s' not found\n", username);
        return 1;
    }
    uid_t uid = pw->pw_uid;
    gid_t gid = pw->pw_gid;
    if (chown(filename, uid, gid) == 0)
    {
        printf("Ownership of '%s' changed to user '%s'\n", filename, username);
    } else {
        perror("Error changing ownership");
        return 1;
    }
    return 0;
}

19. Develop a C program to get the last modified timestamp of a file named "file.txt"?
#include <stdio.h>
#include <sys/stat.h>
#include <time.h>
int main()
{
    const char *filename = "file.txt";
    struct stat fileStat;
    if (stat(filename, &fileStat) != 0) {
        perror("Error getting file information");
        return 1;
    }
    printf("Last modified time of '%s': %s", filename, ctime(&fileStat.st_mtime));
    return 0;
}

20. Implement a C program to create a temporary file and write some data to it?
#include <stdio.h>
#include <stdlib.h>
int main()
{
    FILE *tempFile = tmpfile();
    if (tempFile == NULL)
    {
        perror("Failed to create temporary file");
        return 1;
    }
    const char *data = "This is some sample data written to a temporary file\n";
    if (fputs(data, tempFile) == EOF)
    {
        perror("Failed to write to temporary file");
        fclose(tempFile);
        return 1;
    }
    rewind(tempFile);
    printf("Data written to temporary file:\n");
    char buffer[256];
    while (fgets(buffer, sizeof(buffer), tempFile) != NULL)
    {
        fputs(buffer, stdout);
    }
    fclose(tempFile);
    return 0;
}



```
