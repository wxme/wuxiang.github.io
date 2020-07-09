# HashMap
> 基于哈希表的实现的Map接口。 此实现提供了所有可选的map操作，并允许null的值和null键。

### 继承体系
![HashMap](../../../images/hashMap.png "HashMap")
- 实现Serializable接口,可序列化
- 实现Clone接口,可克隆
- 实现Map接口,具有基本Map的crud操作

### 详细属性

#### 属性
```java
    // ----------------------常量
    // 初始化默认容量16
    static final int DEFAULT_INITIAL_CAPACITY = 1 << 4;
    // 最大容量
    static final int MAXIMUM_CAPACITY = 1 << 30;
    // 默认负载因子
    static final float DEFAULT_LOAD_FACTOR = 0.75f;
    // 树化阈值
    static final int TREEIFY_THRESHOLD = 8;
    // 拆分树化阈值
    static final int UNTREEIFY_THRESHOLD = 6;
    // 最小树容量
    static final int MIN_TREEIFY_CAPACITY = 64;
    // ----------------------属性
    // 桶
    transient Node<K,V>[] table;
    // 保持缓存的集合
    transient Set<Map.Entry<K,V>> entrySet;
    // 桶中包含的键值对映射数
    transient int size;
    // 操作数,用于fail-fast机制
    transient int modCount;
    // 扩容/缩减的阈值 = 容量 * 负载因子
    int threshold;
    // 负载因子
    final float loadFactor;
    // Node结构
    static class Node<K,V> implements Map.Entry<K,V> {
        final int hash;
        final K key;
        V value;
        Node<K,V> next;
    }
```

#### 构造方法

1. `HashMap()`  
构建一个空HashMap,设置负载因子为默认负载因子
```java
    public HashMap() {
        this.loadFactor = DEFAULT_LOAD_FACTOR;
    }
```

2. `HashMap(int initialCapacity)`  
构建一个空HashMap,传入默认容量,负载因子使用默认负载因子
```java
    public HashMap(int initialCapacity) {
        this(initialCapacity, DEFAULT_LOAD_FACTOR);
    }
```

3. `HashMap(int initialCapacity, float loadFactor)`
构建一个空HashMap,传入默认容量和负载因子
```java
    public HashMap(int initialCapacity, float loadFactor) {
        // 检查值
        if (initialCapacity < 0)
            throw new IllegalArgumentException("Illegal initial capacity: " +
                                               initialCapacity);
        if (initialCapacity > MAXIMUM_CAPACITY)
            initialCapacity = MAXIMUM_CAPACITY;
        if (loadFactor <= 0 || Float.isNaN(loadFactor))
            throw new IllegalArgumentException("Illegal load factor: " + loadFactor);
        // 赋值和计算与传入默认容量最接近的二进制数
        this.loadFactor = loadFactor;
        this.threshold = tableSizeFor(initialCapacity);
    }
    // 计算最接近的二进制数,例如cap = 5
    static final int tableSizeFor(int cap) {
        int n = cap - 1;  // n = 4: 0000 0000 0000 0100 
        n |= n >>> 1;     // n = 6: 0000 0000 0000 0110
        n |= n >>> 2;     // n = 7: 0000 0000 0000 0111
        n |= n >>> 4;     // n = 7: 0000 0000 0000 0111
        n |= n >>> 8;     // n = 7: 0000 0000 0000 0111
        n |= n >>> 16;    // n = 7: 0000 0000 0000 0111 -> return 8;
        return (n < 0) ? 1 : (n >= MAXIMUM_CAPACITY) ? MAXIMUM_CAPACITY : n + 1;
    }
```

4. `HashMap(Map<? extends K, ? extends V> m)`  
构建一个空HashMap,并指定填充Map中的元素
```java
    public HashMap(Map<? extends K, ? extends V> m) {
        this.loadFactor = DEFAULT_LOAD_FACTOR;
        putMapEntries(m, false);
    }
```

#### 新增

1. `put(K key, V value)`  
插入指定键值对
```java
    public V put(K key, V value) {
        return putVal(hash(key), key, value, false, true);
    }
```

2. `putAll(Map<? extends K, ? extends V> m)`  
插入制定Map中的键值对
```java
    public void putAll(Map<? extends K, ? extends V> m) {
        putMapEntries(m, true);
    }
```

3. `putIfAbsent(K key, V value)`  
如果不存在key就插入并返回null,存在key则不插入并返回key已关联的value
```java
    public V putIfAbsent(K key, V value) {
        return putVal(hash(key), key, value, true, true);
    }
```
**explain**  
```java
    final V putVal(int hash, K key, V value, boolean onlyIfAbsent, boolean evict) {
        // 桶
        Node<K,V>[] tab; 
        // 桶元素
        Node<K,V> p; 
        // 桶长度和桶下标
        int n, i;
        // 如果桶为空则重新计算桶
        if ((tab = table) == null || (n = tab.length) == 0)
            n = (tab = resize()).length;
        // 如果桶中计算下标位置没有元素,则直接插入元素
        if ((p = tab[i = (n - 1) & hash]) == null)
            tab[i] = newNode(hash, key, value, null);
        else {
            Node<K,V> e;
            K k;
            // 通过hash和key判断该元素是否在桶数组中(非链表或树)
            if (p.hash == hash &&
                ((k = p.key) == key || (key != null && key.equals(k))))
                e = p;
            // 判断树节点
            else if (p instanceof TreeNode)
                e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
            // 链表节点
            else {
                // 遍历链表,binCount为记录链表节点数,用于判断树化
                for (int binCount = 0; ; ++binCount) {
                    if ((e = p.next) == null) {
                        // 将节点插入链表尾节点后
                        p.next = newNode(hash, key, value, null);
                        // 达到树化阈值,链表树化
                        if (binCount >= TREEIFY_THRESHOLD - 1)
                            treeifyBin(tab, hash);
                        break;
                    }
                    // 判断是否是相同节点
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        break;
                    p = e;
                }
            }
            // 处理已存在key
            if (e != null) {
                V oldValue = e.value;
                // 覆盖value
                if (!onlyIfAbsent || oldValue == null)
                    e.value = value;
                // 节点访问后的操作,HashMap未实现,猜测是为了操作完整性添加在此,其实现可见LinkedHashMap
                afterNodeAccess(e);
                // 返回旧值
                return oldValue;
            }
        }
        ++modCount;
        // 更新size和扩容
        if (++size > threshold)
            resize();
        // 节点操作后的操作同afterNodeAccess()
        afterNodeInsertion(evict);
        return null;
    }
```
```java
    final void putMapEntries(Map<? extends K, ? extends V> m, boolean evict) {
        // map长度
        int s = m.size();
        if (s > 0) {
            if (table == null) {
                // 计算容量
                float ft = ((float)s / loadFactor) + 1.0F;
                int t = ((ft < (float)MAXIMUM_CAPACITY) ?
                         (int)ft : MAXIMUM_CAPACITY);
                // 重新计算扩容阈值
                if (t > threshold)
                    threshold = tableSizeFor(t);
            }
            else if (s > threshold)
                // 扩容
                resize();
            // 遍历装配元素
            for (Map.Entry<? extends K, ? extends V> e : m.entrySet()) {
                K key = e.getKey();
                V value = e.getValue();
                putVal(hash(key), key, value, false, evict);
            }
        }
    }
```
```java
    final void treeifyBin(Node<K,V>[] tab, int hash) {
        int n, index; Node<K,V> e;
        // 计算扩容
        if (tab == null || (n = tab.length) < MIN_TREEIFY_CAPACITY)
            resize();
        // 
        else if ((e = tab[index = (n - 1) & hash]) != null) {
            // 头节点和尾节点
            TreeNode<K,V> hd = null, tl = null;
            // 遍历链表,将链表中的节点替换成树节点
            do {
                TreeNode<K,V> p = replacementTreeNode(e, null);
                if (tl == null)
                    hd = p;
                else {
                    p.prev = tl;
                    tl.next = p;
                }
                tl = p;
            } while ((e = e.next) != null);
            if ((tab[index] = hd) != null)
                hd.treeify(tab);
        }
    }

    // 构造树节点
    TreeNode<K,V> replacementTreeNode(Node<K,V> p, Node<K,V> next) {
        return new TreeNode<>(p.hash, p.key, p.value, next);
    }

    // 树化
    final void treeify(Node<K,V>[] tab) {
            // 遍历链表进行树化
            TreeNode<K,V> root = null;
            for (TreeNode<K,V> x = this, next; x != null; x = next) {
                // 下一节点,左子节点,右子节点
                next = (TreeNode<K,V>)x.next;
                x.left = x.right = null;
                // 设置根节点
                if (root == null) {
                    x.parent = null;
                    x.red = false;
                    root = x;
                }
                else {
                    // 红黑树化
                    K k = x.key;
                    int h = x.hash;
                    Class<?> kc = null;
                    for (TreeNode<K,V> p = root;;) {
                        int dir, ph;
                        K pk = p.key;
                        // 将新节点与树节点hash比较
                        if ((ph = p.hash) > h)
                            dir = -1;
                        else if (ph < h)
                            dir = 1;
                        else if ((kc == null &&
                                  (kc = comparableClassFor(k)) == null) ||
                                 (dir = compareComparables(kc, k, pk)) == 0)
                            dir = tieBreakOrder(k, pk);

                        TreeNode<K,V> xp = p;
                        // 将节点放在左/右节点
                        if ((p = (dir <= 0) ? p.left : p.right) == null) {
                            x.parent = xp;
                            if (dir <= 0)
                                xp.left = x;
                            else
                                xp.right = x;
                            // 红黑平衡
                            root = balanceInsertion(root, x);
                            break;
                        }
                    }
                }
            }
            moveRootToFront(tab, root);
        }
```
> 红黑树性质:
> 性质1：每个节点要么是黑色，要么是红色。  
> 性质2：根节点是黑色。  
> 性质3：每个叶子节点（NIL）是黑色。  
> 性质4：每个红色结点的两个子结点一定都是黑色。  
> 性质5：任意一结点到每个叶子结点的路径都包含数量相同的黑结点 
```java
    // 红黑树自平衡插入
    static <K,V> TreeNode<K,V> balanceInsertion(TreeNode<K,V> root, TreeNode<K,V> x) {
        // 红节点
        x.red = true;
        for (TreeNode<K,V> xp, xpp, xppl, xppr;;) {
            // 该节点是根节点直接返回
            if ((xp = x.parent) == null) {
                x.red = false;
                return x;
            }
            // 父节点是黑色或者父节点是根节点(红黑树的性质之一是根节点是黑色)
            else if (!xp.red || (xpp = xp.parent) == null)
                return root;
            if (xp == (xppl = xpp.left)) {
                // 父节点是左孩子,且和其兄弟节点均为红色节点
                // 根据性质4,将父节点xp变为黑色
                // 再根据性质5,将父父节点xpp变为红色
                // 再根据性质4,将父父节点的右叶子变为黑色
                if ((xppr = xpp.right) != null && xppr.red) {
                    xppr.red = false;
                    xp.red = false;
                    xpp.red = true;
                    x = xpp;
                }
                else {
                    // 父节点的兄弟节点为nill
                    // 如果节点是右孩子进行左旋
                    if (x == xp.right) {
                        root = rotateLeft(root, x = xp);
                        xpp = (xp = x.parent) == null ? null : xp.parent;
                    }
                    if (xp != null) {
                        xp.red = false;
                        if (xpp != null) {
                            xpp.red = true;
                            root = rotateRight(root, xpp);
                        }
                    }
                }
            }
            else {
                if (xppl != null && xppl.red) {
                    xppl.red = false;
                    xp.red = false;
                    xpp.red = true;
                    x = xpp;
                }
                else {
                    if (x == xp.left) {
                        root = rotateRight(root, x = xp);
                        xpp = (xp = x.parent) == null ? null : xp.parent;
                    }
                    if (xp != null) {
                        xp.red = false;
                        if (xpp != null) {
                            xpp.red = true;
                            root = rotateLeft(root, xpp);
                        }
                    }
                }
            }
        }
    }
```
```java
    // 左旋
    static <K,V> TreeNode<K,V> rotateLeft(TreeNode<K,V> root, TreeNode<K,V> p) {    
            // 右叶子,p的父节点,右叶子的左叶子节点
            TreeNode<K,V> r, pp, rl;
            // 如果节点不为null且含非空右叶子
            if (p != null && (r = p.right) != null) {
                if ((rl = p.right = r.left) != null)
                    rl.parent = p;
                if ((pp = r.parent = p.parent) == null)
                    (root = r).red = false;
                else if (pp.left == p)
                    pp.left = r;
                else
                    pp.right = r;
                r.left = p;
                p.parent = r;
            }
            return root;
        }
        // 右旋
        static <K,V> TreeNode<K,V> rotateRight(TreeNode<K,V> root,
                                               TreeNode<K,V> p) {
            TreeNode<K,V> l, pp, lr;
            if (p != null && (l = p.left) != null) {
                if ((lr = p.left = l.right) != null)
                    lr.parent = p;
                if ((pp = l.parent = p.parent) == null)
                    (root = l).red = false;
                else if (pp.right == p)
                    pp.right = l;
                else
                    pp.left = l;
                l.right = p;
                p.parent = l;
            }
            return root;
        }
```
```java
    // 初始化桶或者调整桶大小
    final Node<K,V>[] resize() {
        // 旧桶
        Node<K,V>[] oldTab = table;
        // 旧容量
        int oldCap = (oldTab == null) ? 0 : oldTab.length;
        // 旧阈值
        int oldThr = threshold;
        // 新容量和新阈值
        int newCap, newThr = 0;
        if (oldCap > 0) {
            // 桶容量达到最大值就设置阈值为最大int值2^31-1
            if (oldCap >= MAXIMUM_CAPACITY) {
                threshold = Integer.MAX_VALUE;
                return oldTab;
            }
            // 扩容为两倍,满足条件下新阈值为两倍
            else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
                     oldCap >= DEFAULT_INITIAL_CAPACITY)
                newThr = oldThr << 1; // double threshold
        }
        // 旧容量<=0,初始容量设为旧阈值
        else if (oldThr > 0)
            newCap = oldThr;
        // 旧容量和旧阈值都为0,则将新容量和阈值都设为默认值
        else {
            newCap = DEFAULT_INITIAL_CAPACITY;
            newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
        }
        // 计算新阈值:新容量 * 负载因子
        if (newThr == 0) {
            float ft = (float)newCap * loadFactor;
            newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ?
                      (int)ft : Integer.MAX_VALUE);
        }
        // 设置阈值
        threshold = newThr;
        // 设置新桶并将旧桶中的元素重新装配
        Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];
        table = newTab;
        if (oldTab != null) {
            // 遍历桶
            for (int j = 0; j < oldCap; ++j) {
                Node<K,V> e;
                if ((e = oldTab[j]) != null) {
                    // 置空桶位置
                    oldTab[j] = null;
                    // 直接设置桶元素
                    if (e.next == null)
                        newTab[e.hash & (newCap - 1)] = e;
                    // 树操作
                    else if (e instanceof TreeNode)
                        ((TreeNode<K,V>)e).split(this, newTab, j, oldCap);
                    // 链表操作,保持顺序,用高位和低位两个节点,高位节点插入桶位置需要加上旧容量大小,低位不用
                    // hash:6 -> 0000 0000 0000 0110 -> hash * (cap - 1)    -> hash & cap
                    // old:8  -> 0000 0000 0000 1000 -> 0000 0000 0000 0110(6) -> ... 0000
                    // new:16 -> 0000 0000 0001 0000 -> 0000 0000 0000 0110(6) -> ... 0000
                    // hash:14-> 0000 0000 0000 1110
                    // old:8  -> 0000 0000 0000 1000 -> 0000 0000 0000 0110(6) -> ... 1000
                    // new:16 -> 0000 0000 0001 0000 -> 0000 0000 0000 1110(14) -> ... 0000
                    else {
                        Node<K,V> loHead = null, loTail = null;
                        Node<K,V> hiHead = null, hiTail = null;
                        Node<K,V> next;
                        do {
                            next = e.next;
                            if ((e.hash & oldCap) == 0) {
                                if (loTail == null)
                                    loHead = e;
                                else
                                    loTail.next = e;
                                loTail = e;
                            }
                            else {
                                if (hiTail == null)
                                    hiHead = e;
                                else
                                    hiTail.next = e;
                                hiTail = e;
                            }
                        } while ((e = next) != null);
                        if (loTail != null) {
                            loTail.next = null;
                            newTab[j] = loHead;
                        }
                        if (hiTail != null) {
                            hiTail.next = null;
                            newTab[j + oldCap] = hiHead;
                        }
                    }
                }
            }
        }
        return newTab;
    }
```
```java
    final void split(HashMap<K,V> map, Node<K,V>[] tab, int index, int bit) {
        // 处理高低位和保持元素顺序
        TreeNode<K,V> b = this;
        TreeNode<K,V> loHead = null, loTail = null;
        TreeNode<K,V> hiHead = null, hiTail = null;
        int lc = 0, hc = 0;
        for (TreeNode<K,V> e = b, next; e != null; e = next) {
            next = (TreeNode<K,V>)e.next;
            e.next = null;
            if ((e.hash & bit) == 0) {
                if ((e.prev = loTail) == null)
                    loHead = e;
                else
                    loTail.next = e;
                loTail = e;
                ++lc;
            }
            else {
                if ((e.prev = hiTail) == null)
                    hiHead = e;
                else
                    hiTail.next = e;
                hiTail = e;
                ++hc;
            }
        }

        if (loHead != null) {
            if (lc <= UNTREEIFY_THRESHOLD)
                tab[index] = loHead.untreeify(map);
            else {
                tab[index] = loHead;
                if (hiHead != null) // (else is already treeified)
                    loHead.treeify(tab);
            }
        }
        if (hiHead != null) {
            if (hc <= UNTREEIFY_THRESHOLD)
                tab[index + bit] = hiHead.untreeify(map);
            else {
                tab[index + bit] = hiHead;
                if (loHead != null)
                    hiHead.treeify(tab);
            }
        }
    }
```

#### 查询

1. `get(Object key)`  
获取指定key的value,key不存在返回null
```java
    public V get(Object key) {
        Node<K,V> e;
        return (e = getNode(hash(key), key)) == null ? null : e.value;
    }
```

2. `getOrDefault(Object key, V defaultValue)`  
获取指定key的value,如果key不存在就返回默认值defaultValue
```java
    public V getOrDefault(Object key, V defaultValue) {
        Node<K,V> e;
        return (e = getNode(hash(key), key)) == null ? defaultValue : e.value;
    }
```

**explain**  
```java
    final Node<K,V> getNode(int hash, Object key) {
        Node<K,V>[] tab; 
        Node<K,V> first, e; 
        int n; 
        K k;
        if ((tab = table) != null && (n = tab.length) > 0 &&
            (first = tab[(n - 1) & hash]) != null) {
            // 先判断该位置第一个元素
            if (first.hash == hash && ((k = first.key) == key || (key != null && key.equals(k))))
                return first;
            // 从链表和树中查询
            if ((e = first.next) != null) {
                // 遍历树
                if (first instanceof TreeNode)
                    return ((TreeNode<K,V>)first).getTreeNode(hash, key);
                do {
                // 遍历链表
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        return e;
                } while ((e = e.next) != null);
            }
        }
        return null;
    }
```

```java
    final TreeNode<K,V> getTreeNode(int h, Object k) {
        return ((parent != null) ? root() : this).find(h, k, null);
    }
    // 返回树的根节点
    final TreeNode<K,V> root() {
        for (TreeNode<K,V> r = this, p;;) {
            // 从该节点向上遍历,没有父节点的节点就是树根节点
            if ((p = r.parent) == null)
                return r;
            r = p;
        }
    }
    // 返回对应hash和key的节点
    final TreeNode<K,V> find(int h, Object k, Class<?> kc) {
        // 基于红黑树,左子节点的hash值小于根节点小于右子节点
        TreeNode<K,V> p = this;
        do {
            int ph, dir; K pk;
            TreeNode<K,V> pl = p.left, pr = p.right, q;
            // 将hash与根节点hash比较,小于就左移,大于就右移,等于就判断key是否为相等
            if ((ph = p.hash) > h)
                p = pl;
            else if (ph < h)
                p = pr;
            else if ((pk = p.key) == k || (k != null && k.equals(pk)))
                return p;
            else if (pl == null)
                p = pr;
            else if (pr == null)
                p = pl;
            else if ((kc != null ||
                        (kc = comparableClassFor(k)) != null) &&
                        (dir = compareComparables(kc, k, pk)) != 0)
                p = (dir < 0) ? pl : pr;
            else if ((q = pr.find(h, k, kc)) != null)
                return q;
            else
                p = pl;
        } while (p != null);
        return null;
    }
```

#### 修改

1. `replace(K key, V value)`  
只有当key存在时才会替换并返回旧值,否则不会替换
```java
    public V replace(K key, V value) {
       Node<K,V> e;
       // 先获取key的节点,然后设置节点的值
       if ((e = getNode(hash(key), key)) != null) {
           V oldValue = e.value;
           e.value = value;
           afterNodeAccess(e);
           return oldValue;
       }
       return null;
    }
```

2. `replace(K key, V oldValue, V newValue)`
只有当key存在且对应value为指定值oldValue时才会将其替换成新值,成功返回true
```java
    public boolean replace(K key, V oldValue, V newValue) {
        Node<K,V> e; V v;
        if ((e = getNode(hash(key), key)) != null &&
            ((v = e.value) == oldValue || (v != null && v.equals(oldValue)))) {
            e.value = newValue;
            afterNodeAccess(e);
            return true;
        }
        return false;
    }
```

3. `replaceAll(BiFunction<? super K, ? super V, ? extends V> function)`  
将Map中的每个键值对进行操作后替换
```java
    public void replaceAll(BiFunction<? super K, ? super V, ? extends V> function) {
        Node<K,V>[] tab;
        if (function == null)
            throw new NullPointerException();
        if (size > 0 && (tab = table) != null) {
            int mc = modCount;
            // 遍历使用apply()处理
            for (int i = 0; i < tab.length; ++i) {
                // 遍历链表
                for (Node<K,V> e = tab[i]; e != null; e = e.next) {
                    // 替换value
                    e.value = function.apply(e.key, e.value);
                }
            }
            // fail-fast
            if (modCount != mc)
                throw new ConcurrentModificationException();
        }
    }
```

#### 删除

1. `remove(Object key)`  
删除指定key
```java
    public V remove(Object key) {
        Node<K,V> e;
        return (e = removeNode(hash(key), key, null, false, true)) == null ?
            null : e.value;
    }
```

2. `remove(Object key, Object value)`
删除指定key和指定value,否则删除失败
```java
    public boolean remove(Object key, Object value) {
        return removeNode(hash(key), key, value, true, true) != null;
    }
```

**explain**  
```java
    final Node<K,V> removeNode(int hash, Object key, Object value,
                               boolean matchValue, boolean movable) {
        Node<K,V>[] tab; 
        Node<K,V> p; 
        int n, index;
        if ((tab = table) != null && (n = tab.length) > 0 &&
            (p = tab[index = (n - 1) & hash]) != null) {
            Node<K,V> node = null, e; K k; V v;
            // 遍历桶元素符合条件就删除
            if (p.hash == hash &&
                ((k = p.key) == key || (key != null && key.equals(k))))
                node = p;
            else if ((e = p.next) != null) {
                // 遍历树
                if (p instanceof TreeNode)
                    node = ((TreeNode<K,V>)p).getTreeNode(hash, key);
                // 遍历链表
                else {
                    do {
                        if (e.hash == hash &&
                            ((k = e.key) == key ||
                             (key != null && key.equals(k)))) {
                            node = e;
                            break;
                        }
                        p = e;
                    } while ((e = e.next) != null);
                }
            }
            if (node != null && (!matchValue || (v = node.value) == value ||
                                 (value != null && value.equals(v)))) {
                // 删除树节点
                if (node instanceof TreeNode)
                    ((TreeNode<K,V>)node).removeTreeNode(this, tab, movable);
                // 删除桶上节点
                else if (node == p)
                    tab[index] = node.next;
                // 删除链表节点
                else
                    p.next = node.next;
                ++modCount;
                // 更新size
                --size;
                // 删除操作后事件
                afterNodeRemoval(node);
                return node;
            }
        }
        return null;
    }
```

