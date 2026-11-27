# Two Sum

- **LeetCode:** [#1](https://leetcode.com/problems/two-sum/) · [NeetCode](https://neetcode.io/problems/two-integer-sum/question?list=blind75)
- **Difficulty:** Easy
- **Topic:** Arrays & Hashing
- **Date solved:** 27/11/2026
- **Attempts / time taken:**

## Problem
Given an array of integers `nums` and an integer `target`, return the indices of the two different elements that add up to `target`. Exactly one valid pair exists, and the same element can't be used twice.

## Initial thoughts
we're given an array of integers `nums`, so every value has an index from 0 up to `len(nums) - 1`, and an integer `target`, which is what we're trying to hit by adding two of those values together. we return the two indices, not the values themselves.

my first idea was to use two pointers, `i` and `j`. `i` starts at index 0 (the first value) and `j` starts at index 1. for whatever `nums[i]` is, the number i actually need is `target - nums[i]` (the complement). so i check if `nums[j]` equals the complement. if it does, i've found the pair and return `[i, j]`. if it doesn't, i move `j` along the rest of the array looking for it.

if `j` gets to the end and there's no match, then `nums[i]` isn't part of the answer, so i move `i` forward one and start `j` again at `i + 1`. it doesn't need to go back to the start because any pair before that has already been checked, and `j` can't equal `i` because we can't use the same element twice. repeat until the pair is found. that's two nested for loops, so it's the brute force method and it's O(n²) time, because for every number we could be scanning the whole rest of the array.

thinking about where the time actually goes: the inner loop is only ever searching for one specific number, the complement. so the real question for each value is "have i already seen the number that pairs with this?". searching an array for that is O(n) every time, but if i store each number i've passed in a dictionary (value → index), like how i used a dictionary in LeetCode 3 (Longest Substring Without Repeating Characters), checking whether the complement is in there is O(1). so the rough plan is one pass through `nums` with enumerate: work out the complement, and if it's already in the dictionary, return its stored index with the current index. if it isn't, add the current number and its index to the dictionary and keep going. checking before adding matters, because otherwise a number could pair with itself (like `[3, 2, 4]` with target 6, where 3 + 3 isn't allowed). that should get it down to O(n) time, trading off O(n) space for the dictionary.

## Approach
The key insight / pattern, step by step.

## Complexity
- **Time:** O(?)
- **Space:** O(?)

## Solution
See [`solution.py`](solution.py)

## Edge cases
- Negative numbers or zero in `nums`
- The same value appears twice (e.g. `[3, 3]`, target `6`)
- Half of `target` appears only once (e.g. `[3, 2, 4]`, target `6`, so `3` can't pair with itself)

## What I learned / how to recognise this pattern
-

## Follow-up questions

**Question?**
Answer.

## Related problems

**Same list (Blind 75, Arrays & Hashing)**
- [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/) - Easy
- [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/) - Easy
- [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/) - Medium

**Other Two Sum variants**
- [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) - Medium
- [15. 3Sum](https://leetcode.com/problems/3sum/) - Medium (Blind 75, Two Pointers)
- [18. 4Sum](https://leetcode.com/problems/4sum/) - Medium
