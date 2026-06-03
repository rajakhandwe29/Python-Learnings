# Coding Challenges

Practical problem-solving exercises for interview preparation.

## Easy Problems (15 minutes each)

### 1. Two Sum
Find two numbers that add up to target.

```python
def two_sum(nums, target):
    """
    Args:
        nums: List of integers
        target: Target sum
    Returns:
        List of indices of two numbers that sum to target
    """
    seen = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
    return []

# Test cases
assert two_sum([2, 7, 11, 15], 9) == [0, 1]
assert two_sum([3, 2, 4], 6) == [1, 2]
assert two_sum([3, 3], 6) == [0, 1]
```

### 2. Reverse String
Reverse a string in-place (or return reversed).

```python
def reverse_string(s):
    """Reverse a string"""
    return s[::-1]

def reverse_string_iterative(s):
    """Reverse without using slice"""
    result = ""
    for char in s:
        result = char + result
    return result

# Test
assert reverse_string("hello") == "olleh"
assert reverse_string_iterative("world") == "dlrow"
```

### 3. Palindrome Check
Check if string is palindrome.

```python
def is_palindrome(s):
    """Check if string is palindrome (ignore spaces, punctuation, case)"""
    # Filter alphanumeric and convert to lowercase
    cleaned = ''.join(c.lower() for c in s if c.isalnum())
    return cleaned == cleaned[::-1]

# Test
assert is_palindrome("A man, a plan, a canal: Panama") == True
assert is_palindrome("race a car") == False
```

### 4. Contains Duplicates
Check if array has duplicates.

```python
def contains_duplicate(nums):
    """Check if list contains duplicates"""
    return len(nums) != len(set(nums))

# Test
assert contains_duplicate([1, 2, 3, 1]) == True
assert contains_duplicate([1, 2, 3, 4]) == False
```

### 5. Missing Number
Find missing number in array.

```python
def missing_number(nums):
    """Find missing number in range 0 to n"""
    n = len(nums)
    expected_sum = n * (n + 1) // 2
    actual_sum = sum(nums)
    return expected_sum - actual_sum

# Test
assert missing_number([3, 0, 1]) == 2
assert missing_number([0, 1]) == 2
```

---

## Medium Problems (30 minutes each)

### 6. Group Anagrams
Group words that are anagrams of each other.

```python
def group_anagrams(words):
    """Group anagrams together"""
    anagram_groups = {}
    
    for word in words:
        # Sort letters to get key
        key = ''.join(sorted(word))
        if key not in anagram_groups:
            anagram_groups[key] = []
        anagram_groups[key].append(word)
    
    return list(anagram_groups.values())

# Test
result = group_anagrams(["eat", "tea", "ate", "bat", "tab"])
# [["eat", "tea", "ate"], ["bat", "tab"]]
```

### 7. Longest Substring Without Repeating
Find longest substring without repeating characters.

```python
def length_of_longest_substring(s):
    """Find length of longest substring without repeating chars"""
    char_index = {}
    max_length = 0
    start = 0
    
    for end, char in enumerate(s):
        if char in char_index and char_index[char] >= start:
            start = char_index[char] + 1
        
        char_index[char] = end
        max_length = max(max_length, end - start + 1)
    
    return max_length

# Test
assert length_of_longest_substring("abcabcbb") == 3  # "abc"
assert length_of_longest_substring("bbbbb") == 1     # "b"
```

### 8. Valid Parentheses
Check if parentheses are balanced.

```python
def is_valid(s):
    """Check if parentheses are balanced"""
    stack = []
    pairs = {'(': ')', '{': '}', '[': ']'}
    
    for char in s:
        if char in pairs:
            stack.append(char)
        elif char in pairs.values():
            if not stack or pairs[stack.pop()] != char:
                return False
    
    return len(stack) == 0

# Test
assert is_valid("()[]{}") == True
assert is_valid("([{}])") == True
assert is_valid("([)]") == False
```

### 9. Binary Tree Level Order Traversal
Traverse tree level by level.

```python
from collections import deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def level_order(root):
    """Level order traversal of binary tree"""
    if not root:
        return []
    
    result = []
    queue = deque([root])
    
    while queue:
        level_size = len(queue)
        current_level = []
        
        for _ in range(level_size):
            node = queue.popleft()
            current_level.append(node.val)
            
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        
        result.append(current_level)
    
    return result
```

### 10. Merge K Sorted Lists
Merge k sorted linked lists.

```python
from heapq import heappush, heappop

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def merge_k_lists(lists):
    """Merge k sorted lists using heap"""
    min_heap = []
    
    # Add first node from each list
    for i, lst in enumerate(lists):
        if lst:
            heappush(min_heap, (lst.val, i, lst))
    
    dummy = ListNode(0)
    current = dummy
    
    while min_heap:
        val, i, node = heappop(min_heap)
        current.next = node
        current = current.next
        
        if node.next:
            heappush(min_heap, (node.next.val, i, node.next))
    
    return dummy.next
```

---

## Hard Problems (45+ minutes each)

### 11. LRU Cache
Implement LRU (Least Recently Used) Cache.

```python
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity):
        self.cache = OrderedDict()
        self.capacity = capacity
    
    def get(self, key):
        if key not in self.cache:
            return -1
        
        # Move to end (most recent)
        self.cache.move_to_end(key)
        return self.cache[key]
    
    def put(self, key, value):
        if key in self.cache:
            self.cache.move_to_end(key)
        
        self.cache[key] = value
        
        # Remove oldest if over capacity
        if len(self.cache) > self.capacity:
            self.cache.popitem(last=False)

# Test
lru = LRUCache(2)
lru.put(1, 1)
lru.put(2, 2)
assert lru.get(1) == 1
lru.put(3, 3)  # Evicts 2
assert lru.get(2) == -1
```

### 12. Word Ladder
Find shortest path from start to end word.

```python
from collections import deque

def ladder_length(begin_word, end_word, word_list):
    """Find shortest transformation sequence"""
    if end_word not in word_list:
        return 0
    
    word_set = set(word_list)
    queue = deque([(begin_word, 1)])
    
    while queue:
        word, length = queue.popleft()
        
        if word == end_word:
            return length
        
        # Try changing each character
        for i in range(len(word)):
            for c in 'abcdefghijklmnopqrstuvwxyz':
                new_word = word[:i] + c + word[i+1:]
                
                if new_word in word_set:
                    queue.append((new_word, length + 1))
                    word_set.remove(new_word)
    
    return 0
```

### 13. Longest Increasing Subsequence
Find longest increasing subsequence.

```python
def length_of_lis(nums):
    """Find length of longest increasing subsequence"""
    if not nums:
        return 0
    
    n = len(nums)
    dp = [1] * n  # dp[i] = length of LIS ending at i
    
    for i in range(1, n):
        for j in range(i):
            if nums[j] < nums[i]:
                dp[i] = max(dp[i], dp[j] + 1)
    
    return max(dp)

# Test
assert length_of_lis([10, 9, 2, 5, 3, 7, 101, 18]) == 4  # [2, 3, 7, 101]
```

### 14. Word Break
Check if word can be segmented.

```python
def word_break(s, word_dict):
    """Check if string can be segmented into dictionary words"""
    word_set = set(word_dict)
    dp = [False] * (len(s) + 1)
    dp[0] = True
    
    for i in range(1, len(s) + 1):
        for j in range(i):
            if dp[j] and s[j:i] in word_set:
                dp[i] = True
                break
    
    return dp[-1]

# Test
assert word_break("leetcode", ["leet", "code"]) == True
assert word_break("applepenapple", ["apple", "pen"]) == True
```

---

## Data Structure Specific

### 15. Implement Trie
Implement prefix tree.

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True
    
    def search(self, word):
        node = self._find_node(word)
        return node is not None and node.is_end
    
    def starts_with(self, prefix):
        return self._find_node(prefix) is not None
    
    def _find_node(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return None
            node = node.children[char]
        return node
```

---

## Problem-Solving Strategies

### 1. Understand the Problem
- Read carefully
- Clarify constraints
- Ask examples
- Identify edge cases

### 2. Plan Approach
- Brute force first
- Optimize step by step
- Consider data structures
- Analyze complexity

### 3. Implement
- Write clean code
- Handle edge cases
- Test as you go

### 4. Verify
- Test with examples
- Check edge cases
- Verify complexity

---

## Complexity Analysis Guide

| Time Complexity | Operations | Example |
|---|---|---|
| O(1) | Constant | Array access, hash lookup |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Loop through array |
| O(n log n) | Linearithmic | Merge sort, quick sort |
| O(n²) | Quadratic | Nested loops |
| O(2ⁿ) | Exponential | Subset generation |
| O(n!) | Factorial | Permutations |

---

## Tips for Solving Coding Challenges

✅ Start simple, then optimize
✅ Use appropriate data structures
✅ Analyze time and space complexity
✅ Handle edge cases (empty, single element, null)
✅ Write clean, readable code
✅ Test your solution
✅ Explain your approach

---

**Continue with**: [Company-Specific Questions](../company-specific.md)
