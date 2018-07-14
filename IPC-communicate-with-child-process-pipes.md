You can communicate PIPEs. It is another IPC mechanism.

**From linux manual:**
int pipe(int fd[2]) -- creates a pipe and returns two file descriptors, fd[0], fd[1]. fd[0] is opened for reading, fd[1] for writing.

### Code:

    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    #include <unistd.h>
    #include <sys/types.h>

    int main(void)
    {
        int     fd[2], nbytes;
        pid_t   pid;
        int arr[10]={0,};
        int readbuffer[10];
        int state, c, i, j;

        pipe(fd);

        if((pid = fork()) == -1)
        {
            printf("can't fork, error\n");
            exit(-1);
        }
        else if(pid == 0)
        {
                /* Child process closes up input side of pipe */
                close(fd[0]);

                /* Send "arr" through the output side of pipe */
                printf("\nProducer is created.\n");

                printf("array: ");
                for(c=0; c<10; c++)
                {
                    printf("%d ", arr[c]);
                    arr[c]=c+1;
                }

                write(fd[1], arr, (sizeof(int)*10));
                exit(0);
        }
        else
        {
                /* Parent process closes up output side of pipe */
                close(fd[1]);

                pid=wait(&state);
                sleep(1);
                printf("\nConsumer takes control of array");

                /* Read in arr from the pipe */
                nbytes = read(fd[0], arr, (sizeof(int)*10));

                printf("\narray:");

                for(j=0;j<10;j++) 
                {
                    printf(" %d", arr[j]);
                }

                printf("\nConsumer is done.");

                printf("\narray: ");
                for ( i =0; i<10; i++)
                {
                    arr[i]=-1;
                    printf("%d ", arr[i]);
                }
                printf("\ndone\n");
                exit(0);

        }

        return(0);
    }
