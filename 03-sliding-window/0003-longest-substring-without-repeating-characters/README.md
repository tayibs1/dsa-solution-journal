# Longest Substring Without Repeating Characters

- **LeetCode:** [#3](https://leetcode.com/problems/longest-substring-without-repeating-characters/) · [NeetCode](https://neetcode.io/problems/longest-substring-without-duplicates/question?list=blind75)
- **Difficulty:** Medium
- **Topic:** Sliding Window
- **Date solved:** 16/11/2026
- **Attempts / time taken:**

## Problem
Given a string `s`, find the length of the longest substring that contains no repeated characters.

## Initial thoughts
This was my first sliding window question so I had to learn the concept of sliding windows first going step by step of understanding how sliding windows work, the concept of why to use dictionaries instead of lists, what enumerate does and what it looks like visiualised. essentially, i was questioning why for everything why so that every line of code I can understand and build a genuine understanding of what sliding windows is and not what this specific question wants

## Approach
1: last{} creates an empty dictionary which remembers the index for every character for where it was seen. Why Dictionary? O(1) lookup and update by character and store the index which a **Set** cannot.

2: left = best = 0 both counters start at 0. Why Chained? two variables, one line, 0 is an **immutable** integer (cannot be changed) so safe to chain both variables

3: enumerate(s) means it starts fromthe first string char and its corresponding index so:
        -(0,'a') -> right = 0 , c = 'a' where right stores the index value and c variable stores the char string value

        - we use enum so we have index and the character together. **Tuple Unpacking** splits index and character 

4: if c in last and last[c] >= left
    -so we are first checking if c which is the current string char value we are pointing to and whether that string value which in this case right now is the first character of the string s and we check the dictionary last to see whether it exists in that list. That is the first statement that must be true for this if statement to be true and execute. the second statement is whether the last[c] which is the index value attached to c in the dictionary is more than the leftmost pointer in the sliding window just to ensure we are in the sliding window
    
    -if both statements are true we move to the next line which would be the process of a duplicate character in the window

5: left = last[c] + 1
    - This moves the left point which is the left side of the sliding window by one space to the right so now it will be pointing to the index value of the second character in string 

6: last[c] = right
    - If the if condition is not satisfied (i.e. the character isn't already in the window), Python skips the if block and moves on to this line, which is part of the for loop. Here it stores the current index (right) of the current character (c) in the dictionary. So now we have created the sliding window which it will keep track of
7: best = max(best, right -left + 1)
    - Here we work out the length of the sliding window  by subtracting the right and left points which form the sliding window and we add one as both indexes of the sliding window are counted

8: The for loop visits every character of s; each iteration updates best with the longest valid window so far. When the loop ends, best is the answer and is returned.

## Complexity
- **Time:** O(n) -  the for loop runs n times and the if statement checks the dictionary lookup which is on average O(1)
- **Space:** O(n) s = "abcdef"   → dict grows to 6 entries -> O(n) space
s = "aaaaaa" -> dict stays at 1 entry   -> O(1) space

## Solution
See [`solution.py`](solution.py)

## Edge cases
- Empty string
- All characters the same
- All characters unique

## What I learned / how to recognise this pattern
-If a problem asks for the longest/shortest/Max/Min something over a **Continguous** subarray or substring -> very likely a sliding window

**What i learnt:**
- What a sliding window concept actually is
- Why we use a dictionary instead of set/list
- what enumerate does
- Time and Space Complexities and why


## Companies that ask this
*Researched 2026-11-17. LeetCode's own per-company frequency data is behind Premium, so this is compiled from public sources. Treat counts as indicative, not official.*

**Most commonly reported (appear across nearly every source)**

| Company | Reported frequency* | Evidence |
|---------|---------------------|----------|
| Amazon | 127 | [Tutorialspoint](https://www.tutorialspoint.com/practice/longest-substring-without-repeating-characters.htm), [Finxter](https://blog.finxter.com/?p=30922), [Taro](https://www.jointaro.com/interviews/amazon/longest-substring-without-repeating-characters) |
| Google | 95 | [Tutorialspoint](https://www.tutorialspoint.com/practice/longest-substring-without-repeating-characters.htm), [Taro](https://www.jointaro.com/interview-insights/google/longest-substring-without-repeating-characters), [DEV Community](https://dev.to/akhilpokle/longest-substring-without-repeating-characters-solving-google-interview-question-2n72) |
| Microsoft | 73 | [Tutorialspoint](https://www.tutorialspoint.com/practice/longest-substring-without-repeating-characters.htm), [Workat.tech](https://workat.tech/problem-solving/practice/longest-substring-without-repeat/) |
| Meta (Facebook) | 68 | [Tutorialspoint](https://www.tutorialspoint.com/practice/longest-substring-without-repeating-characters.htm), [Codemia](https://codemia.io/practice/longest-substring-without-repeating-characters) (frequent in phone screens), [Taro](https://www.jointaro.com/interviews/meta/longest-substring-without-repeating-characters) |
| Apple | 45 | [Tutorialspoint](https://www.tutorialspoint.com/practice/longest-substring-without-repeating-characters.htm) |
| Bloomberg | 42 | [Tutorialspoint](https://www.tutorialspoint.com/practice/longest-substring-without-repeating-characters.htm), [LeetCode discuss: Bloomberg phone screen](https://leetcode.com/discuss/interview-experience/386438/) |

\*Counts are Tutorialspoint's own "asked in" numbers and are not independently verified. Use them for relative ranking only.

**Also reported (individual interview reports)**
- Adobe: [Finxter](https://blog.finxter.com/?p=30922)
- Goldman Sachs (senior role): [Hello Interview](https://www.hellointerview.com/community/questions/longest-substring/cm5eh7nrh04n3838oxavsnhul)
- Snowflake (onsite): [PracHub](https://prachub.com/interview-questions/longest-substring-without-repeating-characters)
- Antra (technical screen): [PracHub](https://prachub.com/coding-questions/longest-substring-without-repeating-characters)
- Cisco (variant wording): [PracHub](https://prachub.com/interview-questions/longest-substring-without-repeated-characters)
- Others appearing in a mirror of LeetCode's tags: Alibaba, Uber, ByteDance, Huawei, Zillow, Yahoo, Grab, eBay, Twitch, Atlassian ([GitHub mirror](https://github.com/aryan1shrivastava/LeetCode-2/blob/master/leetcode/3.%20Longest%20Substring%20Without%20Repeating%20Characters))

**Takeaway:** this is one of the most commonly reported sliding window questions, with Amazon, Google, Meta, Microsoft and Bloomberg the safest bets.
## Related problems

**Same list (Blind 75, Sliding Window)**
- [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) - Easy
- [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/) - Medium
- [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/) - Hard

**Same pattern: longest/shortest window with a condition**
- [904. Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/) - Medium
- [1004. Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/) - Medium
- [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/) - Medium
- [159. Longest Substring with At Most Two Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/) - Medium (Premium)
- [340. Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/) - Medium (Premium)

**Windows that track character counts**
- [567. Permutation in String](https://leetcode.com/problems/permutation-in-string/) - Medium
- [438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/) - Medium

**Harder sliding window follow-ups**
- [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/) - Hard
