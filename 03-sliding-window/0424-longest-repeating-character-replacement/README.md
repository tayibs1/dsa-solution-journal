# Longest Repeating Character Replacement

- **LeetCode:** [#424](https://leetcode.com/problems/longest-repeating-character-replacement/) · [NeetCode](https://neetcode.io/problems/longest-repeating-substring-with-replacement/question?list=blind75)
- **Difficulty:** Medium
- **Topic:** Sliding Window
- **Date solved:** 24/11/2026
- **Attempts / time taken:**

## Problem
Given a string `s` of uppercase English letters and an integer `k`, you may choose any character of the string and change it to any other uppercase letter at most `k` times. Return the length of the longest substring containing the same letter you can get after performing those replacements.

## Initial thoughts
Im given a string with characters of the same type all letters and it says specifically return the length of the longest substring so clearly we are moving through the different characters and returning the highest possible length of the substring with the same characters so this is a sliding window problem but however we cant keep track of where within the string we are so we need to convert the string into an array so we can use the python function list(s) to convert every character in the string into an array  and then we can have a Left point which points to 0 which is the first character in the Array and then Right pointer which points to index value 1 which is the second character in the array. and then we constrain the right pointer so it doesnt go past the length of the array into an infinite loop so we use a while loop and also ensure that k > 0 and within that loop we compare if the characters stored in Index L and R are the same if they are we work out the length between R and L  and then increase R by 1 to move the right pointer as we performed a swap  otherwise if R is not the same as L then we make the the charact3er pointing to right the same as Left and remove 1 from K and then L =R or maybe its the other way round in the if statement we compare if they are not equal and if they are equal we just move to the next until its not and k has been exhausted  but if they are equal we work out the length between R and L

### First iteration

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        

        l = 0
        r = 1
        best = 0

        arr = list(s)

        while r < len(s):
            if arr[l] != arr[r] and k != 0:
                arr[r] = arr[l]
                best = max(best, r - l + 1)
                k = k - 1
            else:
                best = max(best, r - l + 1) 
            r += 1
        return best
```

it passes case one but case two it fails because k is only 1 but it replaces all the letters in the string not only 1 so clearly k has an issue maybe its not stopping after k hits 0 so need to find a way around this

### Second iteration

Reordered the logic (count the replacement first, only update `best` while `used <= k`) without adding anything new:

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:

        l = 0
        r = 1
        best = 0
        used = 0

        arr = list(s)

        while r < len(s):
            if arr[l] != arr[r]:
                arr[r] = arr[l]
                used += 1
            if used <= k:
                best = max(best, r - l + 1)
            r += 1
        return best
```

This fixed the first two test cases, but failed on a later one (passed 8 / 39):

```
s = "ABAA"
k = 0

Your output: 0
Expected output: 2
```

Trace of the failing case:

| r | compare | used | window valid? | best |
|---|---------|------|---------------|------|
| 1 | `A` vs `B`, differ | 1 | no, 1 > 0 | 0 |
| 2 | `A` vs `A`, equal | 1 | no, `used` is still 1 | 0 |
| 3 | `A` vs `A`, equal | 1 | no | 0 |

Why it fails:
1. `l` is stuck at 0, so only windows starting at the first character are ever tried. The best answer here is `"AA"` at indexes 2 and 3.
2. `used` never goes down, so after one mismatch it stays above `k` for the rest of the string.

So `l` needs to move forward when the window becomes invalid, and `used` needs to drop when the character being dropped was a mismatch.

## Approach
The key insight / pattern, step by step.

## Complexity
- **Time:** O(?)
- **Space:** O(?)

## Solution
See [`solution.py`](solution.py)

## Edge cases
- `k = 0`
- Single character string
- All characters the same
- `k` is as large as or larger than the string length

## What I learned / how to recognise this pattern
-

## Follow-up questions

**Question?**
Answer.

## Related problems

**Same list (Blind 75, Sliding Window)**
- [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) - Medium
- [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) - Easy
- [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/) - Hard

**Same pattern: longest window allowed up to k "bad" elements**
- [1004. Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/) - Medium
- [2024. Maximize the Confusion of an Exam](https://leetcode.com/problems/maximize-the-confusion-of-an-exam/) - Medium
- [1493. Longest Subarray of 1's After Deleting One Element](https://leetcode.com/problems/longest-subarray-of-1s-after-deleting-one-element/) - Medium
- [487. Max Consecutive Ones II](https://leetcode.com/problems/max-consecutive-ones-ii/) - Medium (Premium)
