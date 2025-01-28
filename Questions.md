### 1. Write a program to find the node where two singly linked lists intersect.
```c
#include <stdio.h>
#include <stdlib.h>
typedef struct s1{
    int data;
    struct s1 *link;
}node;
node *head1 = NULL;
node *head2 = NULL;
node *memalloc(int d){
    node *new = (node*)malloc(sizeof(node));
    if(new == NULL){
        printf("Memory not allocated");
        exit (0);
    }
    new -> data = d;
    new -> link = NULL;
    return new;
}
void insertend(int d,node **head){
    node *new = memalloc(d);
    node *temp = *head;
    if(*head == NULL){
        *head = new;
        return;
    }
    while(temp->link != NULL){
        temp = temp->link;
    }
    temp->link = new;
}
void sort_data(node **head) {
    int swapped, tempData;
    node *temp;
    node *ptr1 = *head;
    if (ptr1 == NULL) {
        return;
    }
    do {
        swapped = 0;
        temp = *head;
        while (temp->link != NULL) {
            if (temp->data > temp->link->data) {
                tempData = temp->data;
                temp->data = temp->link->data;
                temp->link->data = tempData;
                swapped = 1;
            }
            temp = temp->link;
        }
    } while (swapped);
}


node* intersection(node *head1, node *head2){
    if (head1 == NULL || head2 == NULL){
        printf("One of the list is empty");
        return;
    }
    sort_data(&head1);
    sort_data(&head2);
    printf("\nSorted List : ");
    display(head1);
    printf("\nSorted List : ");
    display(head2);
    node *temp1 = head1;
    node *temp2 = head2;
    printf("The two list intersection elements are : ");
    while (temp1 != NULL && temp2 != NULL){
        if(temp1 -> data == temp2->data){
            printf("%d",temp1->data);
            temp1 = temp1->link;
            temp2 = temp2 -> link;
        }
        else if(temp1 ->data < temp2 -> data){
            temp1 = temp1->link;
        }
        else{
            temp2 = temp2->link;
        }
    }
}

void display(node *head){
    printf("Your data Elements are : ");
    node *temp = head;
    while(temp != NULL){
        printf("%d ",temp->data);
        temp = temp->link;
    }
    printf("\n");
}

int main(){
    int d,n,m;
    printf("Enter the number of nodes : ");
    scanf("%d",&n);
    for(int i=0;i<n;i++){
            printf("Enter the Value : ");
            scanf("%d",&d);
            insertend(d,&head1);
    }
    printf("Enter the number of nodes : ");
    scanf("%d",&m);
    for(int i=0;i<m;i++){
            printf("Enter the Value : ");
            scanf("%d",&d);
            insertend(d,&head2);
    }
    display(head1);
    display(head2);
    intersection(head1,head2);
    return 0;
}
```

### 2. Implement a function to merge two sorted linked lists into one sorted list.
```c
#include <stdio.h>
#include <stdlib.h>
typedef struct s1{
    int data;
    struct s1 *link;
}node;
node *head1 = NULL;
node *head2 = NULL;
node *memalloc(int d){
    node *new = (node*)malloc(sizeof(node));
    if(new == NULL){
        printf("Memory not allocated");
        exit (0);
    }
    new -> data = d;
    new -> link = NULL;
    return new;
}
void insertend(int d,node **head){
    node *new = memalloc(d);
    node *temp = *head;
    if(*head == NULL){
        *head = new;
        return;
    }
    while(temp->link != NULL){
        temp = temp->link;
    }
    temp->link = new;
}
void sort_data(node **head) {
    int swapped, tempData;
    node *temp;
    node *ptr1 = *head;
    if (ptr1 == NULL) {
        return;
    }
    do {
        swapped = 0;
        temp = *head;
        while (temp->link != NULL) {
            if (temp->data > temp->link->data) {
                tempData = temp->data;
                temp->data = temp->link->data;
                temp->link->data = tempData;
                swapped = 1;
            }
            temp = temp->link;
        }
    } while (swapped);
}

void mergelist(node *head1,node *head2){

    if (head1 == NULL || head2 == NULL){
        printf("One of the list is empty");
        return;
    }
    sort_data(&head1);
    sort_data(&head2);

    node *temp1 = head1;
    while(temp1->link != NULL){
        temp1 = temp1->link;
    }
    temp1->link = head2;
    printf("\n\nMerged List before Sorting\n");
    display(head1);
    printf("\n\nMerged List After Sorting\n");
    sort_data(&head1);
    display(head1);

}


void display(node *head){
    printf("Your data Elements are : ");
    node *temp = head;
    while(temp != NULL){
        printf("%d ",temp->data);
        temp = temp->link;
    }
    printf("\n");
}

int main(){
    int d,n,m;
    printf("Enter the number of nodes : ");
    scanf("%d",&n);
    for(int i=0;i<n;i++){
            printf("Enter the Value : ");
            scanf("%d",&d);
            insertend(d,&head1);
    }
    printf("Enter the number of nodes : ");
    scanf("%d",&m);
    for(int i=0;i<m;i++){
            printf("Enter the Value : ");
            scanf("%d",&d);
            insertend(d,&head2);
    }
    display(head1);
    display(head2);
    mergelist(head1,head2);
    return 0;
}
```






# Date 28/01/2025
### Question

Write a C program to check if a given string of parentheses is **balanced**. The string may contain the following types of brackets: `()`, `[]`, and `{}`. A string is considered balanced if:
1. Every opening bracket has a corresponding closing bracket.
2. The brackets are closed in the correct order.

### Example Input and Output

- **Input**: `{[()]}`
  - **Output**: Balanced

- **Input**: `[(])`
  - **Output**: Not Balanced

---

## Practice Questions

### 1. Find Two Indices for Sum

**Description:**  
Given an array of integers, your task is to find two indices such that the numbers at those indices add up to a specific target value. Return the indices of these two numbers. If no such indices exist, return an indication (e.g., `-1`).

**Test Cases:**
- **Input:** `[1, 2, 1, 5, 6]`, **Target:** `7`  
  **Output:** `[3, 4]` (since `5 + 6 = 11`)

- **Input:** `[2, 7, 11, 15]`, **Target:** `9`  
  **Output:** `[0, 1]` (since `2 + 7 = 9`)

- **Input:** `[1, 3, 4, 2]`, **Target:** `6`  
  **Output:** `[-1]` (no such indices exist)

### 2. Check Anagrams

**Description:**  
Write a program that reads two strings from the user and checks if they are anagrams of each other. Anagrams are words or phrases that contain the same characters in a different order.

**Test Cases:**
- **Input:** `"listen"`, `"silent"`  
  **Output:** `True` (they are anagrams)

- **Input:** `"hello"`, `"world"`  
  **Output:** `False` (they are not anagrams)

- **Input:** `"rail safety"`, `"fairy tales"`  
  **Output:** `True` (they are anagrams)

### 3. FizzBuzz Program

**Description:**  
Write a program that prints numbers from `1` to `n`. For multiples of `3`, print "Fizz"; for multiples of `5`, print "Buzz"; and for numbers that are multiples of both, print "FizzBuzz".

**Test Cases:**
- **Input:** `n = 15`  
  **Output:** `1 2 Fizz 4 Buzz Fizz 7 8 Fizz Buzz 11 Fizz 13 14 FizzBuzz`

- **Input:** `n = 5`  
  **Output:** `1 2 Fizz 4 Buzz`

- **Input:** `n = 20`  
  **Output:** `1 2 Fizz 4 Buzz Fizz 7 8 Fizz Buzz 11 Fizz 13 14 FizzBuzz 16 17 Fizz 19 Buzz`

### 4. Maximize Stock Profit

**Description:**  
Given an array `prices` where `prices[i]` is the price of a stock on the `i`-th day, write a program to maximize the profit by buying one stock on one day and selling it on a different day in the future. Return the maximum profit you can achieve. If no profit can be made, return `0`.

**Test Cases:**
- **Input:** `[7, 1, 5, 3, 6, 4]`  
  **Output:** `5` (buy at `1` and sell at `6`)

- **Input:** `[7, 6, 4, 3, 1]`  
  **Output:** `0` (no profit can be made)

- **Input:** `[1, 2, 3, 4, 5]`  
  **Output:** `4` (buy at `1` and sell at `5`)

- **Input:** `[3, 2, 6, 5, 0, 3]`  
  **Output:** `4` (buy at `2` and sell at `6`)


