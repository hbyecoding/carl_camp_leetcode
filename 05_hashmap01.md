
> **代码随想录算法训练营第5天 | 242.有效的字母异位词 & 349.两个数组的交集**

---

# 📘 代码随想录算法训练营第5天  

---


## 📌 什么是哈希表？

哈希表是一种通过 **键值映射** 实现快速查找的数据结构，底层是一个数组 + 哈希函数。

- 类似数组：通过索引访问元素，时间复杂度为 O(1)
- 不同之处：索引由 key 计算得出，支持任意类型的 key（如字符串、对象）

---

## ⚙️ 哈希函数的作用

哈希函数将任意类型的 key 映射为数组索引：

```java
int hash(K key) {
    int h = key.hashCode();        // 获取哈希值
    h = h & 0x7fffffff;            // 清除符号位，确保非负
    return h % table.length;       // 映射到合法索引
}
```

### 💡 为什么不能直接取负号？

- Java 的 `int` 范围是 [-2³¹, 2³¹ - 1]
- `-(-2³¹)` 会溢出，导致不可预期的结果
- 使用位运算 `h & 0x7fffffff` 更安全也更高效

---

## 🚨 哈希冲突不可避免

哈希函数将无限空间映射到有限数组，冲突在所难免。

### 常见解决方案：

| 方法       | 原理说明 |
|------------|----------|
| 拉链法     | 每个数组槽位存一个链表，冲突的键值对挂在链表上 |
| 开放寻址法 | 冲突时向后寻找空位插入（线性探查、二次探查等） |

---

## 📈 扩容与负载因子

- **负载因子** = 元素数量 / 数组容量
- 当负载因子超过阈值（如 0.75），哈希表会自动扩容
- 扩容后需重新计算所有 key 的索引位置

---

## ✅ 总结

- 哈希表操作平均复杂度为 O(1)，但依赖于哈希函数质量和冲突处理方式
- 哈希冲突无法避免，只能优化处理策略
- 位运算是高效处理哈希值的常见技巧
- 标准库如 Java 的 `HashMap` 已做大量优化，源码值得一读！

---


## ✏️ 题目：242. 有效的字母异位词  
[Leetcode 242](https://leetcode.cn/problems/valid-anagram/)

### ✅ 题目描述  
判断两个字符串是否是字母异位词。字母异位词指的是两个字符串包含的字符相同，顺序可以不同。

---

### 🧠 解题思路  
- 使用一个长度为 26 的整型数组 `count` 记录每个字母出现次数。
- 遍历 `s` 时对每个字符 `+1`，遍历 `t` 时对每个字符 `-1`。
- 最后检查 `count` 是否所有元素都为 0。

---

### 💻 Java代码实现

```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) return false;
    int[] count = new int[26];
    for (int i = 0; i < s.length(); i++) {
        count[s.charAt(i) - 'a']++;
        count[t.charAt(i) - 'a']--;
    }
    for (int c : count) {
        if (c != 0) return false;
    }
    return true;
}
```

---

### ⏱️ 时间复杂度  
- 时间复杂度：O(n)  
- 空间复杂度：O(1)（固定长度数组）

---

## ✏️ 题目：349. 两个数组的交集  
[Leetcode 349](https://leetcode.cn/problems/intersection-of-two-arrays/)

### ✅ 题目描述  
给定两个数组，返回它们的交集，结果中不包含重复元素。

---

### 🧠 解题思路  
- 使用 `HashSet` 存储第一个数组的元素。
- 遍历第二个数组，判断是否在 `set1` 中出现，若出现则加入结果集合 `set2`。
- 最后将 `set2` 转换为数组返回。

---

### 💻 Java代码实现

```java
public int[] intersection(int[] nums1, int[] nums2) {
    Set<Integer> set1 = new HashSet<>();
    Set<Integer> result = new HashSet<>();
    for (int num : nums1) set1.add(num);
    for (int num : nums2) {
        if (set1.contains(num)) result.add(num);
    }
    int[] res = new int[result.size()];
    int i = 0;
    for (int num : result) res[i++] = num;
    return res;
}
```

---

### ⏱️ 时间复杂度  
- 时间复杂度：O(n + m)  
- 空间复杂度：O(n)（使用了两个集合）

---
