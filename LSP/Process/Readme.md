### Programs on Process Management
```c
1. Write a C program to demonstrate the use of fork() system call. 
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
int main()
{
    pid_t pid;
    printf("Before fork\n");
    pid = fork();
    if (pid < 0)
    {
        perror("fork failed");
        return 1;
    }
    else if (pid == 0)
    {
        printf("Hello from child process! PID = %d\n", getpid());
    }
    else
    {
        printf("Hello from parent process! PID = %d, Child PID = %d\n", getpid(),pid);
    }
    printf("This line is executed by both processes\n");
    return 0;
}

2. Write a C program to illustrate the use of the execvp() function. 
#include <stdio.h>
#include <unistd.h>
int main()
{
    char *args[] = {"ls", "-l", NULL};
    printf("Before execvp\n");
    execvp("ls", args);
    perror("execvp failed");
    return 1;
}

3. Write a program in C to create a child process using fork() and print its PID. 
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
int main()
{
    pid_t pid = fork();
    if (pid < 0) {
        perror("fork failed");
        return 1;
    }
    else if (pid == 0)
    {
        printf("Child process: My PID is %d\n", getpid());
    }
    else
    {
        printf("Parent process: Created child with PID %d\n", pid);
    }
    return 0;
}

4. Write a C program to create multiple child processes using fork() and display their PIDs. 
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#define NUM_CHILDREN 5
int main()
{
    pid_t pid;
    for (int i = 0; i < NUM_CHILDREN; i++)
    {
        pid = fork();
        if (pid < 0)
        {
            perror("fork failed");
            return 1;
        }
        else if (pid == 0)
        {
            printf("Child %d: My PID is %d\n", i + 1, getpid());
            return 0;
        }
        else
        {
            printf("Parent: Created child %d with PID %d\n", i + 1, pid);
        }
    }
    for (int i = 0; i < NUM_CHILDREN; i++)
    {
        wait(NULL);
    }
    return 0;
}

5. Write a program in C to create a zombie process and explain how to avoid it. 
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
int main()
{
    pid_t pid = fork();
    if (pid > 0)
    {
        printf("Parent process PID: %d\n", getpid());
        printf("Child process PID: %d (will become zombie)\n", pid);
        sleep(30);
    }
    else if (pid == 0)
    {
        printf("Child process PID: %d is exiting\n", getpid());
        _exit(0);
    }
    else
    {
        perror("fork failed");
        return 1;
    }
    return 0;
}

6. Write a C program to demonstrate the use of the waitpid() function for process synchronization. 
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
int main()
{
    pid_t pid = fork();
    if (pid < 0)
    {
        perror("fork failed");
        return 1;
    }
    if (pid == 0)
    {
        printf("Child process started (PID: %d)\n", getpid());
        sleep(3);
        printf("Child process exiting\n");
        _exit(0);
    }
    else
    {
        int status;
        printf("Parent waiting for child PID %d to finish...\n", pid);
        waitpid(pid, &status, 0);
        if (WIFEXITED(status))
        {
            printf("Child exited with status %d\n", WEXITSTATUS(status));
        }
        else
        {
            printf("Child terminated abnormally\n");
        }
        printf("Parent continues after child has finished\n");
    }
    return 0;
}

7. Write a program in C to create a daemon process. 
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
int main() {
    pid_t pid;
    pid = fork();
    if (pid < 0) {
        perror("fork failed");
        exit(EXIT_FAILURE);
    }
    if (pid > 0) {
        printf("Parent process exiting, child PID %d will run as daemon\n", pid);
        exit(EXIT_SUCCESS);
    }
    if (setsid() < 0) {
        perror("setsid failed");
        exit(EXIT_FAILURE);
    }
    pid = fork();
    if (pid < 0) {
        perror("fork failed");
        exit(EXIT_FAILURE);
    }
    if (pid > 0) {
        exit(EXIT_SUCCESS);
    }
    if (chdir("/") < 0) {
        perror("chdir failed");
        exit(EXIT_FAILURE);
    }
    close(STDIN_FILENO);
    close(STDOUT_FILENO);
    close(STDERR_FILENO);
    open("/dev/null", O_RDONLY);   // stdin
    open("/dev/null", O_RDWR);     // stdout
    open("/dev/null", O_RDWR);     // stderr
    while (1) {
        sleep(10);
    }
    return 0;
}

8. Write a C program to demonstrate the use of the system() function for executing shell commands. 
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int ret;
    printf("Listing current directory contents:\n");
    ret = system("ls -l");
    if (ret == -1)
    {
        perror("system() failed");
        return 1;
    }
    else
    {
        printf("Command executed with return code: %d\n", ret);
    }

    return 0;
}

9. Write a C program to create a process using fork() and pass arguments to the child process. 
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <stdlib.h>
int main()
{
    pid_t pid = fork();
    if (pid < 0)
    {
        perror("fork failed");
        return 1;
    }
    if (pid == 0)
    {
        printf("Child process (PID: %d) executing ls command...\n", getpid());
        char *args[] = {"ls", "-l", "/", NULL};
        execvp("ls", args);
        perror("execvp failed");
        exit(1);
    }
    else
    {
        printf("Parent process (PID: %d) created child with PID: %d\n", getpid(), pid);
        wait(NULL);
    }
    return 0;
}

10. Write a program in C to demonstrate process synchronization using semaphores.
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/sem.h>
#include <sys/types.h>
#include <sys/wait.h>
union semun {
    int val;
};
void wait_semaphore(int semid)
{
    struct sembuf sb = {0, -1, 0};
    semop(semid, &sb, 1);
}
void signal_semaphore(int semid)
{
    struct sembuf sb = {0, 1, 0};
    semop(semid, &sb, 1);
}
int main()
{
    int semid;
    pid_t pid;
    semid = semget(IPC_PRIVATE, 1, IPC_CREAT | 0666);
    if (semid < 0)
    {
        perror("semget failed");
        exit(1);
    }
    union semun arg;
    arg.val = 1;
    semctl(semid, 0, SETVAL, arg);
    pid = fork();
    if (pid < 0)
    {
        perror("fork failed");
        exit(1);
    }
    for (int i = 0; i < 5; i++)
    {
        if (pid == 0)
        {
            wait_semaphore(semid);
            printf("Child entering critical section\n");
            sleep(1);
            printf("Child leaving critical section\n");
            signal_semaphore(semid);
            sleep(1);
        }
        else
        {
            wait_semaphore(semid);
            printf("Parent entering critical section\n");
            sleep(1);
            printf("Parent leaving critical section\n");
            signal_semaphore(semid);
            sleep(1);
        }
    }
    if (pid != 0)
    {
        wait(NULL);
        semctl(semid, 0, IPC_RMID);
    }
    return 0;
}

11. Write a C program to demonstrate the use of the execvpe() function.
#define _GNU_SOURCE  // Required for execvpe
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
int main()
{
    char *args[] = {"ls", "-l", NULL};
    char *env[] = {
        "MY_VAR=HelloFromExecvpe",
        NULL
    };
    printf("Running 'ls -l' with execvpe...\n");
    if (execvpe("ls", args, env) == -1)
    {
        perror("execvpe failed");
    }
    return 0;
}

12. Write a C program to create a process group and change its process group ID (PGID).
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <stdlib.h>
int main()
{
    pid_t pid = fork();
    if (pid < 0)
    {
        perror("fork failed");
        return 1;
    }
    if (pid == 0)
    {
        printf("Child PID: %d\n", getpid());
        printf("Child PGID before: %d\n", getpgrp());
        if (setpgid(0, 0) == 0)
        {
            printf("Child PGID changed to: %d\n", getpgrp());
        }
        else
        {
            perror("setpgid failed in child");
        }
        sleep(2);
    }
    else
    {
        printf("Parent PID: %d\n", getpid());
        printf("Parent PGID: %d\n", getpgrp());
        sleep(5);
    }
    return 0;
}

13. Write a program in C to demonstrate inter-process communication (IPC) using shared memory.
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <unistd.h>
#include <string.h>
#define SHM_SIZE 1024
int main()
{
    key_t key;
    int shmid;
    char *data;
    key = ftok("shmfile", 65);
    shmid = shmget(key, SHM_SIZE, 0666 | IPC_CREAT);
    if (shmid < 0)
    {
        perror("shmget");
        exit(1);
    }
    pid_t pid = fork();
    if (pid < 0)
    {
        perror("fork");
        exit(1);
    }
    else if (pid == 0)
    {
        data = (char *) shmat(shmid, (void *)0, 0);
        if (data == (char *)(-1))
        {
            perror("shmat");
            exit(1);
        }
        printf("Child: Writing to shared memory...\n");
        strcpy(data, "Hello from child process!");
        shmdt(data);
    }
    else
    {
        wait(NULL);
        data = (char *) shmat(shmid, (void *)0, 0);
        if (data == (char *)(-1))
        {
            perror("shmat");
            exit(1);
        }
        printf("Parent: Reading from shared memory: '%s'\n", data);
        shmdt(data);
        shmctl(shmid, IPC_RMID, NULL);
    }
    return 0;
}

14. Write a C program to create a child process using vfork() and demonstrate its usage.
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
int main()
{
    int x = 10;
    printf("Before vfork, x = %d\n", x);
    pid_t pid = vfork();
    if (pid < 0)
    {
        perror("vfork failed");
        exit(1);
    }
    else if (pid == 0)
    {
        printf("Child: PID = %d\n", getpid());
        printf("Child: x = %d\n", x);
        x += 5;
        printf("Child: Modified x = %d\n", x);
        _exit(0);
    }
    else
    {
        printf("Parent: PID = %d\n", getpid());
        printf("Parent: x = %d\n", x);
    }
    return 0;
}

15. Write a C program to create a pipeline between two processes using the pipe() system call.
#include <stdio.h>
#include <unistd.h>
#include <string.h>
int main()
{
    int fd[2];
    char message[] = "Hello from parent!";
    char buffer[100];
    pipe(fd);
    pid_t pid = fork();
    if (pid == 0)
    {
        close(fd[1]);
        read(fd[0], buffer, sizeof(buffer));
        printf("Child read: %s\n", buffer);
        close(fd[0]);
    }
    else
    {
        close(fd[0]);
        write(fd[1], message, strlen(message) + 1);
        close(fd[1]);
    }
    return 0;
}

16. Write a program in C to demonstrate the use of the nice() system call for adjusting process priority.
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/time.h>
#include <sys/resource.h>
#include <errno.h>
int main() {
    int priority;
    priority = getpriority(PRIO_PROCESS, 0);
    printf("Current priority (nice value): %d\n", priority);
    int new_priority = nice(5);
    if (new_priority == -1 && errno != 0) {
        perror("nice");
        exit(EXIT_FAILURE);
    }
    printf("New priority after nice(5): %d\n", new_priority);
    for (int i = 0; i < 3; i++) {
        printf("Process working with nice value: %d\n", new_priority);
        sleep(1);
    }
    return 0;
}

17. Write a C program to demonstrate the use of the clone() system call to create a thread.
#define _GNU_SOURCE
#include <sched.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <signal.h>
#include <sys/wait.h>
#define STACK_SIZE 1024*1024
int child_function(void *arg)
{
    printf("Hello from child process (clone)!\n");
    return 0;
}
int main()
{
    char *stack = malloc(STACK_SIZE);
    if (!stack) {
        perror("malloc");
        exit(1);
    }
    pid_t pid = clone(child_function, stack + STACK_SIZE, SIGCHLD, NULL);
    if (pid == -1)
    {
        perror("clone");
        free(stack);
        exit(1);
    }
    waitpid(pid, NULL, 0);
    printf("Hello from parent process!\n");
    free(stack);
    return 0;
}

18. Write a C program to create a child process using fork() and communicate between parent and child using pipes.
#include <stdio.h>
#include <unistd.h>
#include <string.h>
int main()
{
    int fd[2];
    char message[] = "Hello from parent!";
    char buffer[100];
    pipe(fd);
    pid_t pid = fork();
    if (pid == 0)
    {
        close(fd[1]);
        read(fd[0], buffer, sizeof(buffer));
        printf("Child received: %s\n", buffer);
        close(fd[0]);
    }
    else
    {
        close(fd[0]);
        write(fd[1], message, strlen(message) + 1);
        close(fd[1]);
    }
    return 0;
}

19. Write a C program to demonstrate process synchronization using the fork() and wait() system calls.
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>
int main()
{
    pid_t pid = fork();
    if (pid < 0)
    {
        perror("fork");
        return 1;
    }
    else if (pid == 0)
    {
        printf("Child process: Doing some work...\n");
        sleep(2);
        printf("Child process: Done!\n");
    }
    else
    {
        printf("Parent process: Waiting for child to complete...\n");
        wait(NULL);
        printf("Parent process: Child finished. Now parent continues.\n");
    }
    return 0;
}

20. Write a C program to create a process using fork() and change its scheduling policy using sched_setscheduler().
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sched.h>
#include <sys/types.h>
#include <errno.h>
#include <string.h>
int main()
{
    pid_t pid;
    struct sched_param param;
    pid = fork();
    if (pid < 0)
    {
        perror("fork failed");
        exit(EXIT_FAILURE);
    }
    if (pid == 0)
    {
        printf("Child process (PID %d)\n", getpid());
        param.sched_priority = 10;
        if (sched_setscheduler(0, SCHED_FIFO, &param) == -1)
        {
            fprintf(stderr, "Failed to set scheduler: %s\n", strerror(errno));
            exit(EXIT_FAILURE);
        }
        printf("Child: Scheduling policy changed to SCHED_FIFO with priority %d\n", param.sched_priority);
        for (int i = 0; i < 5; i++)
        {
            printf("Child working... %d\n", i);
            sleep(1);
        }

    }
    else
    {
        printf("Parent process (PID %d), child PID: %d\n", getpid(), pid);
        wait(NULL);
        printf("Parent: Child finished execution\n");
    }
    return 0;
}

21. Write a C program to create a child process using fork() and demonstrate inter-process communication (IPC) using shared memory.
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/types.h>
#include <unistd.h>
#include <string.h>
#define SHM_SIZE 1024
int main()
{
    key_t key;
    int shmid;
    char *shared_memory;
    key = ftok("shmfile", 65);
    if (key == -1) {
        perror("ftok");
        exit(1);
    }
    shmid = shmget(key, SHM_SIZE, 0666 | IPC_CREAT);
    if (shmid < 0)
    {
        perror("shmget");
        exit(1);
    }
    pid_t pid = fork();
    if (pid < 0)
    {
        perror("fork");
        exit(1);
    }
    if (pid == 0)
    {
        shared_memory = (char *) shmat(shmid, NULL, 0);
        if (shared_memory == (char *)(-1))
        {
            perror("shmat in child");
            exit(1);
        }
        printf("Child: Reading from shared memory...\n");
        printf("Child: Data = \"%s\"\n", shared_memory);
    shmdt(shared_memory);
    }
    else
    {
        shared_memory = (char *) shmat(shmid, NULL, 0);
        if (shared_memory == (char *)(-1))
        {
            perror("shmat in parent");
            exit(1);
        }
        const char *message = "Hello from parent process!";
        strncpy(shared_memory, message, SHM_SIZE);
        printf("Parent: Data written to shared memory.\n");
        wait(NULL);
        shmdt(shared_memory);
        shmctl(shmid, IPC_RMID, NULL);
        printf("Parent: Shared memory detached and removed.\n");
    }
    return 0;
}

22. Write a C program to demonstrate the use of the prctl() system call to change process attributes.
#define _GNU_SOURCE
#include <stdio.h>
#include <sys/prctl.h>
#include <string.h>
#include <unistd.h>
#include <stdlib.h>
int main()
{
    char name[17];
    if (prctl(PR_SET_NAME, "MyProcess", 0, 0, 0) == -1)
    {
        perror("prctl(PR_SET_NAME)");
        exit(EXIT_FAILURE);
    }
    printf("Process name set to \"MyProcess\"\n");
    if (prctl(PR_GET_NAME, name, 0, 0, 0) == -1)
    {
        perror("prctl(PR_GET_NAME)");
        exit(EXIT_FAILURE);
    }
    printf("Current process name: %s\n", name);
    sleep(5);
    return 0;
}

23. Write a C program to create a child process using fork() and demonstrate process synchronization using semaphores.
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <semaphore.h>
#include <sys/mman.h>
#include <sys/wait.h>
int main()
{
    sem_t *sem = mmap(NULL, sizeof(sem_t),
                      PROT_READ | PROT_WRITE,
                      MAP_SHARED | MAP_ANONYMOUS, -1, 0);
    if (sem == MAP_FAILED)
    {
        perror("mmap");
        exit(1);
    }
    sem_init(sem, 1, 0);
    pid_t pid = fork();
    if (pid < 0)
    {
        perror("fork");
        exit(1);
    }
    if (pid == 0)
    {
        printf("Child: Hello!\n");
        sleep(1);
        printf("Child: Done.\n");
        sem_post(sem);
    }
    else
    {
        sem_wait(sem);
        printf("Parent: Now it's my turn!\n");
        wait(NULL);
        sem_destroy(sem);
        munmap(sem, sizeof(sem_t));
    }
    return 0;
}
24. Write a C program to create a child process using fork() and demonstrate process communication using message queues. 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <unistd.h>
#include <sys/wait.h>
struct msg_buffer
{
    long msg_type;
    char msg_text[100];
};
int main()
{
    key_t key;
    int msgid;
    struct msg_buffer message;
    key = ftok("msgfile", 65);
    if (key == -1)
    {
        perror("ftok");
        exit(1);
    }
    msgid = msgget(key, 0666 | IPC_CREAT);
    if (msgid == -1)
    {
        perror("msgget");
        exit(1);
    }
    pid_t pid = fork();
    if (pid < 0)
    {
        perror("fork");
        exit(1);
    }
    if (pid == 0)
    {
        msgrcv(msgid, &message, sizeof(message.msg_text), 1, 0);
        printf("Child received message: %s\n", message.msg_text);
        msgctl(msgid, IPC_RMID, NULL);
    }
    else
    {
        strcpy(message.msg_text, "Hello from parent!");
        message.msg_type = 1;
        msgsnd(msgid, &message, sizeof(message.msg_text), 0);
        wait(NULL);
    }
    return 0;
}

25. Write a C program to create a child process using fork() and demonstrate process synchronization using condition variables.
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>
#include <sys/mman.h>
#include <sys/wait.h>
typedef struct {
    pthread_mutex_t mutex;
    pthread_cond_t cond;
    int done;
} shared_data;
int main()
{
    shared_data *data = mmap(NULL, sizeof(shared_data),
                             PROT_READ | PROT_WRITE,
                             MAP_SHARED | MAP_ANONYMOUS, -1, 0);
    if (data == MAP_FAILED)
    {
        perror("mmap");
        exit(1);
    }
    pthread_mutexattr_t mattr;
    pthread_condattr_t cattr;
    pthread_mutexattr_init(&mattr);
    pthread_mutexattr_setpshared(&mattr, PTHREAD_PROCESS_SHARED);
    pthread_condattr_init(&cattr);
    pthread_condattr_setpshared(&cattr, PTHREAD_PROCESS_SHARED);
    pthread_mutex_init(&data->mutex, &mattr);
    pthread_cond_init(&data->cond, &cattr);
    data->done = 0;
    pid_t pid = fork();
    if (pid < 0)
    {
        perror("fork");
        exit(1);
    }
    if (pid == 0)
    {
        sleep(1);
        pthread_mutex_lock(&data->mutex);
printf("Child: work done, signaling parent.\n");
        data->done = 1;
        pthread_cond_signal(&data->cond);
        pthread_mutex_unlock(&data->mutex);
    }
    else
    {
        pthread_mutex_lock(&data->mutex);
        while (data->done == 0)
        {
            pthread_cond_wait(&data->cond, &data->mutex);
        }
        printf("Parent: received signal from child.\n");
        pthread_mutex_unlock(&data->mutex);
        wait(NULL);
    }
    pthread_mutex_destroy(&data->mutex);
    pthread_cond_destroy(&data->cond);
    munmap(data, sizeof(shared_data));
    return 0;
}

26. Write a C program to create a child process using fork() and demonstrate process communication using sockets.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/socket.h>
int main() {
    int sv[2];  // sv[0] for parent, sv[1] for child

    if (socketpair(AF_UNIX, SOCK_STREAM, 0, sv) == -1) {
        perror("socketpair");
        exit(1);
    }

    pid_t pid = fork();

    if (pid < 0) {
        perror("fork");
        exit(1);
    }

    if (pid == 0) {
        // Child process
        close(sv[0]);  // Close parent's end

        char buffer[100];
        read(sv[1], buffer, sizeof(buffer));
        printf("Child received: %s\n", buffer);

        close(sv[1]);  // Close after use
    } else {
        // Parent process
        close(sv[1]);  // Close child's end

        const char *message = "Hello from parent via socket!";
        write(sv[0], message, strlen(message) + 1);

        wait(NULL);  // Wait for child to finish
        close(sv[0]);  // Close after use
    }

    return 0;
}
27. Write a C program to create a child process using fork() and demonstrate process synchronization using mutexes.
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>
#include <sys/mman.h>
#include <sys/wait.h>
int main()
{
    // Allocate shared memory for the mutex
    pthread_mutex_t *mutex = mmap(NULL, sizeof(pthread_mutex_t),
                                  PROT_READ | PROT_WRITE,
                                  MAP_SHARED | MAP_ANONYMOUS, -1, 0);

    if (mutex == MAP_FAILED) {
        perror("mmap");
        exit(1);
    }
    // Initialize mutex attributes for inter-process sharing
    pthread_mutexattr_t attr;
    pthread_mutexattr_init(&attr);
    pthread_mutexattr_setpshared(&attr, PTHREAD_PROCESS_SHARED);
    pthread_mutex_init(mutex, &attr);
    pid_t pid = fork();
    if (pid < 0) {
        perror("fork");
        exit(1);
    }
    if (pid == 0) {
        // Child process
        pthread_mutex_lock(mutex);
        printf("Child: Acquired lock. Doing work...\n");
        sleep(1);
        printf("Child: Releasing lock.\n");
        pthread_mutex_unlock(mutex);
    } else {
        // Parent process
        sleep(0.5); // Ensure child tries first (for demo)
        pthread_mutex_lock(mutex);
        printf("Parent: Acquired lock after child.\n");
        pthread_mutex_unlock(mutex);
    wait(NULL); // Wait for child
    }
    // Cleanup
    pthread_mutex_destroy(mutex);
    pthread_mutexattr_destroy(&attr);
    munmap(mutex, sizeof(pthread_mutex_t));
    return 0;
}

28. Write a C program to create a child process using fork() and demonstrate process communication using named pipes (FIFOs).
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <string.h>

#define FIFO_NAME "myfifo"
int main()
{
    pid_t pid;
    char message[] = "Hello from child!";
    char buffer[100];
    if (mkfifo(FIFO_NAME, 0666) == -1)
    {
        perror("mkfifo");
    }
    pid = fork();
    if (pid < 0)
    {
        perror("fork");
        exit(EXIT_FAILURE);
    }
    else if (pid == 0)
    {
        int fd = open(FIFO_NAME, O_WRONLY);
        if (fd == -1)
        {
            perror("Child: open");
            exit(EXIT_FAILURE);
        }
        write(fd, message, strlen(message) + 1);
        close(fd);
        printf("Child: Message sent.\n");
    }
    else
    {
    int fd = open(FIFO_NAME, O_RDONLY);
        if (fd == -1)
        {
            perror("Parent: open");
            exit(EXIT_FAILURE);
        }
        read(fd, buffer, sizeof(buffer));
        close(fd);
        printf("Parent: Received message: '%s'\n", buffer);
        unlink(FIFO_NAME);
    }
    return 0;
}
29. Write a C program to create a child process using fork() and demonstrate process communication using shared memory and semaphores
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/sem.h>

#define SHM_KEY 0x1234
#define SEM_KEY 0x5678
#define SHM_SIZE 100

union semun {
    int val;
};

void sem_wait(int semid) {
    struct sembuf sb = {0, -1, 0};  // wait
    semop(semid, &sb, 1);
}

void sem_signal(int semid) {
    struct sembuf sb = {0, 1, 0};   // signal
    semop(semid, &sb, 1);
}

int main() {
    int shmid, semid;
    char *shared_data;
    shmid = shmget(SHM_KEY, SHM_SIZE, IPC_CREAT | 0666);
    if (shmid == -1) {
        perror("shmget");
        exit(1);
    }
    semid = semget(SEM_KEY, 1, IPC_CREAT | 0666);
    if (semid == -1) {
        perror("semget");
        exit(1);
    }
union semun sem_union;
    sem_union.val = 0;
    semctl(semid, 0, SETVAL, sem_union);

    pid_t pid = fork();

    if (pid < 0) {
        perror("fork");
        exit(1);
    }
    else if (pid == 0) {
        shared_data = (char *)shmat(shmid, NULL, 0);
        if (shared_data == (char *)(-1)) {
            perror("shmat (child)");
            exit(1);
        }

        strcpy(shared_data, "Hello from child!");
        printf("Child: Written to shared memory.\n");

        sem_signal(semid); // Signal parent
        shmdt(shared_data); // Detach
    }

    else {
        // Parent process
        shared_data = (char *)shmat(shmid, NULL, 0);
        if (shared_data == (char *)(-1)) {
            perror("shmat (parent)");
            exit(1);
        }

        sem_wait(semid); // Wait for child
        printf("Parent: Read from shared memory: %s\n", shared_data);
         // Cleanup
        shmdt(shared_data);
        shmctl(shmid, IPC_RMID, NULL);
        semctl(semid, 0, IPC_RMID);
    }

    return 0;
}
```
