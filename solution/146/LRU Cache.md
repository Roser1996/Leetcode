## Solution
### Java
**解题思路**
<br/>
1. 定义一个双向链表存储键值对信息
2. 每次访问到一个结点的时候，将结点插入到表头
3. 当链表的size超过capacity的时候，将链表末尾的结点删除
4. 注意用一个HashMap存储key与结点的对应关系

```java
class LRUCache {
    class DLinkedNode {
        int key;
        int value;
        DLinkedNode pre;
        DLinkedNode next;
    }
    
    private void addNode(DLinkedNode node) {
        node.next = head.next;
        node.pre = head;
        head.next.pre = node;
        head.next = node;
    }
    
    private void deleteNode(DLinkedNode node) {
        DLinkedNode pre = node.pre;
        DLinkedNode next = node.next;
        pre.next = next;
        next.pre = pre;
    }
    
    private void moveToHead(DLinkedNode node) {
        deleteNode(node);
        addNode(node);
    }
    
    private DLinkedNode popTail() {
        DLinkedNode res = tail.pre;
        deleteNode(res);
        return res;
    }
    
    private HashMap<Integer, DLinkedNode> map = new HashMap<>();
    private DLinkedNode head, tail;
    private int size;
    private int capacity;

    public LRUCache(int capacity) {
        this.size = 0;
        this.capacity = capacity;
        this.head = new DLinkedNode();
        this.tail = new DLinkedNode();
        head.next = tail;
        tail.pre = head;
    }
    
    public int get(int key) {
        DLinkedNode node = map.get(key);
        if (node == null) return -1;
        
        moveToHead(node);
        return node.value;
    }
    
    public void put(int key, int value) {
        DLinkedNode node = map.get(key);
        
        if (node == null) {
            DLinkedNode newNode = new DLinkedNode();
            newNode.key = key;
            newNode.value = value;
            
            map.put(key, newNode);
            addNode(newNode);
            size++;
            
            if (size > capacity) {
                DLinkedNode tailNode = popTail();
                map.remove(tailNode.key);
                size--;
            }
        } else {
            node.value = value;
            moveToHead(node);
        }
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```