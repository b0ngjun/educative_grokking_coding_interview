# Find Median from a Data Stream
Try to solve the Find Median from a Data Stream problem.

## Statement
Create a data structure that can store a list of integers that can change in size over time and find the median from this dynamically growing list in constant time, O(1).

## Approach
1. Split up incoming numbers into two list - small and large. Those that are smaller than the current middle element are small, and those that are larger than it are large.
2. Maintain these lists as heaps so that the root of the small heap is the largest element in it and the root of large heap is the smallest element in it.
3. If the size of the large heap is grater than the size of small heap or, if size of small heap is greater than the size of the large heap + 1, rebalance the heaps.
4. If the number of elements is even, the median is the mean of the root of the two heaps. Else, it's the root of the small heap.

## Code
```cpp
class MedianOfStream
{
public:
    std::priority_queue<int> maxHeapForSmallNum;
    std::priority_queue<int, std::vector<int>, std::greater<int>> minHeapForLargeNum;

    MedianOfStream(){
        maxHeapForSmallNum = std::priority_queue<int>();
        minHeapForLargeNum = std::priority_queue<int, std::vector<int>, std::greater<int>>();
    }

    void InsertNum(int num){
        if (maxHeapForSmallNum.empty() || num <= maxHeapForSmallNum.top()) {
            maxHeapForSmallNum.push(num);
        } else {
            minHeapForLargeNum.push(num);
        }

        if (minHeapForLargeNum.size() + 1 < maxHeapForSmallNum.size()) {
            minHeapForLargeNum.push(maxHeapForSmallNum.top());
            maxHeapForSmallNum.pop();
        } else if (maxHeapForSmallNum.size() < minHeapForLargeNum.size()) {
            maxHeapForSmallNum.push(minHeapForLargeNum.top());
            minHeapForLargeNum.pop();
        } else {
            /* do nothing */
        }
    }

    double FindMedian(){
        if (maxHeapForSmallNum.size() == minHeapForLargeNum.size()) {
            return maxHeapForSmallNum.top() / 2.0 + minHeapForLargeNum.top() / 2.0;
        }
        
        return maxHeapForSmallNum.top();
    }
};
```