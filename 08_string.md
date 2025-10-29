## 基础

字符串  list 如果用Python 实现的话， 通过 list（）， .split() 和  .join() 可以互通
## 题目

### 反转字符串

```cpp

class Solution {
public:
void reverseString(vector<char>& s) {
    int left = 0, right = s.size() - 1;
    while (left < right) {
        swap(s[left], s[right]);
        left++;
        right--;
    }
}
};
```

```python
from typing import List

def reverse_string(s: List) -> str:
    left, right = 0, len(s) - 1
    # if not list:

    s = list(s)
    while left < right:
        s[left], s[right] = s[right], s[left]
        left += 1
        right -= 1
    return "".join(s)
```

### 反转字符串 II


```python
def reverseStr(s: str, k: int) -> str:
    s = list(s)
    for i in range(0, len(s), 2 * k):
        s[i:i + k] = reversed(s[i:i + k])
    return "".join(s)
```

### 替换数字

给定一个字符串 s，它包含小写字母和数字字符，请编写一个函数，将字符串中的字母字符保持不变，而将每个数字字符替换为number。 例如，对于输入字符串 "a1b2c3"，函数应该将其转换为 "anumberbnumbercnumber"。

```cpp
#include <iostream>
#include <string>
#include <cctype>

using namespace std;

string replaceDigits(const string &s) {
    string out;
    out.reserve(s.size() * 6); // 预分配，"number" 长度为6
    for (unsigned char c : s) {
        if (isdigit(c)) out += "number";
        else out.push_back(c);
    }
    return out;
}

int main() {
    string s = "a1b2c3";
    cout << replaceDigits(s) << '\n'; // 输出: anumberbnumbercnumber
    return 0;
}
```

