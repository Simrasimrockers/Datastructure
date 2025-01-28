# Queue

- **Definition:**  
  A queue is a linear data structure that organizes data in a specific order.

- **Order of Organization:**  
  Queues operate on a First-In-First-Out (FIFO) or Last-In-Last-Out (LILO) principle, meaning that the first element added to the queue will be the first one to be removed.

- **Operations:**
  - **Insertion (Enqueue):**  
    New elements are added to the rear (or back) of the queue.
  
  - **Deletion (Dequeue):**  
    Elements are removed from the front of the queue.

- **Usage:**  
  Queues are commonly used in scenarios such as scheduling processes in operating systems, managing requests in web servers, and handling asynchronous data transfer in communication systems.

--- 

Here’s a structured question based on the provided code:

### Question: Implement a Queue Using a Linked List

**Description:**  
Write a program to implement a queue data structure using a singly linked list in C. The program should support the following operations:

1. **Enqueue:** Insert an element at the rear of the queue.
2. **Dequeue:** Remove an element from the front of the queue.
3. **Display:** Print all elements in the queue.

---

### Code

```c
#include <stdio.h>
#include <stdlib.h>
typedef struct s1{
    int data;
    struct s1 *link;
}node;
node *front = NULL;
node *rear = NULL;
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
void enqueue(int d){
    node *new = memalloc(d);
    if(front == NULL){
        front = new;
        rear = new;
        return;
    }
    rear->link = new;
    rear = new;
}
void dequeue(){
    if (front == NULL) {
        printf("Queue is empty, nothing to dequeue.\n");
        return;
    }
    node *temp = front;
    front = temp->link ;
    free(temp);
}
void display(){
    printf("Your data Elements are : ");
    node *temp = front;
    while(temp != NULL){
        printf("%d ",temp->data);
        temp = temp->link;
    }
    printf("\n");
}
int main(){
    int d,n;
    printf("Enter the number of nodes : ");
    scanf("%d",&n);
    for(int i=0;i<n;i++){
            printf("Enter the Value : ");
            scanf("%d",&d);
            enqueue(d);
    }
    display();
    dequeue();
    dequeue();
    display();
    return 0;
}

```
Here’s a well-structured question based on the provided code:

### Question: Implement a Queue Using a Doubly Linked List

**Description:**  
Write a program to implement a queue data structure using a doubly linked list in C. The program should support the following operations:

1. **Enqueue:** Insert an element at the rear of the queue.
2. **Dequeue:** Remove an element from the front of the queue.
3. **Handle Empty Queue:** Properly manage situations when attempting to dequeue from an empty queue.

---

### Code

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct dll {
    int data;
    struct dll *nlink;
    struct dll *plink;
} node;

node *rear = NULL;
node *front = NULL;

node *memalloc(int d) {
    node *new = (node *)malloc(sizeof(node));
    if (new == NULL) {
        printf("Memory not allocated\n");
        exit(0);
    }
    new->data = d;
    new->nlink = NULL;
    new->plink = NULL;
    return new;
}

void enqueue(int d) {
    node *new = memalloc(d);
    if (rear == NULL) {
        front = rear = new;
    } else {
        rear->nlink = new;
        new->plink = rear;
        rear = new;
    }
    printf("Enqueued %d into Queue\n", d);
}

int dequeue() {
    if (front == NULL) {
        printf("Queue is empty\n");
        return -1;
    }

    int value = front->data;
    node *temp = front;
    front = front->nlink;

    if (front != NULL) {
        front->plink = NULL;
    } else {
        rear = NULL;
    }

    printf("Dequeued %d from Queue\n", value);
    free(temp);
    return value;
}

int main() {
    enqueue(10);
    enqueue(20);
    enqueue(30);
    dequeue();
    dequeue();
    dequeue();
    dequeue();
    return 0;
}
```


### Question: Implement a Queue Using a Array

```c
#include <stdio.h>
#include <stdlib.h>

#define SIZE 5
int queue[SIZE];
int front = -1;
int rear = -1;

int isFull() {
    return rear == SIZE - 1;
}

int isEmpty() {
    return front == -1 || front > rear;
}

void enqueue(int value) {
    if (isFull()) {
        printf("Queue is full. Cannot enqueue %d\n", value);
        return;
    }

    if (front == -1 && rear == -1) {
        front = rear = 0;
        queue[rear] = value;
        printf("Enqueued %d\n", value);
        return;
    }
    else{
        rear++;
        queue[rear] = value;
        printf("Enqueued %d\n", value);
    }

}

int dequeue() {
    if (isEmpty()) {
        printf("Queue is empty. Cannot dequeue.\n");
        return -1;
    }

    int value = queue[front];
    front++;
    if (front > rear) {
        front = rear = -1;
    }

    return value;
}

void display() {
    if (isEmpty()) {
        printf("Queue is empty.\n");
        return;
    }

    printf("Queue elements: ");
    for (int i = front; i <= rear; i++) {
        printf("%d ", queue[i]);
    }
    printf("\n");
}


int main() {
    enqueue(10);
    enqueue(20);
    enqueue(30);
    enqueue(40);
    enqueue(50);
    display();
    printf("Dequeued: %d\n", dequeue());
    display();
    enqueue(60);
    display();
    return 0;
}
```
