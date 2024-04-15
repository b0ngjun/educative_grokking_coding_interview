# Task Scheduler
Try to solve the Task Scheduler problem.

## Statement
Given a character array _tasks_, where each character represents a unique task and a positive integer _n_ that represents the cooling period between any two identical tasks, find the minimum number of time units the CPU will need to complete all the given tasks. Each task requires one unit to perform, and the CPU must wait for at least n units of time before it can repeat the same task. During the cooling period, the CPU can perform other tasks or remain idle.

## Approach
1. Count and store the frequencies of all the tasks.
2. Sort the tasks based on the frequencies.
3. Start scheduling the tasks in the descending order of their frequencies, and compute the idle time during the process.
4. Calculate the total time by adding the number of tasks and the idle time.

## Code
```cpp
#include <vector>

int LeastTime(const std::vector<char>& tasks, int n) {
    std::unordered_map<char, int> frequencies;
    for (char t : tasks) {
        frequencies[t] = frequencies[t] + 1;
    }

    std::vector<std::pair<char, int>> sortedFrequencies(frequencies.begin(), frequencies.end());

    std::sort(sortedFrequencies.begin(), sortedFrequencies.end(), [](const auto& lhs, const auto& rhs) {
        return lhs.second < rhs.second;
    });

    int maxFreq = sortedFrequencies.back().second();
    sortedFrequencies.pop_back();

    int idleTime = (maxFreq - 1) * n;

    while(!sortedFrequencies.empty() && idleTime > 0) {
        idleTime -= std::min(maxFreq - 1, sortedFrequencies.back().second);
        sortedFrequencies.pop_back();
    }
    idleTime = std::max(0, idleTime);

    return tasks.size() + idleTime;
}
```

## Review
Task가 몇 개 있는지, 각 Task마다 몇 번 수행되어야하는지 안다고하면, 많은 것 부터 차례대로 하나씩 넣어서 길이를 계산
idleTime으로 계산하여 size와 더한다는 점이 해당 솔루션의 접근 방법
Functor, lambda, for_each, sort with lambda