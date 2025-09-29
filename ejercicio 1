import java.util.*;

public class CostosMinimos {
    static class Edge implements Comparable<Edge> {
        int u, v, w;
        Edge(int u, int v, int w) { this.u = u; this.v = v; this.w = w; }
        public int compareTo(Edge e) { return Integer.compare(this.w, e.w); }
    }

    public static void main(String[] args) {
        int[][] graph = generarGrafo(10, 15);
        int primCost = prim(graph);
        int kruskalCost = kruskal(graph);
        System.out.println("Prim: " + primCost + ", Kruskal: " + kruskalCost);
    }

    static int[][] generarGrafo(int n, int edges) {
        Random rand = new Random();
        int[][] graph = new int[n][n];
        for (int i = 0; i < edges; i++) {
            int u = rand.nextInt(n), v = rand.nextInt(n), w = rand.nextInt(20) + 1;
            if (u != v) graph[u][v] = graph[v][u] = w;
        }
        return graph;
    }

    static int prim(int[][] graph) {
        int n = graph.length, cost = 0;
        boolean[] visited = new boolean[n];
        PriorityQueue<Edge> pq = new PriorityQueue<>();
        pq.add(new Edge(0, 0, 0));
        
        while (!pq.isEmpty()) {
            Edge e = pq.poll();
            if (!visited[e.v]) {
                visited[e.v] = true;
                cost += e.w;
                for (int i = 0; i < n; i++) 
                    if (graph[e.v][i] > 0 && !visited[i]) 
                        pq.add(new Edge(e.v, i, graph[e.v][i]));
            }
        }
        return cost;
    }

    static int kruskal(int[][] graph) {
        int n = graph.length;
        List<Edge> edges = new ArrayList<>();
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                if (graph[i][j] > 0) edges.add(new Edge(i, j, graph[i][j]));
        Collections.sort(edges);
        
        int[] parent = new int[n];
        for (int i = 0; i < n; i++) parent[i] = i;
        
        int cost = 0, count = 0;
        for (Edge e : edges) {
            if (find(parent, e.u) != find(parent, e.v)) {
                union(parent, e.u, e.v);
                cost += e.w;
                if (++count == n - 1) break;
            }
        }
        return cost;
    }

    static int find(int[] parent, int x) {
        if (parent[x] != x) parent[x] = find(parent, parent[x]);
        return parent[x];
    }

    static void union(int[] parent, int x, int y) {
        parent[find(parent, x)] = find(parent, y);
    }
}
