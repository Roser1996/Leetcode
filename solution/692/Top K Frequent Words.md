## Solution
### Java
```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        HashMap<String, Integer> map = new HashMap<>();
        for (String word : words) {
            map.put(word, map.getOrDefault(word, 0) + 1);
        }
        PriorityQueue<Map.Entry<String, Integer>> pq = new PriorityQueue<Map.Entry<String, Integer>> (new Comparator<Map.Entry<String, Integer>>() {
           @Override
            public int compare(Map.Entry<String, Integer> a, Map.Entry<String, Integer> b) {
                int comp = a.getValue() - b.getValue();
                return comp == 0 ? b.getKey().compareTo(a.getKey()) : comp;
            }
        });
        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            pq.offer(entry);
            if (pq.size() > k) pq.poll();
        }
        List<String> res = new ArrayList<>();
        for (int i = 0; i < k; i++) {
            res.add(0, pq.poll().getKey());
        }
        return res;
    }
}
```