# 哈希表和双指针

四数相加II

```cpp
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, 
                     vector<int>& nums3, vector<int>& nums4) {
        unordered_map<int, int> umap;

        // 统计 nums1 和 nums2 所有组合的和及其出现次数
        for (int a : nums1) {
            for (int b : nums2) {
                umap[a + b]++;
            }
        }

        int count = 0;

        // 查找 nums3 和 nums4 的组合和的相反数是否在哈希表中
        for (int c : nums3) {
            for (int d : nums4) {
                int target = -(c + d);
                if (umap.find(target) != umap.end()) {
                    count += umap[target];
                }
            }
        }

        return count;
    }
};
```

---

### 🧠 补充理解
这个算法的核心思想是：
- 将四数之和问题拆成两部分：前两个数组的和 + 后两个数组的和。
- 用哈希表记录前两个数组的所有可能和及其出现次数。
- 遍历后两个数组，查找是否存在相反数，从而使四数之和为 0。

LeetCode 第 15 题“三数之和”
```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        sort(nums.begin(), nums.end());  // 排序是关键

        int n = nums.size();
        for (int i = 0; i < n - 2; ++i) {
            // 跳过重复的起始元素
            if (i > 0 && nums[i] == nums[i - 1]) continue;

            int left = i + 1;
            int right = n - 1;

            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];

                if (sum == 0) {
                    res.push_back({nums[i], nums[left], nums[right]});

                    // 跳过重复的 left 和 right
                    while (left < right && nums[left] == nums[left + 1]) ++left;
                    while (left < right && nums[right] == nums[right - 1]) --right;

                    ++left;
                    --right;
                } else if (sum < 0) {
                    ++left;  // 需要更大的数
                } else {
                    --right; // 需要更小的数
                }
            }
        }

        return res;
    }
};

```




