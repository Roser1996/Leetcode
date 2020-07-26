## Solution
### Java
```java
class Solution {
    public String mostCommonWord(String paragraph, String[] banned) {
        String[] words = paragraph.toLowerCase().split("[^a-z]+");
        HashSet<String> set = new HashSet<>(Arrays.asList(banned));
        HashMap<String, Integer> freq = new HashMap<>();
        for (String word : words) {
            freq.put(word, freq.getOrDefault(word, 0) + 1);
        }
        
        String res = "";
        int maxNum = 0;
        for (Map.Entry<String, Integer> entry : freq.entrySet()) {
            if (!set.contains(entry.getKey()) && maxNum < entry.getValue()) {
                res = entry.getKey();
                maxNum = entry.getValue();
            }
        }
        return res;
    }
}
```