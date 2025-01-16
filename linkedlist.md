## Linked list

```c
#include <stdio.h>
#include <stdlib.h>

// Define a structure 'node' to represent each node in the singly linked list
typedef struct s{
    int data;          // To store the integer data in the node
    struct s *link;    // Self-referencing pointer to the next node in the list
}node;


node *head = NULL;

int countlist(){
    int count = 0;
    node *temp = head;
    while(temp !=NULL){
        temp = temp->link;
        count++;
    }
    printf("The Count of List is %d\n",count);
    return count;
}
node *memalloc(int d){
    node *new  = (node *) malloc(sizeof(node));
    if(new == NULL){
        printf("Memory not allocated");
        exit(1);
    }
    new->data = d;
    new->link = NULL;
    return new;
}

void insertfront(int d){
    node *new = memalloc(d);
    if(head == NULL){
        head = new;
        return;
    }
    new->link = head;
    head = new;
}

void insertend(int d){
    node *new = memalloc(d);
    node *temp = head;
    if (head == NULL) {
        head = new;
        return;
        }
    while(temp->link != NULL){
        temp = temp->link;
    }
    temp->link = new;
}
void deletefront(){
    if(head == NULL){
        printf("List is Empty\n");
        return;
    }
    node *temp = head;
    head = head->link;
    printf("The Deleted Node is : %d\n",temp->data);
    free(temp);
}
void deleteend(){
    if (head == NULL) {
        printf("List is Empty\n");
        return;
    }
    node *temp = head;
    node *prev = NULL;
    while(temp->link != NULL){
        prev = temp;
        temp = temp->link;
    }
    if(prev != NULL)
        prev->link = NULL;
    else
        head = NULL;
    printf("%d is Removed\n",temp->data);
    free(temp);
}
void insertAtPosition(){
    int pos, d;
    int count = countlist();

    if(count == 0){
        printf("List is empty\n");
        printf("Adding new node\n");
        printf("Enter the value: ");
        scanf("%d", &d);
        insertfront(d);
        return;
    }
    printf("Enter the position between 0 - %d: ", count);
    scanf("%d", &pos);
    if(pos < 0 || pos > count){
        printf("Invalid position. Position out of bounds.\n");
        return;
    }
    printf("Enter the value: ");
    scanf("%d", &d);
    if(pos == 0){
        insertfront(d);
        return;
    }
    if(pos == count){
        insertend(d);
        return;
    }

    node *new = memalloc(d);
    node *temp = head;

    for(int i = 1; i < pos; i++){
        temp = temp->link;
    }
    new->link = temp->link;
    temp->link = new;
}
void printlist(){
    printf("Your Elements are : ");
    node *temp = head;
    while(temp !=NULL){
        printf("%d ", temp->data);
        temp = temp->link;
    }
    printf("\n");
}

int main(){
    int option, data;
    while(1){
        printf("1. Insert Front\n2. Insert End\n3. Insert at Position\n4. Delete Front\n5. Delete End\n6. Display List\n7. Exit\n");
        printf("Enter your option: ");
        scanf("%d", &option);
        switch(option){
            case 1:
                printf("Enter the value: ");
                scanf("%d", &data);
                insertfront(data);
                break;
            case 2:
                printf("Enter the value: ");
                scanf("%d", &data);
                insertend(data);
                break;
            case 3:
                insertAtPosition();
                break;
            case 4:
                deletefront();
                break;
            case 5:
                deleteend();
                break;
            case 6:
                printlist();
                break;
            case 7:
                exit(0);
            default:
                printf("Invalid option\n");
        }
    }
    return 0;
}

```
