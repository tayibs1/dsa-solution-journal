# Two Sum

- **LeetCode:** [#1](https://leetcode.com/problems/two-sum/) · [NeetCode](https://neetcode.io/problems/two-integer-sum/question?list=blind75)
- **Difficulty:** Easy
- **Topic:** Arrays & Hashing
- **Date solved:** 27/11/2026
- **Attempts / time taken:** 2 attempts, 20 minutes

## Problem
Given an array of integers `nums` and an integer `target`, return the indices of the two different elements that add up to `target`. Exactly one valid pair exists, and the same element can't be used twice.

## Initial thoughts
we're given an array of integers `nums`, so every value has an index from 0 up to `len(nums) - 1`, and an integer `target`, which is what we're trying to hit by adding two of those values together. we return the two indices, not the values themselves.

my first idea was to use two pointers, `i` and `j`. `i` starts at index 0 (the first value) and `j` starts at index 1. for whatever `nums[i]` is, the number i actually need is `target - nums[i]` (the complement). so i check if `nums[j]` equals the complement. if it does, i've found the pair and return `[i, j]`. if it doesn't, i move `j` along the rest of the array looking for it.

if `j` gets to the end and there's no match, then `nums[i]` isn't part of the answer, so i move `i` forward one and start `j` again at `i + 1`. it doesn't need to go back to the start because any pair before that has already been checked, and `j` can't equal `i` because we can't use the same element twice. repeat until the pair is found. that's two nested for loops, so it's the brute force method and it's O(n²) time, because for every number we could be scanning the whole rest of the array.

thinking about where the time actually goes: the inner loop is only ever searching for one specific number, the complement. so the real question for each value is "have i already seen the number that pairs with this?". searching an array for that is O(n) every time, but if i store each number i've passed in a dictionary (value → index), like how i used a dictionary in LeetCode 3 (Longest Substring Without Repeating Characters), checking whether the complement is in there is O(1). so the rough plan is one pass through `nums` with enumerate: work out the complement, and if it's already in the dictionary, return its stored index with the current index. if it isn't, add the current number and its index to the dictionary and keep going. checking before adding matters, because otherwise a number could pair with itself (like `[3, 2, 4]` with target 6, where 3 + 3 isn't allowed). that should get it down to O(n) time, trading off O(n) space for the dictionary.

## Approach
* Create a hash map to store the value and index of every element in the array as you enumerate through it
* Enumerate Through the array using index i and work out the difference between the target youre trying to reach and the value of the current index you are on under the variable name diff
* Check if diff exists/stored in the hashmap
* If it does, then you return the indice value of the one stored in the hash map and the current indice you are on
* If not you store the value and indice that you are currently on in the hash map
* if you have enumerated through the whole array and no pair is found then youd return an empty array

## Complexity
- **Time:** O(n). We only go through the array once with enumerate, and for each number the work inside the loop is constant: one subtraction to get `diff`, one `in` check on the hash map, and maybe one insert. Looking something up or adding it to a hash map is O(1) on average, so n numbers × O(1) work each = O(n). That's the big win over brute force, where checking for the complement meant scanning the rest of the array every time (O(n²)).
- **Space:** O(n). The hash map is the extra memory. In the worst case the pair is the last two numbers, so we've stored almost every value and its index before we find it, which grows with the size of the array.

## Solution
See [`solution.py`](solution.py)

## Edge cases
- Negative numbers or zero in `nums`
- The same value appears twice (e.g. `[3, 3]`, target `6`)
- Half of `target` appears only once (e.g. `[3, 2, 4]`, target `6`, so `3` can't pair with itself)

## What I learned / how to recognise this pattern
my first idea was brute force, checking every pair with two loops, and it was only when i asked what the inner loop was actually doing that it clicked. it's only ever looking for one number, the complement (`target - n`). once you know exactly what you're looking for, you don't need to search for it, you just need to remember what you've seen. a hash map does that in O(1), which turns O(n²) into one pass. i'd already used a dictionary for value → index in LeetCode 3, so it was cool seeing the same tool solve a completely different problem. the other thing i learned is that the order matters: check for `diff` first, then store the current number, so a number can never pair with itself.

how to recognise it:
- the question asks you to find two things in an array that pair up (add to a target, match, cancel out)
- for every element you can work out exactly what its partner would have to be
- the array isn't sorted (if it is, two pointers might do it without extra space)
- you're basically asking "have i seen this before?" over and over. that's a hash map / set question
- the obvious solution is nested loops but that has a time complexity of o(n^2) and we want to find the most efficient runtime and space

## Follow-up questions

**What if the array was already sorted?**
Then you don't need the hash map. Put one pointer at the start and one at the end. If the sum is too small, move the left pointer right (makes the sum bigger). If it's too big, move the right pointer left (makes it smaller). Still O(n) time, but O(1) space because nothing is stored. This is exactly [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/).

**Can you do it in O(1) extra space without it being sorted?**
Only by giving up time. Brute force is O(1) space but O(n²) time. Sorting first and using two pointers is O(n log n), but sorting moves the numbers around so you'd have to keep their original indices, which costs O(n) space again. So the hash map is the best trade-off: a bit of memory for a much faster solution.

**What if there might be no answer?**
Return an empty array (or whatever the interviewer asks for) after the loop finishes. LeetCode guarantees exactly one solution, which is why the loop always returns before it ends.

**What if you need three numbers that add up to the target?**
Sort the array, then for each number fix it and run the sorted Two Sum (two pointers) on the rest to find the other two. That's O(n²). This is [15. 3Sum](https://leetcode.com/problems/3sum/), and the same idea extends to [18. 4Sum](https://leetcode.com/problems/4sum/) by adding another outer loop.

**What if you need all the pairs, not just one?**
Don't return on the first match. Collect each pair as you find it, and be careful with duplicate values so you don't count the same pair twice.

**What if the numbers arrive one at a time (a stream) instead of as an array?**
Keep the hash map around between calls: `add(number)` stores it, and `find(target)` checks every stored value for its complement. This is [170. Two Sum III - Data structure design](https://leetcode.com/problems/two-sum-iii-data-structure-design/) (LeetCode Premium).

## Related problems

**Same list (Blind 75, Arrays & Hashing)**
- [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/) - Easy
- [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/) - Easy
- [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/) - Medium

**Other Two Sum variants**
- [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) - Medium
- [15. 3Sum](https://leetcode.com/problems/3sum/) - Medium (Blind 75, Two Pointers)
- [18. 4Sum](https://leetcode.com/problems/4sum/) - Medium
