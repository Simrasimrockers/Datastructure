### Graph 

```c
#include <stdio.h>
#include <stdlib.h>
void createGraph(int vertices,int graph[vertices][vertices]) {
    for (int i = 0; i < vertices; i++) {
        for (int j = 0; j < vertices; j++) {
            graph[i][j] = 0;
        }
    }
}
void addEdge(int vertices,int graph[vertices][vertices], int src, int dest) {
    graph[src][dest] = 1;
    graph[dest][src] = 1;
}

void printGraph( int vertices,int graph[vertices][vertices]) {
    for (int i = 0; i < vertices; i++) {
        for (int j = 0; j < vertices; j++) {
            printf("%d ", graph[i][j]);
        }
        printf("\n");
    }
}

int main() {
    int vertices;

    printf("Enter the vertices : ");
    scanf("%d",&vertices);

    int graph[vertices][vertices];
    createGraph(vertices,graph );

    addEdge(vertices,graph, 0, 1);
    addEdge(vertices,graph, 0, 4);
    addEdge(vertices,graph, 1, 2);
    addEdge(vertices,graph, 1, 3);
    addEdge(vertices,graph, 1, 4);
    addEdge(vertices,graph, 2, 3);
    addEdge(vertices,graph, 3, 4);

    printf("Adjacency Matrix Representation of the Graph:\n");
    printGraph( vertices,graph);

    return 0;
}

```

### BFS 

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX_VERTICES 5

void createGraph(int graph[MAX_VERTICES][MAX_VERTICES], int vertices) {

    for (int i = 0; i < vertices; i++) {
        for (int j = 0; j < vertices; j++) {
            graph[i][j] = 0;
        }
    }
}

void addEdge(int graph[MAX_VERTICES][MAX_VERTICES], int src, int dest) {
    graph[src][dest] = 1;
    graph[dest][src] = 1;
}

void BFS(int graph[MAX_VERTICES][MAX_VERTICES], 
    int visited[MAX_VERTICES], int start, int vertices) {
        
    int queue[MAX_VERTICES];
    int front = 0, rear = 0;

    visited[start] = 1;
    queue[rear++] = start;

    while (front != rear) {
        int vertex = queue[front++];

        printf("%d ", vertex);

        for (int i = 0; i < vertices; i++) {
            if (graph[vertex][i] == 1 && !visited[i]) {
                visited[i] = 1;
                queue[rear++] = i;
            }
        }
    }
}

int main() {
    int graph[MAX_VERTICES][MAX_VERTICES];
    int visited[MAX_VERTICES] = {0};
    int vertices = MAX_VERTICES;

    createGraph(graph, vertices);

    addEdge(graph, 0, 1);
    addEdge(graph, 0, 4);
    addEdge(graph, 1, 2);
    addEdge(graph, 1, 3);
    addEdge(graph, 1, 4);
    addEdge(graph, 2, 3);
    addEdge(graph, 3, 4);

    for (int i = 0; i < vertices; i++) {
        visited[i] = 0;
    }

    printf("BFS Traversal starting from vertex 0: ");
    BFS(graph, visited, 0, vertices);
    printf("\n");


    return 0;
}

```
**Problem Statement: Simple Social Network Model in C**

Design a simple social network model in C using an undirected graph. In this network:
- Each person is represented as a node (or vertex).
- Each friendship between two people is represented as an undirected edge between their respective nodes.

**Requirements:**
1. **Graph Representation**: Use an adjacency list to represent the graph structure.

2. **Core Functions**:
   - **`addFriend(int user1, int user2)`**: Establish a friendship between `user1` and `user2`. This function should create an undirected edge between the two users, indicating a friendship. Self-friendships (i.e., a user being friends with themselves) should not be allowed.
   
   - **`viewConnections(int user)`**: List all direct friends of a given user.
   
   - **`suggestFriends(int user)`**: Suggest potential friends for the given user based on mutual connections. A mutual friend is defined as someone who is a friend of a friend but not a direct friend of the user.

3. **Program Execution**:
   - Input the number of users in the network.
   - Input an initial list of friendships to initialize the graph.
   - Display a menu allowing the user to:
     1. View friends of a specific user.
     2. Add a new friendship between two users.
     3. Get friend suggestions for a user based on mutual connections.
---
