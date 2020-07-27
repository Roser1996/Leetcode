## Solution
### Java
**解题思路**
<br/>
1. 定义两个最小堆（优先队列），一个存储所有数字较大的一半，另一个存储剩下较小的一半
2. small中存储的数字需要取相反数（负数），所以队列的首个元素是原本数字集合的最大值
3. 注意large与small的size在偶数时相等，奇数时large会的size会比small大1

```java
class MedianFinder {

    /** initialize your data structure here. */
    
    PriorityQueue<Long> small;
    PriorityQueue<Long> large;
        
    public MedianFinder() {
        small = new PriorityQueue<>();
        large = new PriorityQueue<>();
    }
    
    public void addNum(int num) {
        large.add((long)num);
        small.add(-large.poll());
        if (large.size() < small.size()) {
            large.add(-small.poll());
        }
    }
    
    public double findMedian() {
        return large.size() > small.size() ? large.peek() : ((double)large.peek() - (double)small.peek()) / 2;
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```