# Two pointers toolkit
- some observations while solving 2 pointers problems
# Start
- most standard type of 2 pointers to be used is from 2 ends `0` and `n-1` on an array, we just make decision on which pointer is to be moved when?
  - like when in [3 sum](./3-sum.md) or [two-sum-II](./two-sum-II.md) where we operate on sorted array while finding 2 nums that which have some specific sum, and if currsum if less move left pointer to right `l++`, else if currsum is more move right pointer to left `r--`
  - or like in [water container](./container-with-most-water.md) or [trapping rainwater](./trapping-rain-water.md) problem where we moved the pointer that had smaller value in it 
- [palindrom](./valid-palindrome.md) problem had same problem, we just iterated from both end going one step at a time, skipping or checking based on some condition
- one point to remember that I read online,  pointers mostly have when something has to do from both end, and the pointers converge to each other, like they come closer as iterations occur, if they may diverge or go fwd/bkwd, then it's a sliding window problem not  pointer