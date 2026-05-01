# 🪟 Sliding Window — Revision Notes

> **Pattern:** Maintain a window `[low, high]` that expands right and shrinks left to always stay valid.

---

## 🧠 Core Template

```cpp
int low = 0, ans = 0;

for (int high = 0; high < n; high++) {

    // Step 1: Include arr[high] into the window
    include(arr[high]);

    // Step 2: If window is invalid, shrink from the left
    while (window is invalid) {
        remove(arr[low]);
        low++;
    }

    // Step 3: Update answer with current valid window size
    ans = max(ans, high - low + 1);
}
```

**Key idea:**
- `high` always moves forward (expands window)
- `low` moves forward only when window becomes invalid (shrinks window)
- Answer is always the **maximum valid window size seen**

---

## 📘 Problem 1 — Longest Subarray with Sum ≤ 8

**Array:** `2 3 1 4 2`  
**Goal:** Find the longest subarray whose sum does not exceed 8.

### Approach
- Include `arr[high]` by adding to `sum`
- Window invalid when `sum > 8` → shrink from left
- Track `max(high - low + 1)`

```cpp
int low = 0, sum = 0, ans = 0;

for (int high = 0; high < n; high++) {
    sum += arr[high];           // add new element

    while (sum > 8) {           // window invalid
        sum -= arr[low];
        low++;
    }

    ans = max(ans, high - low + 1);
}
```

### Dry Run

| high | arr[high] | sum | low | Window          | ans |
|------|-----------|-----|-----|-----------------|-----|
| 0    | 2         | 2   | 0   | [2]             | 1   |
| 1    | 3         | 5   | 0   | [2,3]           | 2   |
| 2    | 1         | 6   | 0   | [2,3,1]         | 3   |
| 3    | 4         | 10  | 0   | shrink → [3,1,4]| 3   |
| 4    | 2         | 10  | 2   | shrink → [1,4,2]| 3   |

**Answer: 3**

---

## 📘 Problem 2 — Longest Substring Without Repeating Characters

**LeetCode #3**  
**Input:** `"abcabcbb"` → **Output:** `3` (substring `"abc"`)

### Approach
- Use a **hashmap** to count frequency of each character in the window
- Window invalid when any character has frequency > 1
- Shrink from left until all frequencies ≤ 1

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> mp;
        int low = 0, ans = 0;

        for (int high = 0; high < s.size(); high++) {
            mp[s[high]]++;                      // add character to window

            while (mp[s[high]] > 1) {           // duplicate found → shrink
                mp[s[low]]--;
                low++;
            }

            ans = max(ans, high - low + 1);
        }

        return ans;
    }
};
```

### Dry Run (`"abcabcbb"`)

| high | char | mp              | low | Window  | ans |
|------|------|-----------------|-----|---------|-----|
| 0    | a    | {a:1}           | 0   | "a"     | 1   |
| 1    | b    | {a:1,b:1}       | 0   | "ab"    | 2   |
| 2    | c    | {a:1,b:1,c:1}   | 0   | "abc"   | 3   |
| 3    | a    | a becomes 2 → shrink, low=1 | 1 | "bca" | 3 |
| 4    | b    | b becomes 2 → shrink, low=2 | 2 | "cab" | 3 |
| ...  | ...  | ...             | ... | ...     | 3   |

**Answer: 3**

---

## 📘 Problem 3 — Max Consecutive Ones III (Flip at Most K Zeros)

**LeetCode #1004**  
**Input:** `[1,1,1,0,0,0,1,1,1,1,0]`, `k = 2`  
**Goal:** Flip at most `k` zeros. Find the longest subarray of ones.

### Approach
- Count zeros in the window
- Window invalid when `zeroCount > k` → shrink from left
- When removing `arr[low]`, if it's a `0`, decrement `zeroCount`

```cpp
class Solution {
public:
    int longestOnes(vector<int>& nums, int k) {
        int low = 0, zeroCount = 0, ans = 0;

        for (int high = 0; high < nums.size(); high++) {
            if (nums[high] == 0)
                zeroCount++;                    // new zero included

            while (zeroCount > k) {             // too many zeros → shrink
                if (nums[low] == 0)
                    zeroCount--;
                low++;
            }

            ans = max(ans, high - low + 1);
        }

        return ans;
    }
};
```

### Dry Run (k = 2)

```
Array:  1  1  1  0  0  0  1  1  1  1  0
Index:  0  1  2  3  4  5  6  7  8  9  10
```

- high reaches index 5 → zeroCount = 3 > k → shrink
- low moves to index 3 (removes a 1), then index 4 (removes the 0 at index 3) → zeroCount = 2
- Valid window: `[3..9]` = indices 3 to 9 → length **6**

**Answer: 6**

---

## 📘 Problem 4 — Fruit Into Baskets

**LeetCode #904**  
**Input:** `fruits[]` (each element = fruit type)  
**Goal:** Pick fruits from at most **2 consecutive types**. Find the max fruits you can pick (i.e., longest subarray with at most 2 distinct values).

### Approach
- Use a **hashmap** to count frequency of each fruit type in the window
- Window invalid when `mp.size() > 2` (more than 2 distinct types)
- Shrink from left; remove fruit from map when its count reaches 0

```cpp
class Solution {
public:
    int totalFruit(vector<int>& fruits) {
        unordered_map<int, int> mp;
        int low = 0, ans = 0;

        for (int high = 0; high < fruits.size(); high++) {
            mp[fruits[high]]++;                 // add fruit to basket

            while (mp.size() > 2) {             // more than 2 types → shrink
                mp[fruits[low]]--;
                if (mp[fruits[low]] == 0)
                    mp.erase(fruits[low]);       // remove type from map
                low++;
            }

            ans = max(ans, high - low + 1);
        }

        return ans;
    }
};
```

### Example

```
fruits = [1, 2, 1, 2, 3]
```

| high | fruit | mp              | low | ans |
|------|-------|-----------------|-----|-----|
| 0    | 1     | {1:1}           | 0   | 1   |
| 1    | 2     | {1:1, 2:1}      | 0   | 2   |
| 2    | 1     | {1:2, 2:1}      | 0   | 3   |
| 3    | 2     | {1:2, 2:2}      | 0   | 4   |
| 4    | 3     | size=3 → shrink → remove 1s, low=2 | 2 | 4 |

**Answer: 4** (subarray `[1, 2, 1, 2]`)

---

## 🔁 Pattern Summary

| Problem | Invalid Condition | Data Structure |
|---|---|---|
| Sum ≤ K | `sum > K` | integer variable |
| No repeating chars | `freq[char] > 1` | hashmap |
| At most K zeros | `zeroCount > K` | integer variable |
| At most 2 fruit types | `map.size() > 2` | hashmap |

---

## ⚡ Quick Cheatsheet

```
EXPAND  → always move high forward
SHRINK  → move low forward when window is INVALID
ANSWER  → max(ans, high - low + 1) after every shrink
```

> 💡 **Tip:** The `while` loop for shrinking ensures the window is always valid before updating the answer. Never update `ans` inside the shrink loop.