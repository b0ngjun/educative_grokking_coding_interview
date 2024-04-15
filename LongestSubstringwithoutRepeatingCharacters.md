# Longest Substring without Repeating Characters
Try to solve the Longest Substring without Repeating Characters problem.

## Statement
Given a string, str, return the length of the longest substring without repeating characters.

## Approach
1. Initialize an empty hash map and a variable to track character indexes and the start of the window, respectively.
2. Traverse the string character by character. For each character, if the has map does not contain the current contain the current character, store it with its index as the value.
3. If the hash map contains the current character and its index falls within the current window, a repeating character is found. Otherwise, store it in the hash map with its index as the value.
4. When a repeating character is found, update the start of window th the previous location of current element and increment it. Also, calculate the length of the current window.
5. Update the longest substring seen so far if the length of the current window is greater than its current value.
6. Return the length of the logest substring.

## Code
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <unordered_map>

int FindLongestSubstring(string str){
    if(str.length() == 0) return 0;

    int n = str.length();
    int start = 0, len = 0, i = 0, res = 0;

    std::unordered_map<char, int> window;
    
    for(i = 0; i < str.length(); i++) {
        if(window.find(str[i]) == window.end()) {
            window.insert(make_pair(str[i], i));
        } else {
            if(start <= window.at(str[i])) {
                len = i - start;
                res = (res < len)? len : res;
                start = window.at(str[i]) + 1;
            }
            window.at(str[i]) = i;
        }
    }

    if(res < (i - start)) res = i - start;

   return res;
}
```

## Review
얼핏 보기에는 금방 풀 수 있을 것 같았는데, 구현에서 조건을 잘 신경써야합니다.
해당 문제로 unordered_map 컨테이너에 대해서는 알 수 있었습니다.
* std::unorderd_map은 hash map으로 구성되어있으며, std::map은 binary tree로 구현되어있음
* insert시에 key값이 같은게 있다면 덮어씌움
* find시에 없을 경우 가장 끝 값(end())를 가르킴

