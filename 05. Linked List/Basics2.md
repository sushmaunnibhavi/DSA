# Detect loop in linked list:
Use Floyd's loop detection algo:
- Take 2 pointers
- Slow pointer moves 1 step
- Fast pointer moves 2 steps
- Why does this work? https://www.geeksforgeeks.org/how-does-floyds-slow-and-fast-pointers-approach-work/

# Check if singly linked list is palindrome:
1. Using Stack
2. Reversing the 2nd half of linked list:
- Get the middle of the linked list. 
- Reverse the second half of the linked list. 
- Check if the first half and second half are identical. 
- Construct the original linked list by reversing the second half again and attaching it back to the first half
```
// Function to check if given linked list is palindrome or not
bool isPalindrome(struct Node* head)
{
    struct Node *slow_ptr = head, *fast_ptr = head;
    struct Node *second_half, *prev_of_slow_ptr = head;
 
    // To handle odd size list
    struct Node* midnode = NULL;
 
    // initialize result
    bool res = true;
 
    if (head != NULL && head->next != NULL) {
 
        // Get the middle of the list. Move slow_ptr by 1 and fast_ptr by 2, slow_ptr will have the middle node
        while (fast_ptr != NULL && fast_ptr->next != NULL) {
            fast_ptr = fast_ptr->next->next;
 
            // We need previous of the slow_ptr for
            // linked lists with odd elements
            prev_of_slow_ptr = slow_ptr;
            slow_ptr = slow_ptr->next;
        }
 
        // fast_ptr would become NULL when there are even elements in list. And not NULL for odd elements. We need to skip the middle node for odd case and store it
        // somewhere so that we can restore the original list
        if (fast_ptr != NULL) {
            midnode = slow_ptr;
            slow_ptr = slow_ptr->next;
        }
 
        // Now reverse the second half and compare it with first half
        second_half = slow_ptr;
 
        // NULL terminate first half
        prev_of_slow_ptr->next = NULL;
 
        // Reverse the second half
        reverse(&second_half);
 
        // compare
        res = compareLists(head, second_half);
 
        // Construct the original list back
        reverse(
            &second_half); // Reverse the second half again
 
        // If there was a mid node (odd size case) which was not part of either first half or second half.
        if (midnode != NULL) {
            prev_of_slow_ptr->next = midnode;
            midnode->next = second_half;
        }
        else
            prev_of_slow_ptr->next = second_half;
    }
    return res;
}
```
```
// Function to reverse the linked list
void reverse(struct Node** head_ref)
{
    struct Node* prev = NULL;
    struct Node* current = *head_ref;
    struct Node* next;
 
    while (current != NULL) {
        next = current->next;
        current->next = prev;
        prev = current;
        current = next;
    }
    *head_ref = prev;
}
```

```
// Function to check if two input lists have same data
bool compareLists(struct Node* head1, struct Node* head2)
{
    struct Node* temp1 = head1;
    struct Node* temp2 = head2;
 
    while (temp1 && temp2) {
        if (temp1->data == temp2->data) {
            temp1 = temp1->next;
            temp2 = temp2->next;
        }
        else
            return 0;
    }
 
    // Both are empty return 1
    if (temp1 == NULL && temp2 == NULL)
        return 1;
 
    // Will reach here when one is NULL
    // and other is not
    return 0;
}
```
# Remove duplicates from an unsorted linked list:
1. Brute force:
- Use two loops, Outer loop is used to pick the elements one by one and the Inner loop compares the picked element with the rest of the elements. 
- Time complexity: O(N2)
2. Using sorting:
- Sort the elements using Merge Sort for Linked Lists.
- Remove duplicates in linear time using the algorithm for removing duplicates in sorted Linked List.
- Time Complexity: O(N logN)
3. Using hashing:
- Create a Unordered set to keep a track of the visited elements.
- Traverse the linked list from head to end node 
  - If current node is already present in the Hashset. Then delete the current node. 
  - Else move insert the node in the Hashset and move to the next node.
- Time Complexity: O(N)
- Auxiliary Space : O(N)

# Swap nodes in a linked list without swapping data:
- The problem has the following cases to be handled:
  - x and y may or may not be adjacent.
  - Either x or y may be a head node.
  - Either x or y may be the last node.
  - x and / or y may not be present in the linked list.
- Soln: The idea is to first search x and y in the given linked list. If any of them is not present, then return. While searching for x and y, keep track of current and previous pointers. First change next of previous pointers, then change next of current pointers.
```
void swapNodes(Node** head_ref, int x, int y)
{
    // Nothing to do if x and y are same
    if (x == y)
        return;
 
    // Search for x (keep track of prevX and CurrX
    Node *prevX = NULL, *currX = *head_ref;
    while (currX && currX->data != x) {
        prevX = currX;
        currX = currX->next;
    }
 
    // Search for y (keep track of prevY and CurrY
    Node *prevY = NULL, *currY = *head_ref;
    while (currY && currY->data != y) {
        prevY = currY;
        currY = currY->next;
    }
 
    // If either x or y is not present, nothing to do
    if (currX == NULL || currY == NULL)
        return;
 
    // If x is not head of linked list
    if (prevX != NULL)
        prevX->next = currY;
    else // Else make y as new head
        *head_ref = currY;
 
    // If y is not head of linked list
    if (prevY != NULL)
        prevY->next = currX;
    else // Else make x as new head
        *head_ref = currX;
 
    // Swap next pointers
    Node* temp = currY->next;
    currY->next = currX->next;
    currX->next = temp;
}

Time Complexity: O(N)
```

# Intersection of two Sorted Linked Lists:
1. Iterative:
```
/*This solution uses the temporary
 dummy to build up the result list */
Node* sortedIntersect(Node* a, Node* b)
{
    Node dummy;
    Node* tail = &dummy;
    dummy.next = NULL;
 
    /* Once one or the other
    list runs out -- we're done */
    while (a != NULL && b != NULL) {
        if (a->data == b->data) {
            push((&tail->next), a->data);
            tail = tail->next;
            a = a->next;
            b = b->next;
        }
        /* advance the smaller list */
        else if (a->data < b->data)
            a = a->next;
        else
            b = b->next;
    }
    return (dummy.next);
}
```

2. Recursive:
- TODO

# Intersection point of 2 linked list:
1. Using 2 loops
2. Hashing
3. Difference in node counts

