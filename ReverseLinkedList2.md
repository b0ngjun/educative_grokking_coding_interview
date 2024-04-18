# Reverse Linked List 2
Try to solve the Reverse Linked List II problem.

## Statement
Given a singly linked list with _n_ nodes and two positions, left and right, the objective is to reverse the nodes of the list from left to right. Return the modified list.

## Approach
1. Start from the head node and traverse to the left position node while keeping track of the previous node.
2. From the left position node, traverse to the right position node. Keep track of the right position node and its next node.
3. Reverse the list from the left position node to the right position node.
4. Return the modified list.

## Code
1. Initialize a _dummy_ node.
2. Set the next node of _dummy_ to point to the head of the list.
3. Initialize a pointer, _prev_, to the _dummy_ node.
4. Initialize a _curr_ pointer, which points to the node next to _prev_.
5. Set _next_, to _curr.next_.
6. Update _curr.next_ to _next.next_
7. Update _next.next_ to _curr_
8. Update _prev.next_ to _next_

```cpp
EduLinkedListNode *ReverseBetween(EduLinkedListNode *head, int left, int right)
{
    if (!head || left == right) {
        return head;
    }

    EduLinkedListNode* dummy = new EduLinkedListNode(0);
    dummy->next = head;
    EduLinkedListNode* prev = dummy;

    for (int i = 0; i < left - 1; i++) {
        prev = prev->next;
    }

    EduLinkedListNode* curr = prev->next;

    for (int i = 0; i < right - left; i++) {
        EduLinkedListNode* nextNode = curr->next;
        curr->next = nextNode->next;
        nextNode->next = prev->next;
        prev->next = nextNode;
    }

    return dummy->next;
}
```

## Review
* left, right 전/후의 node들 next를 어떻게 바꿔줄 것인가가 ReverseLinkedList와는 다르게 고민해야할 부분
* Naive하게만 생각했는데, 해당 부분에 대한 좀 더 이해가 필요.

### Naive approach
1. find the _left_ and _right_
2. swap the values of the nodes pointed to by _left_ and the _right_ pointer
3. move the left pointer one step forward to the _(m+1)_ node.
4. if there is no _prev_, we can't update the _right_ pointer in the same in the way as we did for the _left_ pointer.

This time complexity of this solution is O(n^2).

```cpp

```