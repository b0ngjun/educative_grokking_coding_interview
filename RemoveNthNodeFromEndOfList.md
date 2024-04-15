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

## Review
간단하게 접근한다면 Linkde List의 사이즈를 받고, 끝에서 부터 _n_ 번째 node로 접근하여 앞의 노드의 _ptr_ 을 저장하고, 바로 뒤에 있는 node와 연결하는 형태로 문제를 풀 수 있다. 그러나 이렇게 풀면 Linked List를 두번을 탐색 해야하지만 Two pointers 방법을 통하면 한번의 탐색으로 문제를 해결 할 수 있다.

### Missed point
```cpp
	if (!right) {
		return head->next;
	}
```

## To-Do
* 간단하게 풀었을 때의 코드 작성
