
# EX 5E Minimum Spanning Tree -Boruvka's Algorithm
## DATE: 08/09/2026
## AIM:
To write a Java program to for given constraints.
Boruvka's Algorithm - Minimum Spanning Tree

Find the MST using Boruvka's Algorithm for a weighted undirected graph.
<br />
<br />
<img width="292" height="235" alt="image" src="https://github.com/user-attachments/assets/06246b27-37a9-40a8-bd7a-37a1d5187cd1" />

## Algorithm

1. **Start**
2. Read the number of vertices `V` and edges, initialize each vertex as a separate component, and set `mstWeight = 0`.
3. For each component, find the cheapest outgoing edge connecting it to another component.
4. Store the cheapest edge for both components connected by each candidate edge.
5. Add each selected cheapest edge to the MST if it connects two different components.
6. Update the total MST weight, merge the connected components using Union-Find, and decrease the component count.
7. Repeat the process until only one component remains.
8. Display the selected MST edges and the total MST weight.
9. **End**

## Program:
```
/*
Program to implement Reverse a String
Developed by: Vishwaraj G
Register Number: 212223220125
*/
import java.util.*;

public class BoruvkaMST {
    static int[] parent;

    static int find(int i) {
        if (parent[i] != i)
            parent[i] = find(parent[i]);
        return parent[i];
    }

    static void union(int x, int y) {
        parent[find(x)] = find(y);
    }

    
    static int boruvkaMST(int V, List<Edge> edges) {
        //Type your code here
        parent = new int[V];
        for (int i = 0; i < V; i++) parent[i] = i;

        int components = V;
        int mstWeight = 0;

        while (components > 1) {
            Edge[] cheapest = new Edge[V];
            // Find cheapest edge for each component
            for (Edge e : edges) {
                int set1 = find(e.src), set2 = find(e.dest);
                if (set1 == set2) continue;

                if (cheapest[set1] == null || cheapest[set1].weight > e.weight)
                    cheapest[set1] = e;

                if (cheapest[set2] == null || cheapest[set2].weight > e.weight)
                    cheapest[set2] = e;
            }
            // Add cheapest edges to MST and union the components
            for (int i = 0; i < V; i++) {
                Edge e = cheapest[i];
                if (e != null && find(e.src) != find(e.dest)) {
                    mstWeight += e.weight;
                    union(e.src, e.dest);
                    components--;
                    System.out.println("Edge: " + e.src + "-" + e.dest + " Weight: " + e.weight);
                }
            }
        }
        return mstWeight;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int V = sc.nextInt();
        int E = sc.nextInt();

        List<Edge> edges = new ArrayList<>();
        for (int i = 0; i < E; i++) {
            edges.add(new Edge(sc.nextInt(), sc.nextInt(), sc.nextInt()));
        }

        int totalWeight = boruvkaMST(V, edges);
        System.out.println("Total Weight of MST: " + totalWeight);

        sc.close();
    }
}

class Edge {
    int src, dest, weight;
    Edge(int s, int d, int w) {
        src = s; dest = d; weight = w;
    }
}
```

## Output:

<img width="476" height="283" alt="image" src="https://github.com/user-attachments/assets/35e724b4-4b49-4e10-852d-8c5c5079a8a9" />


## Result:
The program successfully implemented and the expected output is verified.
