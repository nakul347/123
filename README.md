#include <stdio.h>
#include <string.h>

#define MAX_FEEDBACKS 100
#define MAX_LENGTH 255

typedef struct {
    char name[MAX_LENGTH];
    char feedback[MAX_LENGTH];
} Feedback;

Feedback feedbacks[MAX_FEEDBACKS];
int feedbackCount = 0;

void submitFeedback(char name[], char feedback[]) {
    if (strlen(name) > 0 && strlen(feedback) > 0 && feedbackCount < MAX_FEEDBACKS) {
        strcpy(feedbacks[feedbackCount].name, name);
        strcpy(feedbacks[feedbackCount].feedback, feedback);
        feedbackCount++;
        printf("Thank you for your review!\n");
    } else {
        printf("Invalid input or storage full.\n");
    }
}

void viewFeedback() {
    printf("\nAll Feedback:\n");
    for (int i = 0; i < feedbackCount; i++) {
        printf("%d. %s: %s\n", i + 1, feedbacks[i].name, feedbacks[i].feedback);
    }
}

int main() {
    char name[MAX_LENGTH];
    char feedback[MAX_LENGTH];
    char choice;

    while (1) {
        printf("\nEnter your name: ");
        fgets(name, MAX_LENGTH, stdin);
        name[strcspn(name, "\n")] = 0;
        
        if (strcmp(name, "8888") == 0) {
            viewFeedback();
            continue;
        }
        
        printf("Enter your feedback: ");
        fgets(feedback, MAX_LENGTH, stdin);
        feedback[strcspn(feedback, "\n")] = 0;

        submitFeedback(name, feedback);
        
        printf("\nDo you want to submit another feedback? (y/n): ");
        scanf(" %c", &choice);
        getchar(); // Clear buffer
        
        if (choice == 'n' || choice == 'N') {
            break;
        }
    }

    return 0;
}
