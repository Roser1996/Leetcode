## Solution
### Java
```java
class Solution {
    public int[] prisonAfterNDays(int[] cells, int N) {
        if (cells == null || cells.length == 0 || N <= 0) {
            return cells;
        }
        boolean hasCycle = false;
        int cycle = 0;
        HashSet<String> set = new HashSet<>();
        for (int i = 0; i < N; i++) {
            int[] next = nextDay(cells);
            String key = Arrays.toString(next);
            if (!set.contains(key)) {
                set.add(key);
                cycle++;
            } else {
                hasCycle = true;
                break;
            }
            cells = next;
        }
        if (hasCycle) {
            for (int i = 0; i < N%cycle; i++) {
                cells = nextDay(cells);
            }
        }
        return cells;
    }
    
    private int[] nextDay(int[] cells) {
        int[] res = new int[cells.length];
        for (int i = 1; i < res.length - 1; i++) {
            res[i] = cells[i - 1] == cells[i + 1] ? 1 : 0;
        }
        return res;
    }
}
```