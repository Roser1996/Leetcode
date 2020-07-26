## Solution
### Java
```java
class Solution {
    public List<Integer> partitionLabels(String S) {
        if (S == null || S.length() == 0) {
            return new ArrayList<Integer>();
        }
        List<Integer> res = new ArrayList<Integer>();
        int[] map = new int[26];
        
        for (int i = 0; i < S.length(); i++) {
            map[S.charAt(i) - 'a'] = i; 
        }
        
        int first = 0;
        int last = 0;
        for (int i = 0; i < S.length(); i++) {
            last = Math.max(last, map[S.charAt(i) - 'a']);
            if (last == i) {
                res.add(last - first + 1);
                first = last + 1;
            }
        }
        return res;
    }
}
```