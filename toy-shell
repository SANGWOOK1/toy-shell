#include <stdio.h>
#include <string.h>
#include <stdbool.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <pwd.h>
#include <errno.h>

#define MAX_LEN_LINE 100
#define LEN_HOST 50
#define SIZE 10000

int main(void)
{
    char command[MAX_LEN_LINE];
    char* arg1, * arg2, * arg3;
    char* args[] = { command, arg1, arg2, arg3,  NULL };
    int ret, status;
    pid_t pid, cpid;


    char hostname[LEN_HOST + 1];
    memset(hostname, 0X00, sizeof(hostname));
    gethostname(hostname, LEN_HOST);

    while (true) {
        char* s;
        int len;
        char dir[SIZE];
        char currentPath[_CS_PATH];
        getcwd(dir, sizeof(dir));

        printf("\033[34m%s\033[0m@%s:033[36m%s\033[0m$ ", getpwuid(getuid())->pw_name, hostname, dir);

        s = fgets(command, MAX_LEN_LINE, stdin);

        if (s == NULL) {
            fprintf(stderr, "fgets failed\n");
            exit(1);
        }

        len = strlen(command);
        printf("%d\n", len);

        if (command[len - 1] == '\n') {
            command[len - 1] = '\0';
        }

        if (!strcmp(command, "exit"))
            printf("program ended");
        exit(0);
    }



    arg1 = strtok(command, " ");

    if (!strcmp(command, "cd")) {

        arg1 = strtok(NULL, " ");

        if (chdir(arg1) < 0)
        {
            printf("No proper Directory[%s].\n", arg1);
        }
        else
        {
            printf("change Directory.\n");
        }
    }
    else if (fchdir(LEN_HOST)) {
        switch (errno) {
        case ENOENT:
            fprintf(stderr, "Unable to locate the directory: %s\n", arg1); break;
        case EINVAL:
            fprintf(stderr, "Invalid buffer. \n"); break;
        default:
            fprintf(stderr, "Unknown error.\n");
        }


        printf("[%s]\n", command);



        pid = fork();
        if (pid < 0) {
            fprintf(stderr, "fork failed\n");
            exit(1);
        }
        if (pid != 0) {  /* parent */
            cpid = waitpid(pid, &status, 0);
            if (cpid != pid) {
                fprintf(stderr, "waitpid failed\n");
            }
            printf("Child process terminated\n");
            if (WIFEXITED(status)) {
                printf("Exit status is %d\n", WEXITSTATUS(status));
            }
        }
        else {  /* child */
            args[0] = arg1;
            args[1] = NULL;
            args[2] = NULL;
            args[3] = NULL;

            ret = execve(args[0], args, NULL);
            if (ret < 0) {
                fprintf(stderr, "execve failed\n");
                return 1;
            }
        }
    }
}
