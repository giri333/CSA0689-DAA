#include <stdio.h>
#include <stdlib.h>
struct Edge {
    int src, dest, weight;
};
struct Subset {
    int parent;
    int rank;
};
int find(struct Subset subsets[], int i) {
    if (subsets[i].parent != i) {
        subsets[i].parent = find(subsets, subsets[i].parent);
    }
    return subsets[i].parent;
}
void unionSets(struct Subset subsets[], int x, int y) {
    int xroot = find(subsets, x);
    int yroot = find(subsets, y);
    if (subsets[xroot].rank < subsets[yroot].rank) {
        subsets[xroot].parent = yroot;
    } else if (subsets[xroot].rank > subsets[yroot].rank) {
        subsets[yroot].parent = xroot;
    } else {
        subsets[yroot].parent = xroot;
        subsets[xroot].rank++;
    }
}
int compareEdges(const void *a, const void *b) {
    return ((struct Edge *)a)->weight - ((struct Edge *)b)->weight;
}
void kruskalMST(int V, int E, struct Edge edges[]) {
    struct Subset *subsets = (struct Subset *)malloc(V * sizeof(struct Subset));
    for (int i = 0; i < V; i++) {
        subsets[i].parent = i;
        subsets[i].rank = 0;
    }
    qsort(edges, E, sizeof(struct Edge), compareEdges);
    struct Edge result[V];
    int resultIndex = 0;
    for (int i = 0; i < E && resultIndex < V - 1; i++) {
        int srcRoot = find(subsets, edges[i].src);
        int destRoot = find(subsets, edges[i].dest);
        if (srcRoot != destRoot) {
            result[resultIndex++] = edges[i];
            unionSets(subsets, srcRoot, destRoot);
        }
    }
    printf("Minimum Spanning Tree:\n");
    for (int i = 0; i < resultIndex; i++) {
        printf("%d - %d: %d\n", result[i].src, result[i].dest, result[i].weight);
    }
    free(subsets);
}
int main() {
    int V, E;
    printf("Enter the number of vertices and edges: ");
    scanf("%d %d", &V, &E);
    struct Edge edges[E];
    printf("Enter source, destination, and weight for each edge:\n");
    for (int i = 0; i < E; i++) {
        scanf("%d %d %d", &edges[i].src, &edges[i].dest, &edges[i].weight);
    }
    kruskalMST(V, E, edges);
    return 0;
}
