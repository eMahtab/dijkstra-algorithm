# Dijkstra Algorithm

Single Source Shortest Path in a directed graph with non-negative weights using a Priority Queue (Min Heap)

**❗❗❗ Remember Dijkstra's algorithm doesn't work with negative weights.

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
		// Build the adjacency matrix.
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
		 for(int v = 0; v < n; v++) {
           	      System.out.println("Shortest path from vertex : V" + src + 
     				" to vertex V" + v +" with distance " + distances[v]); 
        	 }
         }

}

```

![Shortest Path - Dijkstra Algorithm](graph-1.jpg?raw=true "Shortest Path")

### Code execution Output
```
Shortest path from vertex : V0 to vertex V0 with distance 0
Shortest path from vertex : V0 to vertex V1 with distance 7
Shortest path from vertex : V0 to vertex V2 with distance 8
Shortest path from vertex : V0 to vertex V3 with distance 5
Shortest path from vertex : V0 to vertex V4 with distance 12
Shortest path from vertex : V0 to vertex V5 with distance 17
```

## Example 2 :

![Shortest Path - Dijkstra Algorithm](graph-2.jpg?raw=true "Shortest Path")

```java
public static void main(String[] args) {
		int numberOfVertices = 5;
		int[][] edges = {
				{0,1,10},
				{0,4,3},
				{4,1,1},
				{1,4,4},
				{1,2,2},
				{4,2,8},
				{4,3,2},
				{3,2,7},
				{2,3,9}
				};
		int startingVertex = 0;
		findShortestPath(numberOfVertices, edges, startingVertex);
}
```

### Code execution Output
```
Shortest path from vertex : V0 to vertex V0 with distance 0
Shortest path from vertex : V0 to vertex V1 with distance 4
Shortest path from vertex : V0 to vertex V2 with distance 6
Shortest path from vertex : V0 to vertex V3 with distance 5
Shortest path from vertex : V0 to vertex V4 with distance 3
```

## Improvement : Using visited boolean array
We don't want to visit an already visited vertex again, beacuse the weights are non-negative, so it will not result in shortest weights path.
So it doesn't make sense, to try to visit an already visited vertex from a different path.
```java
public static void findShortestPath(int n, int[][] edges, int src) {
	boolean[] visited = new boolean[n];
        // Build the adjacency matrix
        int adjMatrix[][] = new int[n][n];
        for (int[] edge: edges) {
            adjMatrix[edge[0]][edge[1]] = edge[2];
        }
        
        // Shortest distances array
        int[] distances = new int[n];
        Arrays.fill(distances, Integer.MAX_VALUE);
        distances[src] = 0;
        
        
        // The priority queue would contain (vertex, cost)
        PriorityQueue<int[]> minHeap = new PriorityQueue<int[]>((a, b) -> a[1] - b[1]);
        minHeap.offer(new int[]{src, 0});
        
         while (!minHeap.isEmpty()) { 
            int[] node = minHeap.poll();
            int vertex = node[0];
            if(visited[vertex])
            	continue;
            visited[vertex] = true;
            int distance = node[1];
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
         for(int v = 0; v < n; v++) {
           System.out.println("Shortest path from vertex : V" + src + 
     		" to vertex V" + v +" with distance " + distances[v]); 
         }
    }

```

## References :
1. https://www.youtube.com/watch?v=sD0lLYlGCJE (Very good explanation)


