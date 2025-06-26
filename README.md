```c
#include <stdio.h>

// Structure to hold information about each process
struct Process {
    int pid;        // Process ID
    int bt;         // Burst Time
    int wt;         // Waiting Time
    int tat;        // Turnaround Time
};

// Function to swap two processes (used in sorting)sdsdd
void swap(struct Process *a, struct Process *b) {
    struct Process temp = *a;ssss
    *a = *b;
    *b = temp;
}

// Function to sort processes by burst time (SJF)
void sortByBurstTime(struct Process p[], int n) {
    for (int i = 0; i < n-1; i++) {
        for (int j = 0; j < n-i-1; j++) {
            if (p[j].bt > p[j+1].bt) {
                swap(&p[j], &p[j+1]);
            }
        }
    }
}

// Function to calculate waiting time for each process
void calculateWaitingTime(struct Process p[], int n) {
    p[0].wt = 0; // First process has 0 waiting time

    for (int i = 1; i < n; i++) {
        p[i].wt = p[i-1].wt + p[i-1].bt;
    }
}

// Function to calculate turnaround time for each process
void calculateTurnaroundTime(struct Process p[], int n) {
    for (int i = 0; i < n; i++) {
        p[i].tat = p[i].bt + p[i].wt;
    }
}

// Main function
int main() {
    int n;

    // Input number of processes
    printf("Enter number of processes: ");
    scanf("%d", &n);

    struct Process p[n]; // Array to store process info

    // Input burst time for each process
    for (int i = 0; i < n; i++) {
        p[i].pid = i + 1; // Assigning Process ID starting from 1
        printf("Enter burst time for Process %d: ", p[i].pid);
        scanf("%d", &p[i].bt);
    }

    // Sort processes by burst time (SJF logic)
    sortByBurstTime(p, n);

    // Calculate waiting and turnaround times
    calculateWaitingTime(p, n);
    calculateTurnaroundTime(p, n);

    // Display the results
    printf("\nSJF Scheduling (Non-Preemptive):\n");
    printf("PID\tBT\tWT\tTAT\n");

    float totalWT = 0, totalTAT = 0;

    for (int i = 0; i < n; i++) {
        printf("%d\t%d\t%d\t%d\n", p[i].pid, p[i].bt, p[i].wt, p[i].tat);
        totalWT += p[i].wt;
        totalTAT += p[i].tat;
    }

    // Display average waiting and turnaround times
    printf("\nAverage Waiting Time: %.2f\n", totalWT / n);
    printf("Average Turnaround Time: %.2f\n", totalTAT / n);

    return 0;
}
```
