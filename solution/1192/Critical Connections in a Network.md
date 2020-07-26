## Solution
### Java
```java
class Solution {
    public List<List<Integer>> criticalConnections(int n, List<List<Integer>> connections) {
        List<Integer>[] graph = new ArrayList[n];
        for (int i = 0; i < n; i++) {
            graph[i] = new ArrayList<>();
        }
        for (List<Integer> connection : connections) {
            graph[connection.get(0)].add(connection.get(1));
            graph[connection.get(1)].add(connection.get(0));
        }
        HashSet<List<Integer>> connectionSet = new HashSet<>(connections);
        int[] rank = new int[n];
        Arrays.fill(rank, -2);
        dfs(graph, 0, 0, rank, connectionSet);
        return new ArrayList<>(connectionSet);
    }
    
    private int dfs(List<Integer>[] graph, int node, int depth, int[] rank, HashSet<List<Integer>> connectionSet) {
        if (rank[node] >= 0) {
            return rank[node];
        }
        
        rank[node] = depth;
        int minDepthFound = depth;
        for (Integer neighbor : graph[node]) {
            if (rank[neighbor] == depth - 1) {
                continue;
            }
            int minDepth = dfs(graph, neighbor, depth + 1, rank, connectionSet);
            minDepthFound = Math.min(minDepth, minDepthFound);
            if (minDepth <= depth) {
                connectionSet.remove(Arrays.asList(node, neighbor));
                connectionSet.remove(Arrays.asList(neighbor, node));
            }
        }
        return minDepthFound;
    }
}
```