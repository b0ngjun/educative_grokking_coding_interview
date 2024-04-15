# Find the Duplicate Number
Try to solve the Find The Duplicate Number problem.

## Statement
Given an array of positive numbers, _num_, such that the values lie in the range [1, n], inclusive, and that there are _n+1_ numbers in the array, find and return the duplicate number prsent in _nums_. THere is only one repeated number in _nums_.
(You cannot modify the given array _nums_. You have to solve the problem using only constant extra space.)

## Approach
1. Travers in _nums_ using the _fast_ and _slow_ pointers.
2. Move pointers until they meet. The _slow_ pointer moves once and the _fast_ pointer moves twice as fast as the slow pointer.
3. After the pointers meet, traverse in _nums_ again.
4. Move the _slow_ pointer from the start of _nums_ and the _fast_ pointer from the meeting point at the same speed(one step) until they meet again.
5. Return the _fast_ pointer.

## Code
```cpp
#include <iostream>
#include <vector>

int FindDuplicate(vector<int> nums)
{
    int fast = nums[0];
    int slow = nums[0];

    while(true) {
        slow = nums[slow];
        fast = nums[nums[fast]];
        
        std::cout << "(" << slow << ", " << fast << ")" << std::endl;
        if(slow == fast) break;
    }

    std::cout << "====================" << std::endl;

    slow = nums[0];
    while(slow != fast) {
        slow = nums[slow];
        fast = nums[fast];

        std::cout << "(" << slow << ", " << fast << ")" << std::endl;
    }

    return fast;
}
```

## Review
문제의 제한 조건인 
> Note: You cannot modify the given array nums. You have to solve the problem using only constant extra space.

으로 해당 패턴으로 푸는게 의미가 있지 않나 라는 생각을 합니다. 아직까지는 해당 패턴이 얼마나 유의미하게 쓰일지에 대한 부분은 와닿지가 않아 다른 example을 더 풀어봐야 할 것 같습니다. 하지만 재밌는 문제라 생각합니다.