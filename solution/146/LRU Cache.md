## Solution
### Java
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