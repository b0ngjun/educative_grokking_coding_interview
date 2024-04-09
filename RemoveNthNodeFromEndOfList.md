# Remove _n_ th Node From End Of List
Try to solve the Remove nth Node From End of List problem.

## Statement
Given a singly linked list, remove the nth node from the end of the list and return its head.

## Approach
1. Set two pointers, _right_ and _left_, at the head of linked list.
2. Move the _right_ pointer _n_ steps forward.
3. Move both _right_ and _left_ pointers forward until the _right_ pointer reaches the last node. At this point, the _left_ pointer will be pointing to the node behind the _n_ th last node.
4. Relink the _left_ node to the node next to _left_'s next node.
5. Return the head of the linked list.

## Code
```cpp
#include <iostream>
#include <string>
#include <vector>

EduLinkedListNode *RemoveNthLastNode(EduLinkedListNode *head, int n)
{
    EduLinkedListNode *right = head;
	EduLinkedListNode *left = head;

	for (int i = 0; i < n; i++) {
		right = right->next;
	}

	if (!right) {
		return head->next;
	}

	while (right->next) {
		right = right->next;
		left = left->next;
	}

	left->next = (left->next)->next;

    return head;
}

```

## Missed point
```cpp
	if (!right) {
		return head->next;
	}
```

## Review
//