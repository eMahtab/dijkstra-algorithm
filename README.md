# Dijkstra Algorithm



# Implementation :
```java
import java.util.*;

public class App {

	public static void main(String[] args) {
		int numberOfVertices = 6;
		int[][] edges = {
			    {0, 1, 7},
			    {0, 3, 5},
			    {3, 2, 3},
			    {1, 4, 8},
			    {2, 4, 4},
			    {4, 5, 5}
			    
			};
		int startingVertex = 0;
		findShortestPath(numberOfVertices, edges, startingVertex);

	}
	
	public static void findShortestPath(int n, int[][] edges, int src) {
		// Build the adjacency matrix
		int adjMatrix[][] = new int[n][n];
		for (int[] edge: edges) {
		    adjMatrix[edge[0]][edge[1]] = edge[2];
		}

		// Shortest distances array
		int[] distances = new int[n];
		Arrays.fill(distances, Integer.MAX_VALUE);
		distances[src] = 0; // distance of source vertex from source vertex will be zero


		// The priority queue would contain (vertex, cost)
		PriorityQueue<int[]> minHeap = new PriorityQueue<int[]>((a, b) -> a[1] - b[1]);
		minHeap.offer(new int[]{src, 0});
        
		 while (!minHeap.isEmpty()) { 
		    int[] node = minHeap.poll();
		    int vertex = node[0];
		    int distance = node[1];
		    System.out.println("Shortest path from vertex : V" + src + 
				" to vertex V" + vertex +" with distance " + distance); 

		    // Examine and relax all neighboring vertices if possible 
		    for (int v = 0; v < n; v++) {
			if (adjMatrix[vertex][v] > 0) {
			    int dU = distance, dUV = adjMatrix[vertex][v], dV = distances[v];
			    // Better path?
			    if (dU + dUV < dV) {
				minHeap.offer(new int[]{v, dU + dUV});
				distances[v] = dU + dUV;
			    }
			}
		    }
		 }
         }

}

```

![Shortest Path - Dijkstra Algorithm](graph-1.jpg?raw=true "Shortest Path")

### Code execution Output
```
Shortest path from vertex : V0 to vertex V0 with distance 0
Shortest path from vertex : V0 to vertex V3 with distance 5
Shortest path from vertex : V0 to vertex V1 with distance 7
Shortest path from vertex : V0 to vertex V2 with distance 8
Shortest path from vertex : V0 to vertex V4 with distance 12
Shortest path from vertex : V0 to vertex V4 with distance 15
Shortest path from vertex : V0 to vertex V5 with distance 17
```

![Shortest Path - Dijkstra Algorithm](graph-2.jpg?raw=true "Shortest Path")
