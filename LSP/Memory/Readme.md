### Programs on Memory management
```c
1. Write a C program to demonstrate dynamic memory allocation using malloc().
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int *numbers;
    int n, i;
    printf("Enter the number of elements: ");
    scanf("%d", &n);
    numbers = (int *)malloc(n * sizeof(int));
    if (numbers == NULL)
    {
        printf("Memory allocation failed!\n");
        return 1;
    }
    printf("Enter %d integers:\n", n);
    for (i = 0; i < n; i++)
    {
        printf("Element %d: ", i + 1);
        scanf("%d", &numbers[i]);
    }
    printf("You entered:\n");
    for (i = 0; i < n; i++)
    {
        printf("%d ", numbers[i]);
    }
    printf("\n");
    free(numbers);
    return 0;
}

2. Implement a C program to allocate memory for an array dynamically using calloc().
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int *numbers;
    int n, i;
    printf("Enter the number of elements: ");
    scanf("%d", &n);
    numbers = (int *)calloc(n, sizeof(int));
    if (numbers == NULL)
    {
        printf("Memory allocation failed!\n");
        return 1;
    }
    printf("Enter %d integers:\n", n);
    for (i = 0; i < n; i++)
    {
        printf("Element %d: ", i + 1);
        scanf("%d", &numbers[i]);
    }
    printf("You entered:\n");
    for (i = 0; i < n; i++)
    {
        printf("%d ", numbers[i]);
    }
    printf("\n");
    free(numbers);
    return 0;
}

3. Write a C program to resize dynamically allocated memory using realloc().
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int *numbers;
    int n, new_n, i;
    printf("Enter the initial number of elements: ");
    scanf("%d", &n);
    numbers = (int *)malloc(n * sizeof(int));
    if (numbers == NULL)
    {
        printf("Memory allocation failed!\n");
        return 1;
    }
    printf("Enter %d integers:\n", n);
    for (i = 0; i < n; i++)
    {
        printf("Element %d: ", i + 1);
        scanf("%d", &numbers[i]);
    }
    printf("Enter the new number of elements: ");
    scanf("%d", &new_n);
    numbers = (int *)realloc(numbers, new_n * sizeof(int));
    if (numbers == NULL)
    {
        printf("Memory reallocation failed!\n");
        return 1;
    }
    if (new_n > n)
    {
        printf("Enter %d more elements:\n", new_n - n);
        for (i = n; i < new_n; i++)
        {
            printf("Element %d: ", i + 1);
            scanf("%d", &numbers[i]);
        }
    }
    printf("The array elements are:\n");
    for (i = 0; i < new_n; i++)
    {
        printf("%d ", numbers[i]);
    }
    printf("\n");
    free(numbers);
    return 0;
}

4. Develop a program in C to allocate memory for a linked list node dynamically.
#include <stdio.h>
#include <stdlib.h>
struct Node {
    int data;
    struct Node* next;
};
int main()
{
    struct Node* head = (struct Node*)malloc(sizeof(struct Node));
    if (head == NULL)
    {
        printf("Memory allocation failed\n");
        return 1;
    }
    head->data = 10;
    head->next = NULL;
    printf("Data in the node: %d\n", head->data);
    free(head);
    return 0;
}

5. Implement a C program to simulate memory allocation using the first-fit algorithm.
#include <stdio.h>
#define MAX_BLOCKS 10
#define MAX_PROCESSES 10
void firstFit(int blockSize[], int blocks, int processSize[], int processes) {
    int allocation[MAX_PROCESSES];
    for (int i = 0; i < processes; i++)
    {
        allocation[i] = -1;
    }
    for (int i = 0; i < processes; i++)
    {
        for (int j = 0; j < blocks; j++)
        {
            if (blockSize[j] >= processSize[i])
            {
                allocation[i] = j;
                blockSize[j] -= processSize[i];
                break;
            }
        }
    }
    printf("\nProcess No.\tProcess Size\tBlock No.\n");
    for (int i = 0; i < processes; i++) {
        printf("%d\t\t%d\t\t", i + 1, processSize[i]);
        if (allocation[i] != -1)
            printf("%d\n", allocation[i] + 1);
        else
            printf("Not Allocated\n");
    }
}
int main()
{
    int blockSize[MAX_BLOCKS], processSize[MAX_PROCESSES];
    int blocks, processes;
    printf("Enter number of memory blocks: ");
    scanf("%d", &blocks);
    printf("Enter size of each block:\n");
    for (int i = 0; i < blocks; i++)
    {
        printf("Block %d: ", i + 1);
        scanf("%d", &blockSize[i]);
    }
    printf("\nEnter number of processes: ");
    scanf("%d", &processes);
    printf("Enter size of each process:\n");
    for (int i = 0; i < processes; i++)
    {
        printf("Process %d: ", i + 1);
        scanf("%d", &processSize[i]);
    }
    firstFit(blockSize, blocks, processSize, processes);
    return 0;
}

7. Write a C program to simulate memory allocation using the best-fit algorithm.
include <stdio.h>
#define MAX_BLOCKS 10
#define MAX_PROCESSES 10
void bestFit(int blockSize[], int blocks, int processSize[], int processes) {
    int allocation[MAX_PROCESSES];
    for (int i = 0; i < processes; i++) {
        allocation[i] = -1;
    }
    for (int i = 0; i < processes; i++) {
        int bestIdx = -1;
        for (int j = 0; j < blocks; j++) {
            if (blockSize[j] >= processSize[i]) {
                if (bestIdx == -1 || blockSize[j] < blockSize[bestIdx]) {
                    bestIdx = j;
                }
            }
        }
        if (bestIdx != -1) {
            allocation[i] = bestIdx;
            blockSize[bestIdx] -= processSize[i];
        }
    }
    printf("\nProcess No.\tProcess Size\tBlock No.\n");
    for (int i = 0; i < processes; i++) {
        printf("%d\t\t%d\t\t", i + 1, processSize[i]);
        if (allocation[i] != -1) {
            printf("%d\n", allocation[i] + 1); // +1 to convert zero-based index to block number
        } else {
            printf("Not Allocated\n");
        }
    }
}
int main() {
    int blockSize[MAX_BLOCKS], processSize[MAX_PROCESSES];
    int blocks, processes;
    printf("Enter number of memory blocks: ");
    scanf("%d", &blocks);
    printf("Enter size of each block:\n");
    for (int i = 0; i < blocks; i++) {
        printf("Block %d: ", i + 1);
    scanf("%d", &blockSize[i]);
    }
    printf("\nEnter number of processes: ");
    scanf("%d", &processes);
    printf("Enter size of each process:\n");
    for (int i = 0; i < processes; i++) {
        printf("Process %d: ", i + 1);
        scanf("%d", &processSize[i]);
    }
    bestFit(blockSize, blocks, processSize, processes);
    return 0;
}

8. Develop a C program to simulate memory allocation using the worst-fit algorithm.
#include <stdio.h>
#define MAX_BLOCKS 10
#define MAX_PROCESSES 10
void worstFit(int blockSize[], int blocks, int processSize[], int processes)
{
    int allocation[MAX_PROCESSES];
    for (int i = 0; i < processes; i++)
    {
        allocation[i] = -1;
    }
    for (int i = 0; i < processes; i++)
    {
        int worstIdx = -1;
        for (int j = 0; j < blocks; j++)
        {
            if (blockSize[j] >= processSize[i])
            {
                if (worstIdx == -1 || blockSize[j] > blockSize[worstIdx])
                {
                    worstIdx = j;
                }
            }
        }
        if (worstIdx != -1)
        {
            allocation[i] = worstIdx;
            blockSize[worstIdx] -= processSize[i];
        }
    }
    printf("\nProcess No.\tProcess Size\tBlock No.\n");
    for (int i = 0; i < processes; i++) {
        printf("%d\t\t%d\t\t", i + 1, processSize[i]);
        if (allocation[i] != -1)
            printf("%d\n", allocation[i] + 1);
        else
            printf("Not Allocated\n");
    }
}
int main()
{
    int blockSize[MAX_BLOCKS], processSize[MAX_PROCESSES];
    int blocks, processes;
    printf("Enter number of memory blocks: ");
    scanf("%d", &blocks);
    printf("Enter size of each block:\n");
    for (int i = 0; i < blocks; i++)
    {
        printf("Block %d: ", i + 1);
        scanf("%d", &blockSize[i]);
    }
    printf("\nEnter number of processes: ");
    scanf("%d", &processes);
    printf("Enter size of each process:\n");
    for (int i = 0; i < processes; i++)
    {
        printf("Process %d: ", i + 1);
        scanf("%d", &processSize[i]);
    }
    worstFit(blockSize, blocks, processSize, processes);
    return 0;
}
9. Implement a C program to simulate memory allocation using the next-fit algorithm.
#include <stdio.h>
#define MAX_BLOCKS 20
#define MAX_PROCESSES 20
void nextFit(int blockSize[], int blocks, int processSize[], int processes) {
    int allocation[MAX_PROCESSES];
    int lastAllocatedIndex = 0;  // Keeps track of the last allocated block
    for (int i = 0; i < processes; i++) {
        allocation[i] = -1;
    }
    for (int i = 0; i < processes; i++) {
        int count = 0;
        int j = lastAllocatedIndex;
        while (count < blocks) {
            if (blockSize[j] >= processSize[i]) {
                allocation[i] = j;
                blockSize[j] -= processSize[i];
                lastAllocatedIndex = j;
                break;
            }
            j = (j + 1) % blocks;  // Move to next block
            count++;
        }
    }
    printf("\nProcess No.\tProcess Size\tBlock No.\n");
    for (int i = 0; i < processes; i++) {
        printf("%d\t\t%d\t\t", i + 1, processSize[i]);
        if (allocation[i] != -1)
            printf("%d\n", allocation[i] + 1);  // +1 for block number (1-based)
        else
            printf("Not Allocated\n");
    }
}
int main() {
    int blockSize[MAX_BLOCKS], processSize[MAX_PROCESSES];
    int blocks, processes;
    printf("Enter number of memory blocks: ");
    scanf("%d", &blocks);
    printf("Enter size of each block:\n");
    for (int i = 0; i < blocks; i++) {
        printf("Block %d: ", i + 1);
        scanf("%d", &blockSize[i]);
    }
    printf("\nEnter number of processes: ");
    scanf("%d", &processes);
    printf("Enter size of each process:\n");
    for (int i = 0; i < processes; i++) {
        printf("Process %d: ", i + 1);
        scanf("%d", &processSize[i]);
    }
    nextFit(blockSize, blocks, processSize, processes);
    return 0;
}

10. Write a C program to implement a simple memory allocator using the buddy system.
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

#define MEMORY_SIZE 1024 
#define MIN_BLOCK_SIZE 8

char memory[MEMORY_SIZE];
int used[MEMORY_SIZE];

int next_power_of_two(int size)
{
    int power = MIN_BLOCK_SIZE;
    while (power < size) power *= 2;
    return power;
}
void* buddy_malloc(int size)
{
    int block_size = next_power_of_two(size);
    for (int i = 0; i < MEMORY_SIZE; i += block_size)
    {
        int free = 1;
        for (int j = 0; j < block_size; j++)
        {
            if (used[i + j])
            {
                free = 0;
                break;
            }
        }
        if (free)
        {
            for (int j = 0; j < block_size; j++) used[i + j] = 1;
            return &memory[i];
        }
    }
    return NULL;
}
void buddy_free(void* ptr, int size)
{
    int block_size = next_power_of_two(size);
    int index = (char*)ptr - memory;
    for (int i = 0; i < block_size; i++) used[index + i] = 0;
}
int main()
{
    void* a = buddy_malloc(100);
    void* b = buddy_malloc(200);
    printf("Allocated a at %ld\n", (char*)a - memory);
    printf("Allocated b at %ld\n", (char*)b - memory);
    buddy_free(a, 100);
    buddy_free(b, 200);
    printf("Memory freed.\n");
    return 0;
}

11. Develop a C program to implement a memory allocator using a custom memory management algorithm
#include <stdio.h>
#include <stddef.h>

#define MEMORY_SIZE 1024

char memory[MEMORY_SIZE];
int used[MEMORY_SIZE];

void* my_malloc(size_t size)
{
    for (int i = 0; i <= MEMORY_SIZE - size; i++)
    {
        int free = 1;
        for (int j = 0; j < size; j++)
        {
            if (used[i + j])
            {
                free = 0;
                break;
            }
        }
        if (free)
        {
            for (int j = 0; j < size; j++)
            {
                used[i + j] = 1;
            }
            return &memory[i];
        }
    }
    return NULL;
}
void my_free(void* ptr, size_t size)
{
    int index = (char*)ptr - memory;
    for (int i = 0; i < size; i++)
    {
        used[index + i] = 0;
    }
}

int main()
{
    void* a = my_malloc(100);
    void* b = my_malloc(200);
    printf("Allocated a at offset: %ld\n", (char*)a - memory);
    printf("Allocated b at offset: %ld\n", (char*)b - memory);
    my_free(a, 100);
    my_free(b, 200);
    printf("Memory freed.\n");
    return 0;
}

12. Write a C program to demonstrate memory mapping using mmap().
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <sys/mman.h>
#include <unistd.h>
#include <string.h>

#define FILEPATH "mmap_example.txt"
#define SIZE 4096

int main()
{
    int fd;
    char* map;
    // Step 1: Open a file (create if it doesn't exist)
    fd = open(FILEPATH, O_RDWR | O_CREAT, 0666);
    if (fd == -1)
    {
        perror("open");
        return 1;
    }
    // Step 2: Stretch the file size
    if (ftruncate(fd, SIZE) == -1)
    {
        perror("ftruncate");
        close(fd);
        return 1;
    }
    // Step 3: Memory-map the file
    map = mmap(NULL, SIZE, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);
    if (map == MAP_FAILED)
    {
        perror("mmap");
        close(fd);
        return 1;
    }
   // Step 4: Write to the memory-mapped area
    strcpy(map, "Hello, memory-mapped file!");
    printf("Written to mapped memory: %s\n", map);
    // Step 5: Read from the mapped memory
    printf("Read from mapped memory: %s\n", map);
    // Step 6: Unmap and clean up
    if (munmap(map, SIZE) == -1)
    {
        perror("munmap");
    }
    close(fd);
    return 0;
}

13. Implement a C program to read from and write to a memory-mapped file.
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <sys/mman.h>
#include <unistd.h>
#include <string.h>

#define FILEPATH "mmap_file.txt"
#define SIZE 4096

int main()
{
    int fd;
    char* map;
    // Step 1: Open or create the file
    fd = open(FILEPATH, O_RDWR | O_CREAT, 0666);
    if (fd == -1)
    {
        perror("open");
        return 1;
    }
    // Step 2: Resize the file to the required size
    if (ftruncate(fd, SIZE) == -1)
    {
        perror("ftruncate");
        close(fd);
        return 1;
    }
    // Step 3: Memory map the file
    map = mmap(NULL, SIZE, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);
    if (map == MAP_FAILED)
    {
        perror("mmap");
        close(fd);
        return 1;
    }
    // Step 4: Write to the memory-mapped file
    const char* message = "This is a memory-mapped write!\n";
    memcpy(map, message, strlen(message));
    // Step 5: Read from the memory-mapped file
    printf("Reading from memory-mapped file:\n%s", map);
    // Step 6: Unmap and close
    if (munmap(map, SIZE) == -1)
    {
        perror("munmap");
    }
    close(fd);
    return 0;
}

14. Develop a C program to demonstrate shared memory usage using shmget() and shmat().
//Program 1: Reader (shm_reader.c)
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <unistd.h>

#define SHM_KEY 0x1234
#define SHM_SIZE 1024

int main()
{
    int shmid;
    char *shm_ptr;
    // Get the shared memory segment
    shmid = shmget(SHM_KEY, SHM_SIZE, 0666);
    if (shmid == -1)
    {
        perror("shmget failed");
        return 1;
    }
    // Attach to the shared memory
    shm_ptr = (char *)shmat(shmid, NULL, 0);
    if (shm_ptr == (char *)(-1))
    {
        perror("shmat failed");
        return 1;
    }
    // Read the message
    printf("Reader: Message from shared memory: \"%s\"\n", shm_ptr);
    // Detach from shared memory
    shmdt(shm_ptr);
    // Optional: Remove shared memory segment
    shmctl(shmid, IPC_RMID, NULL);
    return 0;
}
//Program 2: Writer (shm_writer.c)
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <unistd.h>

#define SHM_KEY 0x1234
#define SHM_SIZE 1024
int main()
{
    int shmid;
    char *shm_ptr;
    // Create shared memory segment
    shmid = shmget(SHM_KEY, SHM_SIZE, IPC_CREAT | 0666);
    if (shmid == -1) {
        perror("shmget failed");
        return 1;
    }
    // Attach to the shared memory
    shm_ptr = (char *)shmat(shmid, NULL, 0);
    if (shm_ptr == (char *)(-1))
    {
        perror("shmat failed");
        return 1;
    }
    // Write a message into shared memory
    strcpy(shm_ptr, "Hello from shared memory!");
    printf("Writer: Message written to shared memory\n");
    // Detach from shared memory
    shmdt(shm_ptr);
    return 0;
}

15. Write a C program to create a shared memory segment and synchronize access using semaphores.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/sem.h>
#include <unistd.h>

#define SHM_KEY 0x1234
#define SEM_KEY 0x5678
#define SHM_SIZE 1024

// Union required for semctl()
union semun {
    int val;
    struct semid_ds *buf;
    unsigned short *array;
};

// Semaphore wait (P operation)
void sem_wait(int semid) {
    struct sembuf sb = {0, -1, 0}; // wait
    semop(semid, &sb, 1);
}

// Semaphore signal (V operation)
void sem_signal(int semid) {
    struct sembuf sb = {0, 1, 0}; // signal
    semop(semid, &sb, 1);
}

int main(int argc, char *argv[]) {
    if (argc != 2) {
        fprintf(stderr, "Usage: %s [writer|reader]\n", argv[0]);
        exit(1);
    }

    int shmid = shmget(SHM_KEY, SHM_SIZE, IPC_CREAT | 0666);
    if (shmid < 0) {
    perror("shmget");
        exit(1);
    }

    char *data = (char *)shmat(shmid, NULL, 0);
    if (data == (char *)(-1)) {
        perror("shmat");
        exit(1);
    }

    int semid = semget(SEM_KEY, 1, IPC_CREAT | 0666);
    if (semid < 0) {
        perror("semget");
        exit(1);
    }

    // Initialize semaphore only once
    if (strcmp(argv[1], "writer") == 0) {
        union semun sem_union;
        sem_union.val = 1;
        semctl(semid, 0, SETVAL, sem_union);
    }

    if (strcmp(argv[1], "writer") == 0) {
        while (1) {
            sem_wait(semid);
            printf("Enter text: ");
            fgets(data, SHM_SIZE, stdin);
            sem_signal(semid);
            if (strncmp(data, "exit", 4) == 0)
                break;
        }
    } else if (strcmp(argv[1], "reader") == 0) {
        while (1) {
            sem_wait(semid);
            printf("Read from shared memory: %s", data);
    sem_signal(semid);
            if (strncmp(data, "exit", 4) == 0)
                break;
            sleep(1); // avoid busy waiting
        }
    } else {
        fprintf(stderr, "Invalid role. Use 'writer' or 'reader'.\n");
    }

    shmdt(data);

    // Cleanup (optional, typically done after both processes are finished)
    if (strcmp(argv[1], "writer") == 0) {
        shmctl(shmid, IPC_RMID, NULL);
        semctl(semid, 0, IPC_RMID);
    }

    return 0;
}

16. Implement a C program to simulate page replacement algorithms like FIFO, LRU, and optimal.
#include <stdio.h>

#define MAX 50

// Check if page is in frame
int isHit(int page, int frame[], int f) {
    for (int i = 0; i < f; i++)
        if (frame[i] == page)
            return 1;
    return 0;
}

void FIFO(int pages[], int n, int f) {
    int frame[MAX], index = 0, faults = 0;

    printf("\nFIFO:\n");
    for (int i = 0; i < f; i++) frame[i] = -1;

    for (int i = 0; i < n; i++) {
        if (!isHit(pages[i], frame, f)) {
            frame[index] = pages[i];
            index = (index + 1) % f;
            faults++;
        }

        for (int j = 0; j < f; j++)
            printf("%d ", frame[j]);
        printf("\n");
    }

    printf("Total Page Faults (FIFO): %d\n", faults);
}

void LRU(int pages[], int n, int f) {
    int frame[MAX], time[MAX], faults = 0, count = 0;

    printf("\nLRU:\n");
    for (int i = 0; i < f; i++) frame[i] = -1;
    for (int i = 0; i < n; i++) {
        int found = 0;
        for (int j = 0; j < f; j++) {
            if (frame[j] == pages[i]) {
                time[j] = ++count;
                found = 1;
                break;
            }
        }

        if (!found) {
            int min = 0;
            for (int j = 1; j < f; j++)
                if (time[j] < time[min]) min = j;

            frame[min] = pages[i];
            time[min] = ++count;
            faults++;
        }

        for (int j = 0; j < f; j++)
            printf("%d ", frame[j]);
        printf("\n");
    }

    printf("Total Page Faults (LRU): %d\n", faults);
}

void Optimal(int pages[], int n, int f) {
    int frame[MAX], faults = 0;

    printf("\nOptimal:\n");
    for (int i = 0; i < f; i++) frame[i] = -1;

    for (int i = 0; i < n; i++) {
        if (!isHit(pages[i], frame, f)) {
    int replace = -1, farthest = i;

            for (int j = 0; j < f; j++) {
                int k;
                for (k = i + 1; k < n; k++) {
                    if (frame[j] == pages[k]) break;
                }
                if (k > farthest) {
                    farthest = k;
                    replace = j;
                }
                if (k == n) {
                    replace = j;
                    break;
                }
            }

            if (replace == -1) replace = 0;
            frame[replace] = pages[i];
            faults++;
        }

        for (int j = 0; j < f; j++)
            printf("%d ", frame[j]);
        printf("\n");
    }

    printf("Total Page Faults (Optimal): %d\n", faults);
}

int main() {
    int pages[MAX], n, f;

    printf("Enter number of pages: ");
    scanf("%d", &n);
    printf("Enter page reference string:\n");
    for (int i = 0; i < n; i++)
        scanf("%d", &pages[i]);

    printf("Enter number of frames: ");
    scanf("%d", &f);

    FIFO(pages, n, f);
    LRU(pages, n, f);
    Optimal(pages, n, f);

    return 0;
}
```
