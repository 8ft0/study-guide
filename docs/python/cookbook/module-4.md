# Problem Solving

Comprehensive examples for each of the key techniques mentioned in the document: Greedy algorithms, Divide and Conquer, Two Pointers, and the use of hashmaps. These examples will focus on applying these techniques to solve common types of problems efficiently.

### 1. Greedy Algorithm Example: Minimum Coins for Change

**Problem Statement**: Given an array of coin denominations and a total amount, find the minimum number of coins needed to make up that amount.

**Python Solution**:
```python
def minCoins(coins, amount):
    coins.sort(reverse=True)
    count = 0
    for coin in coins:
        count += amount // coin
        amount %= coin
        if amount == 0:
            break
    return count if amount == 0 else -1

# Example usage
coins = [1, 5, 10, 25]
amount = 63
print(minCoins(coins, amount))  # Output will depend on the input values
```

### 2. Divide and Conquer Example: Maximum Subarray Sum

**Problem Statement**: Find the maximum sum of a contiguous subarray in an array of integers.

**Python Solution**:
```python
def maxSubArraySum(arr, left, right):
    if left == right:
        return arr[left]
    
    mid = (left + right) // 2
    max_left_sum = maxSubArraySum(arr, left, mid)
    max_right_sum = maxSubArraySum(arr, mid+1, right)
    max_cross_sum = crossSum(arr, left, mid, right)

    return max(max_left_sum, max_right_sum, max_cross_sum)

def crossSum(arr, left, mid, right):
    sum = 0
    left_sum = float('-inf')
    for i in range(mid, left-1, -1):
        sum += arr[i]
        if sum > left_sum:
            left_sum = sum
    
    sum = 0
    right_sum = float('-inf')
    for i in range(mid+1, right+1):
        sum += arr[i]
        if sum > right_sum:
            right_sum = sum

    return left_sum + right_sum

# Example usage
arr = [-2, -5, 6, -2, -3, 1, 5, -6]
print(maxSubArraySum(arr, 0, len(arr) - 1))  # Output: 7
```

### 3. Two Pointers Example: Pair with Target Sum

**Problem Statement**: Given a sorted array and a target sum, find if there is a pair in the array whose sum is equal to the target sum.

**Python Solution**:
```python
def twoPointerSum(arr, target):
    left, right = 0, len(arr) - 1
    while left < right:
        current_sum = arr[left] + arr[right]
        if current_sum == target:
            return (left, right)
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    return None

# Example usage
arr = [1, 2, 4, 5, 7]
target = 9
print(twoPointerSum(arr, target))  # Output: (2, 3)
```

### 4. Using Hashmaps Example: Count Distinct Elements

**Problem Statement**: Count the number of distinct elements in an array.

**Python Solution**:
```python
def countDistinct(arr):
    seen = set()
    for num in arr:
        seen.add(num)
    return len(seen)

# Example usage
arr = [1, 2, 2, 3, 4, 4, 4, 5]
print(countDistinct(arr))  # Output: 5
```


### 5. Subarray Sum Equals K

**Problem Statement:**
Given an array of integers `nums` and an integer `k`, return the total number of continuous subarrays whose sum equals to `k`.

**Example:**
```python
Input: nums = [1,1,1], k = 2
Output: 2
Explanation: The subarrays [1,1] and [1,1] have sum equals to 2.
```

**Solution:**
```python
def subarray_sum(nums, k):
    count = 0
    sum_freq = {0: 1}
    cur_sum = 0
    
    for num in nums:
        cur_sum += num
        complement = cur_sum - k
        if complement in sum_freq:
            count += sum_freq[complement]
        sum_freq[cur_sum] = sum_freq.get(cur_sum, 0) + 1
    
    return count

# Test the solution
nums = [1, 1, 1]
k = 2
print(subarray_sum(nums, k))  # Output: 2
```

This problem can be solved using a hashmap to store the cumulative sums encountered so far. We check if the complement of the current sum (i.e., `cur_sum - k`) exists in the hashmap, indicating the presence of a subarray with sum `k`.

This example demonstrates the application of a hashmap to optimize the solution for finding subarrays with a specific sum.

By practising similar problems and understanding the application of algorithms like greedy, divide and conquer, and two pointers, you can better prepare for the assessment's problem-solving challenges.

---

Certainly! Let's explore another problem-solving example for Module 4:

### 6: Longest Substring Without Repeating Characters

**Problem Statement:**
Given a string `s`, find the length of the longest substring without repeating characters.

**Example:**
```python
Input: s = "abcabcbb"
Output: 3
Explanation: The longest substring without repeating characters is "abc", which has a length of 3.
```

**Solution:**
```python
def longest_substring(s):
    max_length = 0
    start = 0
    char_index = {}  # Store the index of each character
    
    for end, char in enumerate(s):
        if char in char_index and char_index[char] >= start:
            start = char_index[char] + 1
        char_index[char] = end
        max_length = max(max_length, end - start + 1)
    
    return max_length

# Test the solution
s = "abcabcbb"
print(longest_substring(s))  # Output: 3
```

In this problem, we use the two-pointer technique along with a hashmap to efficiently find the longest substring without repeating characters. The `start` pointer indicates the start of the current substring, and we update it when encountering a repeating character. The `char_index` hashmap stores the most recent index of each character encountered.

This example showcases the application of two pointers and a hashmap to optimize the solution for finding the longest substring without repeating characters.


---


### 7: Minimum Window Substring

**Problem Statement:**
Given two strings `s` and `t`, return the minimum window in `s` which contains all the characters in `t`. If there is no such window in `s` that covers all characters in `t`, return an empty string `""`.

**Example:**
```python
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" contains all characters "A", "B", and "C".
```

**Solution:**
```python
from collections import Counter

def min_window(s, t):
    if not s or not t:
        return ""

    target_counts = Counter(t)
    required = len(target_counts)
    left, right = 0, 0
    formed = 0
    window_counts = {}
    ans = float("inf"), None, None

    while right < len(s):
        char = s[right]
        window_counts[char] = window_counts.get(char, 0) + 1
        if char in target_counts and window_counts[char] == target_counts[char]:
            formed += 1
        while formed == required:
            if right - left + 1 < ans[0]:
                ans = right - left + 1, left, right
            char = s[left]
            window_counts[char] -= 1
            if char in target_counts and window_counts[char] < target_counts[char]:
                formed -= 1
            left += 1
        right += 1

    return "" if ans[0] == float("inf") else s[ans[1]: ans[2] + 1]

# Test the solution
s = "ADOBECODEBANC"
t = "ABC"
print(min_window(s, t))  # Output: "BANC"
```

This problem involves finding the minimum window substring in `s` that contains all characters of `t`. We use a sliding window approach where we maintain a window containing the characters of `s` and move the `left` and `right` pointers to adjust the window until we find the minimum window containing all characters of `t`.


---


### 8: Coin Change

**Problem Statement:**
You are given coins of different denominations and a total amount of money `amount`. Write a function to compute the minimum number of coins needed to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

**Example:**
```python
Input: coins = [1, 2, 5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
```

**Solution:**
```python
def coin_change(coins, amount):
    dp = [float("inf")] * (amount + 1)
    dp[0] = 0
    
    for coin in coins:
        for i in range(coin, amount + 1):
            dp[i] = min(dp[i], dp[i - coin] + 1)
    
    return dp[amount] if dp[amount] != float("inf") else -1

# Test the solution
coins = [1, 2, 5]
amount = 11
print(coin_change(coins, amount))  # Output: 3
```

In this problem, we use dynamic programming to find the minimum number of coins needed to make up the given amount. We iterate over each coin denomination and update the minimum number of coins needed for each amount from `1` to `amount`.

By practising problems like these and understanding how to implement appropriate algorithms like dynamic programming, you'll be better prepared to optimize solutions for similar challenges in the assessment.

---

### 9: Container With Most Water

**Problem Statement:**
Given `n` non-negative integers `a1, a2, ..., an`, where each represents a point at coordinate `(i, ai)`. `n` vertical lines are drawn such that the two endpoints of the line `i` are at `(i, ai)` and `(i, 0)`. Find two lines, which, together with the x-axis, form a container such that the container contains the most water.

**Example:**
```python
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The maximum area of water (highlighted in blue) the container can contain is 49, obtained by selecting the heights of 8 and 7 (distance between them is 7).
```

**Solution:**
```python
def max_area(height):
    max_area = 0
    left = 0
    right = len(height) - 1
    
    while left < right:
        width = right - left
        current_area = min(height[left], height[right]) * width
        max_area = max(max_area, current_area)
        
        if height[left] < height[right]:
            left += 1
        else:
            right -= 1
    
    return max_area

# Test the solution
height = [1, 8, 6, 2, 5, 4, 8, 3, 7]
print(max_area(height))  # Output: 49
```

In this problem, we use a two-pointer approach to find the maximum area of water that can be contained by the container formed by the vertical lines. We start with two pointers at the beginning and end of the array and gradually move them towards each other, calculating the area at each step and updating the maximum area found so far.

---

### 10: Longest Palindromic Substring

**Problem Statement:**
Given a string `s`, return the longest palindromic substring in `s`.

**Example:**
```python
Input: s = "babad"
Output: "bab" or "aba"
Explanation: Either "bab" or "aba" is the longest palindromic substring.
```

**Solution:**
```python
def longest_palindrome(s):
    if len(s) < 2:
        return s
    
    start = 0
    max_length = 1
    
    for i in range(len(s)):
        # Check for odd-length palindromes
        left, right = i, i
        while left >= 0 and right < len(s) and s[left] == s[right]:
            if right - left + 1 > max_length:
                start = left
                max_length = right - left + 1
            left -= 1
            right += 1
        
        # Check for even-length palindromes
        left, right = i, i + 1
        while left >= 0 and right < len(s) and s[left] == s[right]:
            if right - left + 1 > max_length:
                start = left
                max_length = right - left + 1
            left -= 1
            right += 1
    
    return s[start:start + max_length]

# Test the solution
s = "babad"
print(longest_palindrome(s))  # Output: "bab" or "aba"
```

In this problem, we use the technique of expanding around the center to find the longest palindromic substring. We iterate over each character in the string and treat it as the center of a potential palindrome, expanding outward to check if the substring formed is a palindrome. We repeat this process for both odd-length and even-length palindromes.

---
Sure! Let's explore another problem-solving example focusing on implementing an appropriate algorithm:

### 11: Merge Intervals

**Problem Statement:**
Given a collection of intervals, merge overlapping intervals.

**Example:**
```python
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: The intervals [1,3] and [2,6] are overlapping, so they are merged into [1,6].
```

**Solution:**
```python
def merge_intervals(intervals):
    if not intervals:
        return []
    
    intervals.sort(key=lambda x: x[0])  # Sort intervals based on the start time
    merged = [intervals[0]]
    
    for interval in intervals[1:]:
        if interval[0] <= merged[-1][1]:  # Overlapping intervals
            merged[-1][1] = max(merged[-1][1], interval[1])
        else:
            merged.append(interval)
    
    return merged

# Test the solution
intervals = [[1, 3], [2, 6], [8, 10], [15, 18]]
print(merge_intervals(intervals))  # Output: [[1,6],[8,10],[15,18]]
```

In this problem, we first sort the intervals based on their start times. Then, we iterate through the sorted intervals and merge overlapping intervals as necessary. If an interval overlaps with the last interval in the merged list, we update the end time of the last interval accordingly. Otherwise, we add the interval to the merged list.

---

Certainly! Let's explore another problem-solving example focusing on implementing an appropriate algorithm:

### 12: Three Sum

**Problem Statement:**
Given an array `nums` of n integers, find all unique triplets in the array which gives the sum of zero.

**Example:**
```python
Input: nums = [-1, 0, 1, 2, -1, -4]
Output: [[-1, -1, 2], [-1, 0, 1]]
Explanation: The triplets [-1, -1, 2] and [-1, 0, 1] sum up to zero.
```

**Solution:**
```python
def three_sum(nums):
    nums.sort()
    result = []
    n = len(nums)
    
    for i in range(n - 2):
        if i > 0 and nums[i] == nums[i - 1]:  # Skip duplicates
            continue
        left = i + 1
        right = n - 1
        while left < right:
            total = nums[i] + nums[left] + nums[right]
            if total == 0:
                result.append([nums[i], nums[left], nums[right]])
                while left < right and nums[left] == nums[left + 1]:  # Skip duplicates
                    left += 1
                while left < right and nums[right] == nums[right - 1]:  # Skip duplicates
                    right -= 1
                left += 1
                right -= 1
            elif total < 0:
                left += 1
            else:
                right -= 1
    
    return result

# Test the solution
nums = [-1, 0, 1, 2, -1, -4]
print(three_sum(nums))  # Output: [[-1, -1, 2], [-1, 0, 1]]
```

In this problem, we first sort the array `nums` to facilitate the two-pointer approach. Then, we iterate through the array and use two pointers to find the triplets whose sum is zero. We skip duplicate elements to avoid duplicate triplets in the result.

---

### 13: Word Break

**Problem Statement:**
Given a string `s` and a dictionary of strings `wordDict`, determine if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Example:**
```python
Input: s = "leetcode", wordDict = ["leet", "code"]
Output: True
Explanation: "leetcode" can be segmented into "leet code".
```

**Solution:**
```python
def word_break(s, wordDict):
    word_set = set(wordDict)
    n = len(s)
    dp = [False] * (n + 1)
    dp[0] = True
    
    for i in range(1, n + 1):
        for j in range(i):
            if dp[j] and s[j:i] in word_set:
                dp[i] = True
                break
    
    return dp[n]

# Test the solution
s = "leetcode"
wordDict = ["leet", "code"]
print(word_break(s, wordDict))  # Output: True
```

In this problem, we use dynamic programming to determine if the given string `s` can be segmented into words from the dictionary `wordDict`. We iterate through each position in the string and check if the substring ending at that position can be segmented into words from the dictionary.

By practising problems like these and understanding how to implement appropriate algorithms like dynamic programming for word segmentation, you'll be better prepared to optimize solutions for similar challenges in the assessment.

---

### 14: Top K Frequent Elements

**Problem Statement:**
Given a non-empty array of integers `nums`, return the k most frequent elements.

**Example:**
```python
Input: nums = [1, 1, 1, 2, 2, 3], k = 2
Output: [1, 2]
Explanation: The elements 1 and 2 are the most frequent. 
```

**Solution:**
```python
from collections import Counter
import heapq

def top_k_frequent(nums, k):
    count = Counter(nums)
    heap = [(-freq, num) for num, freq in count.items()]
    heapq.heapify(heap)
    return [heapq.heappop(heap)[1] for _ in range(k)]

# Test the solution
nums = [1, 1, 1, 2, 2, 3]
k = 2
print(top_k_frequent(nums, k))  # Output: [1, 2]
```

In this problem, we use a combination of Counter and heapq to efficiently find the k most frequent elements in the given array `nums`. We first count the frequency of each element using Counter, then create a max heap (using a min heap with negative frequencies) to store the elements based on their frequencies. Finally, we pop k elements from the heap to get the k most frequent elements.

By practising problems like these and understanding how to implement appropriate algorithms like heap-based solutions for finding top-k frequent elements, you'll be better prepared to optimize solutions for similar challenges in the assessment.

---

These examples cover the fundamental techniques you should be familiar with for our assessment. They emphasize problem solving and efficient implementation, which are crucial for performing well in this module.