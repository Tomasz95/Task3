# Task3
import java.util.*;

public class Graph {

    private int V; // number of vertices
    private LinkedList<Integer>[] adjList; // adjacency list representation of the graph

    public Graph(int V) {
        this.V = V;
        adjList = new LinkedList[V];
        for (int i = 0; i < V; i++) {
            adjList[i] = new LinkedList<Integer>();
        }
    }

    // add an edge to the graph
    public void addEdge(int u, int v) {
        adjList[u].add(v);
        adjList[v].add(u);
    }

    // depth-first search to visit all the vertices reachable from a given vertex
    private void dfs(int v, boolean[] visited) {
        visited[v] = true;
        for (int u : adjList[v]) {
            if (!visited[u]) {
                dfs(u, visited);
            }
        }
    }

    // find the number of connected components in the graph
    public int numConnectedComponents() {
        boolean[] visited = new boolean[V];
        int numComponents = 0;
        for (int i = 0; i < V; i++) {
            if (!visited[i]) {
                dfs(i, visited);
                numComponents++;
            }
        }
        return numComponents;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt(); // number of edges
        Graph graph = new Graph(n);
        for (int i = 0; i < n; i++) {
            int u = scanner.nextInt();
            int v = scanner.nextInt();
            graph.addEdge(u, v);
        }
        System.out.println(graph.numConnectedComponents());
    }
}
