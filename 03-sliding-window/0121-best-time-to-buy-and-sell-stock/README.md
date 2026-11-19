# Best Time to Buy and Sell Stock

- **LeetCode:** [#121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) · [NeetCode](https://neetcode.io/problems/buy-and-sell-crypto/question?list=blind75)
- **Difficulty:** Easy
- **Topic:** Sliding Window
- **Date solved:** 19/11/2026
- **Attempts / time taken:** Solved in an hour, on my 2nd try

## Problem
Given an array `prices` where `prices[i]` is the price of a stock on day `i`, pick one day to buy and a later day to sell to maximise profit. Return the maximum profit, or `0` if no profit is possible.

## Initial thoughts
What did you try first? Where did you get stuck?

## Approach
Since we must buy and sell on different days, there are two pointers that represent buy and sell (left and right). One pointer starts at 0 (the start of the array) and the other starts at 1, so we are comparing the first two values to see if they give us the most profit. But before that, we need to set up boundaries for what the pointers can do without causing errors:

1. Our while loop should loop until the right pointer reaches the end of the array, so `right < len(prices)`.
2. After that, within the loop, every time before we check the profit we have to ensure the sell (right pointer) is more than the buy (left pointer).

## Complexity
- **Time:** O(?)
- **Space:** O(?)

## Solution
See [`solution.py`](solution.py)

## Edge cases
- Prices only go down (answer is 0)
- Only one price
- All prices equal

## What I learned / how to recognise this pattern
How to easily spot a sliding window problem, and how I can apply the sliding window to a differently phrased question. This question required a different approach, as we did not need to track the index value like we did for LeetCode problem 3, so it did throw me off initially. Now, after completing the problem, I can truly understand how simple sliding windows are.

## Follow-up questions

**How would the approach change if we were allowed at most two transactions?**
A dynamic programming solution would be required. We maintain two transactions, tracking the best buy-sell pairs using two arrays (`left_profit` and `right_profit`), or optimize it using a state machine approach.

## Related problems

**Same list (Blind 75, Sliding Window)**
- [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) - Medium
- [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/) - Medium
- [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/) - Hard

**Same theme: tracking a running best while scanning once**
- [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/) - Medium (Blind 75, Greedy)

**Other Best Time to Buy and Sell Stock variants**
- [122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/) - Medium
- [123. Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/) - Hard
- [188. Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/) - Hard
- [309. Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/) - Medium
- [714. Best Time to Buy and Sell Stock with Transaction Fee](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/) - Medium
