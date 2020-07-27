## Solution
### Java
**解题思路**
<br/>
1. 首先需要将words数组中的string根据长度进行由小到大的排序，每次在words靠后的word只能由前面的word组成
2. 在判断当前word能不能由前面的preWords组成时，需要用到动态规划，具体看代码

```java
class Solution {
    public List<String> findAllConcatenatedWordsInADict(String[] words) {
        List<String> res = new ArrayList<>();
        HashSet<String> preWords = new HashSet<>();
        Arrays.sort(words, new Comparator<String>() {
            @Override
            public int compare(String a, String b) {
                return a.length() - b.length();
            }
        });
        for (int i = 0; i < words.length; i++) {
            if (canForm(words[i], preWords)) {
                res.add(words[i]);
            }
            preWords.add(words[i]);
        }
        return res;
    }
    
    private boolean canForm(String word, HashSet<String> preWords) {
        if (preWords.isEmpty()) {
            return false;
        }
        boolean[] dp = new boolean[word.length() + 1];
        dp[0] = true;
        for (int i = 1; i < dp.length; i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && preWords.contains(word.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[word.length()];
    }
}
```