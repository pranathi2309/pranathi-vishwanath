#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Student {
    int id;
    char name[50];
    float marks;
};

void addStudent() {
    struct Student s;
    FILE *fp = fopen("students.dat", "ab");
    printf("Enter ID: ");
    scanf("%d", &s.id);
    printf("Enter Name: ");
    scanf("%s", s.name);
    printf("Enter Marks: ");
    scanf("%f", &s.marks);
    fwrite(&s, sizeof(s), 1, fp);
    fclose(fp);
    printf("Record Added Successfully!\n");
}

void displayStudents() {
    struct Student s;
    FILE *fp = fopen("students.dat", "rb");
    if (!fp) { printf("No records found!\n"); return; }
    printf("\nID\tName\tMarks\n");
    while (fread(&s, sizeof(s), 1, fp)) {
        printf("%d\t%s\t%.2f\n", s.id, s.name, s.marks);
    }
    fclose(fp);
}

int main() {
    int choice;
    while (1) {
        printf("\n1. Add Student\n2. Display Students\n3. Exit\nChoose: ");
        scanf("%d", &choice);
        switch (choice) {
            case 1: addStudent(); break;
            case 2: displayStudents(); break;
            case 3: exit(0);
            default: printf("Invalid Choice!\n");
        }
    }
    return 0;
}
