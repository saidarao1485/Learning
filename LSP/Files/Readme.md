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

21. Write a C program to check if a given path refers to a file or a directory?
#include <stdio.h>
#include <sys/stat.h>
#include <stdlib.h>
#include<string.h>
int main()
{
    char path[1024];
    struct stat path_stat;
    printf("Enter the path: ");
    fgets(path, sizeof(path), stdin);
    size_t len = strlen(path);
    if (len > 0 && path[len - 1] == '\n')
    {
        path[len - 1] = '\0';
    }
    if (stat(path, &path_stat) != 0)
    {
        perror("stat");
        return 1;
    }
    if (S_ISREG(path_stat.st_mode))
    {
        printf("The path refers to a regular file\n");
    }
    else if (S_ISDIR(path_stat.st_mode))
    {
        printf("The path refers to a directory\n");
    }
    else
    {
        printf("The path is neither a regular file nor a directory\n");
    }
    return 0;
}

22. Develop a C program to create a hard link named "hardlink.txt" to a file named "source.txt"? 
#include <unistd.h>
int main()
{
    const char *source = "source.txt";
    const char *linkname = "hardlink.txt";
    FILE *srcFile = fopen(source, "w");
    if (srcFile == NULL)
    {
        perror("Error creating source.txt");
        return 1;
    }
    fprintf(srcFile, "This is the source file\n");
    fclose(srcFile);
    if (link(source, linkname) == 0)
    {
        printf("Hard link '%s' created to '%s'\n", linkname, source);
    }
    else
    {
        perror("Error creating hard link");
        return 1;
    }
    return 0;
}

23. Implement a C program to read and display the contents of a CSV file named "data.csv"?
#include <stdio.h>
#include <stdlib.h>
int main()
{
    FILE *file;
    char buffer[1024];
    file = fopen("data.csv", "w");
    if (file == NULL)
    {
        perror("Error creating file");
        return 1;
    }
    fprintf(file, "Name,Age,Country\n");
    fprintf(file, "Alice,30,USA\n");
    fprintf(file, "Bob,25,Canada\n");
    fprintf(file, "Charlie,28,UK\n");
    fclose(file);
    file = fopen("data.csv", "r");
    if (file == NULL)
    {
        perror("Error opening file");
        return 1;
    }
    printf("Contents of data.csv:\n");
    while (fgets(buffer, sizeof(buffer), file))
    {
        printf("%s", buffer);
    }
    fclose(file);
    return 0;
}

24. Write a C program to get the absolute path of the current working directory?
#include <stdio.h>
#include <unistd.h>
#include <limits.h>
int main()
{
    char cwd[PATH_MAX];
    if (getcwd(cwd, sizeof(cwd)) != NULL)
    {
        printf("Current working directory: %s\n", cwd);
    }
    else
    {
        perror("getcwd() error");
        return 1;
    }
    return 0;
}

25. Develop a C program to get the size of a directory named "Linux"?
#include <stdio.h>
#include <dirent.h>
#include <sys/stat.h>
#include <string.h>
int main()
{
    const char *folder = "dest_dir";
    struct dirent *entry;
    struct stat file_stat;
    char filepath[1024];
    long long total_size = 0;
    DIR *dir = opendir(folder);
    if (dir == NULL)
    {
        perror("Unable to open directory");
        return 1;
    }
    while ((entry = readdir(dir)) != NULL)
    {
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;
        snprintf(filepath, sizeof(filepath), "%s/%s", folder, entry->d_name);
        if (stat(filepath, &file_stat) == 0 && S_ISREG(file_stat.st_mode))
	{
            total_size += file_stat.st_size;
        }
    }
    closedir(dir);
    printf("Total size of files in '%s': %lld bytes\n", folder, total_size);
    return 0;
}

26. Implement a C program to recursively copy all files and directories from one directory to another?
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <sys/stat.h>
#include <unistd.h>
#include <fcntl.h>
#define BUFFER_SIZE 4096
void create_file(const char *path, const char *content)
{
    FILE *f = fopen(path, "w");
    if (f)
    {
        fputs(content, f);
        fclose(f);
    }
    else
    {
        perror("Error creating file");
    }
}
void copy_file(const char *src, const char *dest)
{
    char buffer[BUFFER_SIZE];
    ssize_t bytes;
    int src_fd = open(src, O_RDONLY);
    int dest_fd = open(dest, O_WRONLY | O_CREAT | O_TRUNC, 0644);
    if (src_fd < 0 || dest_fd < 0)
    {
        perror("Error copying file");
        return;
    }
    while ((bytes = read(src_fd, buffer, BUFFER_SIZE)) > 0)
    {
        write(dest_fd, buffer, bytes);
    }
    close(src_fd);
    close(dest_fd);
}
void copy_directory(const char *src, const char *dest)
{
    mkdir(dest, 0755);
    DIR *dir = opendir(src);
    struct dirent *entry;
    if (!dir) return;
    while ((entry = readdir(dir)) != NULL)
    {
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;
        char src_path[1024], dest_path[1024];
        snprintf(src_path, sizeof(src_path), "%s/%s", src, entry->d_name);
        snprintf(dest_path, sizeof(dest_path), "%s/%s", dest, entry->d_name);
        struct stat st;
        stat(src_path, &st);
        if (S_ISDIR(st.st_mode))
	{
            copy_directory(src_path, dest_path);
        }
	else if (S_ISREG(st.st_mode))
	{
            copy_file(src_path, dest_path);
        }
    }
    closedir(dir);
}
int main()
{
    mkdir("source_dir", 0755);
    mkdir("source_dir/subfolder", 0755);
    create_file("source_dir/file1.txt", "File 1\n");
    create_file("source_dir/subfolder/nested.txt", "Nested File\n");
    copy_directory("source_dir", "destination_dir");
    printf("Files and directories copied successfully\n");
    return 0;
}

27. Write a C program to get the number of files in a directory named "Images"?
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <dirent.h>
#include <string.h>
void create_file(const char *path, const char *content) {
    FILE *file = fopen(path, "w");
    if (file) {
        fputs(content, file);
        fclose(file);
    } else {
        perror("Error creating file");
    }
}
int main() {
    const char *dir_name = "Images";
    char file1[256], file2[256];
    if (mkdir(dir_name, 0755) == -1) {
    }
    snprintf(file1, sizeof(file1), "%s/file1.jpg", dir_name);
    snprintf(file2, sizeof(file2), "%s/file2.png", dir_name);
    create_file(file1, "test");
    create_file(file2, "test");
    DIR *dir = opendir(dir_name);
    struct dirent *entry;
    struct stat statbuf;
    char path[512];
    int count = 0;
    if (!dir) {
        perror("Unable to open directory");
        return 1;
    }
    while ((entry = readdir(dir)) != NULL) {
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;
        snprintf(path, sizeof(path), "%s/%s", dir_name, entry->d_name);
        if (stat(path, &statbuf) == 0 && S_ISREG(statbuf.st_mode)) {
            count++;
        }
    }
    closedir(dir);
    printf("Number of regular files in '%s': %d\n", dir_name, count);
    return 0;
}

28. Develop a C program to create a FIFO (named pipe) named "myfifo" in the current directory?
#include <stdio.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <errno.h>
int main() {
    const char *fifo_path = "myfifo";
    if (mkfifo(fifo_path, 0666) == -1) {
        if (errno == EEXIST) {
            printf("FIFO '%s' already exists.\n", fifo_path);
        } else {
            perror("Error creating FIFO");
            return 1;
        }
    } else {
        printf("FIFO '%s' created successfully.\n", fifo_path);
    }
    return 0;
}

29. Implement a C program to read data from a FIFO named "myfifo"? 
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>
#include <sys/stat.h>
#include <string.h>

#define FIFO_NAME "myfifo"
#define BUFFER_SIZE 1024
int main()
{
    int fd;
    char buffer[BUFFER_SIZE];
    const char *message = "Hello from another process!\n";
    if (access(FIFO_NAME, F_OK) == -1)
    {
        if (mkfifo(FIFO_NAME, 0666) == -1)
	{
            perror("Failed to create FIFO");
            exit(EXIT_FAILURE);
        }
    }
    pid_t pid = fork();
    if (pid < 0)
    {
        perror("Fork failed");
        exit(EXIT_FAILURE);
    }
    if (pid == 0)
    {
        fd = open(FIFO_NAME, O_WRONLY);
        if (fd == -1)
	{
            perror("Child: Error opening FIFO for writing");
            exit(EXIT_FAILURE);
        }
        write(fd, message, strlen(message));
        close(fd);
        printf("Child: Wrote message to FIFO\n");
    }
    else
    {
        fd = open(FIFO_NAME, O_RDONLY);
        if (fd == -1)
	{
            perror("Parent: Error opening FIFO for reading");
            exit(EXIT_FAILURE);
        }
        ssize_t bytesRead = read(fd, buffer, sizeof(buffer) - 1);
        if (bytesRead > 0)
	{
            buffer[bytesRead] = '\0';
            printf("Parent: Received from FIFO: %s", buffer);
        }
	else if (bytesRead == 0)
	{
            printf("Parent: No data received (EOF)\n");
        }
	else
	{
            perror("Parent: Error reading from FIFO");
        }
        close(fd);
    }
    return 0;
} 

30. Write a C program to truncate a file named "file.txt" to a specified length?
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <errno.h>
#include <string.h>
int main()
{
    const char *filename = "file.txt";
    off_t new_length;
    printf("Enter the new length to truncate '%s' to: ", filename);
    if (scanf("%ld", &new_length) != 1)
    {
        fprintf(stderr, "Invalid input\n");
        return EXIT_FAILURE;
    }
    if (truncate(filename, new_length) == -1)
    {
        perror("Error truncating file");
        return EXIT_FAILURE;
    }
    printf("File '%s' successfully truncated to %ld bytes\n", filename, new_length);
    return EXIT_SUCCESS;
}

31. Develop a C program to search for a specific string in a file named "data.txt" and display the line number(s) where it occurs?
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX_LINE_LENGTH 1024
int main()
{
    FILE *file;
    char line[MAX_LINE_LENGTH];
    char searchString[100];
    int lineNumber = 0;
    int found = 0;
    file = fopen("file.txt", "r");
    if (file == NULL)
    {
        perror("Error opening file 'file.txt'");
        return EXIT_FAILURE;
    }
    printf("Enter the string to search: ");
    if (fgets(searchString, sizeof(searchString), stdin) == NULL)
    {
        fprintf(stderr, "Error reading input\n");
        fclose(file);
        return EXIT_FAILURE;
    }
    size_t len = strlen(searchString);
    if (len > 0 && searchString[len - 1] == '\n')
    {
        searchString[len - 1] = '\0';
    }
    while (fgets(line, sizeof(line), file) != NULL)
    {
        lineNumber++;
        if (strstr(line, searchString) != NULL)
	{
            printf("Found on line %d: %s", lineNumber, line);
            found = 1;
        }
    }
    if (!found)
    {
        printf("String '%s' not found in file\n", searchString);
    }
    fclose(file);
    return 0;
}
32. Implement a C program to get the file type (regular file, directory, symbolic link, etc.) of a given path?
#include <stdio.h>
#include <sys/stat.h>
int main()
{
    struct stat fileStat;
    char path[256];
    printf("Enter path: ");
    scanf("%255s", path);
    if (lstat(path, &fileStat) == -1)
    {
        perror("Error");
        return 1;
    }
    if (S_ISREG(fileStat.st_mode))
        printf("Regular file\n");
    else if (S_ISDIR(fileStat.st_mode))
        printf("Directory\n");
    else if (S_ISLNK(fileStat.st_mode))
        printf("Symbolic link\n");
    else
        printf("Other type\n");
    return 0;
}

33. Write a C program to create a new empty file named "empty.txt"?
#include <stdio.h>
int main()
{
    FILE *file = fopen("empty.txt", "w");
    if (file == NULL)
    {
        perror("Error creating file");
        return 1;
    }
    printf("File 'empty.txt' created successfully\n");
    fclose(file);
    return 0;
}

34. Develop a C program to get the permissions (mode) of a file named "file.txt"?
#include <stdio.h>
#include <sys/stat.h>
int main()
{
    struct stat fileStat;
    if (stat("file.txt", &fileStat) == -1)
    {
        perror("Error");
        return 1;
    }
    printf("Permissions (octal) for 'file.txt': %o\n", fileStat.st_mode & 0777);
    return 0;
}

35. Implement a C program to recursively delete a directory named "Temp" and all its contents? 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <unistd.h>
#include <sys/stat.h>
int delete_dir(const char *path)
{
    struct dirent *entry;
    DIR *dir = opendir(path);
    if (!dir) return -1;
    char fullPath[1024];
    while ((entry = readdir(dir)) != NULL)
    {
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;
        snprintf(fullPath, sizeof(fullPath), "%s/%s", path, entry->d_name);
        struct stat st;
        if (stat(fullPath, &st) == 0)
	{
            if (S_ISDIR(st.st_mode))
	    {
                delete_dir(fullPath);
            }
	    else
	    {
                unlink(fullPath);
            }
        }
    }
    closedir(dir);
    return rmdir(path);
}
int main()
{
    const char *folder = "Temp";
    if (delete_dir(folder) == 0)
    {
        printf("Directory '%s' deleted successfully\n", folder);
    }
    else
    {
        perror("Error deleting directory");
    }
    return 0;
}

36. Write a C program to read and display the first 10 lines of a file named "log.txt"?
#include <stdio.h>
#include <stdlib.h>
int main()
{
    FILE *file = fopen("file.txt", "r");
    if (file == NULL)
    {
        perror("Error opening file.txt");
        return 1;
    }
    char line[1024];
    int count = 0;
    while (fgets(line, sizeof(line), file) != NULL && count < 10)
    {
        printf("%s", line);
        count++;
    }
    fclose(file);
    return 0;
}

37. Develop a C program to read data from a text file named "input.txt" and write it to another file named "output.txt" in reverse order?
#include <stdio.h>
int main()
{
    FILE *infile, *outfile;
    long pos;
    infile = fopen("input.txt", "r");
    if (infile == NULL)
    {
        printf("Unable to open input.txt");
        return 1;
    }
    outfile = fopen("output.txt", "w");
    if (outfile == NULL)
    {
        printf("Unable to create output.txt");
        fclose(infile);
        return 1;
    }
    fseek(infile, 0, SEEK_END);
    pos = ftell(infile);
    while (pos-- > 0)
    {
        fseek(infile, pos, SEEK_SET);
        fputc(fgetc(infile), outfile);
    }
    printf("Reversed content written to output.txt\n");
    fclose(infile);
    fclose(outfile);
    return 0;
}

38. Implement a C program to create a new directory named with the current date in the format "YYYY-MM-DD"?
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <sys/stat.h>
#include <sys/types.h>
int main()
{
    time_t t;
    struct tm *tm_info;
    char dirname[20];
    time(&t);
    tm_info = localtime(&t);
    strftime(dirname, sizeof(dirname), "%Y-%m-%d", tm_info);
    if (mkdir(dirname, 0755) == 0)
    {
        printf("Directory '%s' created successfully\n", dirname);
    }
    else
    {
        perror("mkdir failed");
    }
    return 0;
}

39. Write a C program to read and display the contents of a binary file named "binary.bin"?
#include <stdio.h>
#include <stdlib.h>
int main()
{
    FILE *file;
    char data[] = "Hello, Binary World!";
    unsigned char buffer;
    file = fopen("binary.bin", "wb");
    if (file == NULL)
    {
        perror("Error creating binary.bin");
        return 1;
    }
    fwrite(data, sizeof(char), sizeof(data) - 1, file); // Write without null terminator
    fclose(file);
    printf("Data written to binary.bin successfully\n");
    file = fopen("binary.bin", "rb");
    if (file == NULL)
    {
        perror("Error opening binary.bin");
        return 1;
    }
    printf("Reading from binary.bin...\n");
    printf("Hex\tASCII\n");
    printf("---\t-----\n");
    while (fread(&buffer, sizeof(unsigned char), 1, file) == 1)
    {
        printf("%02X\t%c\n", buffer, (buffer >= 32 && buffer <= 126) ? buffer : '.');
    }
    fclose(file);
    return 0;
}

40. Develop a C program to get the size of the largest file in a directory?
#include <stdio.h>
#include <dirent.h>
#include <sys/stat.h>
int main()
{
    DIR *d;
    struct dirent *entry;
    struct stat st;
    long max_size = 0;
    d = opendir(".");
    if (d == NULL)
    {
        printf("Unable to open directory\n");
        return 1;
    }
    while ((entry = readdir(d)) != NULL)
    {
        stat(entry->d_name, &st);
        if (S_ISREG(st.st_mode))
	{
	    if (st.st_size > max_size)
	    {
                max_size = st.st_size;
            }
        }
    }
    closedir(d);
    printf("Largest file size: %ld bytes\n", max_size);
    return 0;
}

41. Implement a C program to check if a file named "file.txt" is readable?
#include <stdio.h>
#include <unistd.h>
int main()
{
    const char *filename = "file.txt";
    if (access(filename, R_OK) == 0)
    {
        printf("The file '%s' is readable\n", filename);
    }
    else
    {
        perror("File check failed");
    }
    return 0;
}

42. Write a C program to create a new directory named "Logs" and move all files with the ".log" extension into it?
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <sys/stat.h>
#include <unistd.h>
int ends_with_log(const char *filename)
{
    int len = strlen(filename);
    return (len > 4 && strcmp(filename + len - 4, ".log") == 0);
}
int main()
{
    DIR *dir;
    struct dirent *entry;
    char oldpath[512], newpath[512];
   if (mkdir("Logs", 0755) == -1 && access("Logs", F_OK) != 0)
   {
        perror("mkdir failed");
        return 1;
    }
    dir = opendir(".");
    if (dir == NULL)
    {
        perror("Failed to open directory");
        return 1;
    }
    while ((entry = readdir(dir)) != NULL)
    {
        if (entry->d_type == DT_REG && ends_with_log(entry->d_name))
	{
            snprintf(oldpath, sizeof(oldpath), "%s", entry->d_name);
            snprintf(newpath, sizeof(newpath), "Logs/%s", entry->d_name);
            if (rename(oldpath, newpath) == 0) {
                printf("Moved: %s -> %s\n", oldpath, newpath);
            }
	    else
	    {
                perror("Failed to move file");
            }
        }
    }
    closedir(dir);
    return 0;
}

43. Develop a C program to check if a file named "config.ini" is writable?
#include <stdio.h>
#include <unistd.h>
int main()
{
    const char *filename = "config.ini";
    if (access(filename, W_OK) == 0)
    {
        printf("The file '%s' is writable\n", filename);
    }
    else
    {
        perror("Permission check");
        printf("The file '%s' is NOT writable\n", filename);
    }
    return 0;
}

44. Implement a C program to read the contents of a text file named "instructions.txt" and execute the instructions as shell commands? 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int main()
{
    FILE *file;
    char command[256];
    file = fopen("instructions.txt", "r");
    if (file == NULL)
    {
        perror("Error opening file");
        return 1;
    }
    while (fgets(command, sizeof(command), file) != NULL)
    {
        if (command[strlen(command) - 1] == '\n')
	{
            command[strlen(command) - 1] = '\0';
        }
        printf("Executing: %s\n", command);
        system(command);
    }
    fclose(file);
    return 0;
}

45. Write a C program to get the number of hard links to a file named "file.txt"? 
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
int main()
{
    struct stat fileStat;
    if (stat("file.txt", &fileStat) == -1)
    {
        perror("Error getting file information");
        return 1;
    }
     printf("Number of hard links to file.txt: %lu\n", fileStat.st_nlink);
    return 0;
}
```
