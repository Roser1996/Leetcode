## Solution
### Java
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