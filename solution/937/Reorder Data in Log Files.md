## Solution
### Java
```java
class Solution {
    public String[] reorderLogFiles(String[] logs) {
        Arrays.sort(logs, new Comparator<String>() {
            
            @Override
            public int compare(String s1, String s2) {
                int index1 = s1.indexOf(' ') + 1;
                int index2 = s2.indexOf(' ') + 1;
                if (!Character.isDigit(s1.charAt(index1)) && !Character.isDigit(s2.charAt(index2))) {
                    String comp1 = s1.substring(index1, s1.length());
                    String comp2 = s2.substring(index2, s2.length());
                    int res = comp1.compareTo(comp2);
                    if (res == 0) {
                        res = s1.substring(0, index1).compareTo(s2.substring(0, index2));
                    }
                    return res;
                } else if (!Character.isDigit(s1.charAt(index1)) && Character.isDigit(s2.charAt(index2))) {
                    return -1;
                } else if (Character.isDigit(s1.charAt(index1)) && !Character.isDigit(s2.charAt(index2))) {
                    return 1;
                } else {
                    return 0;
                }
            }
        });
        return logs;
    }
}
```