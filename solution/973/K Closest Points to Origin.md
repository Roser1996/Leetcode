## Solution
### Java
```java
// Solution one: priority queue
class Solution {
    public int[][] kClosest(int[][] points, int K) {
        int[][] res = new int[K][];
        PriorityQueue<int[]> pq = new PriorityQueue<>(new Comparator<int[]>() {
           @Override
            public int compare(int[] a, int[] b) {
                return b[0]*b[0] + b[1]*b[1] - a[0]*a[0] - a[1]*a[1];
            }
        });
        for (int[] point : points) {
            pq.offer(point);
            if (pq.size() > K) {
                pq.poll();
            }
        }
        for (int i = 0; i < K; i++) {
            int[] cur = pq.poll();
            res[i] = cur;
        }
        return res;
    }
}

// Solution two: quick select
class Solution {
    public int[][] kClosest(int[][] points, int K) {
        int left = 0, right = points.length - 1;
        while (left < right) {
            int mid = helper(points, left, right);
            if (mid == K) {
                break;
            }
            else if (mid < K) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return Arrays.copyOfRange(points, 0, K);
    }
    
    private int helper(int[][] points, int l, int r) {
        int[] pivot = points[l];
        while (l < r) {
            while (l < r && compare(points[r], pivot) >= 0) r--;
            points[l] = points[r];
            while (l < r && compare(points[l], pivot) <= 0) l++;
            points[r] = points[l];
        }
        points[l] = pivot;
        return l;
    }
    
    private int compare(int[] a, int[] b) {
        return a[0] * a[0] + a[1] * a[1] - b[0] * b[0] - b[1] * b[1];
    }
}
```