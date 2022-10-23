# Representation:
```
class Node{
    int value;
   
  // Points to the next node.
    Node next;
}
```

# Insertion:
1. At beginning:
```
struct Node *addBegin(struct Node *last, int data)
{
if (last == NULL)
    return addToEmpty(last, data);
 
// Creating a node dynamically.
struct Node *temp
        = (struct Node *)malloc(sizeof(struct Node));
     
// Assigning the data.
temp -> data = data;
 
// Adjusting the links.
temp -> next = last -> next;
last -> next = temp;
     
return last;
}
```
2. At end:
```
struct Node *addEnd(struct Node *last, int data)
{
if (last == NULL)
    return addToEmpty(last, data);
 
// Creating a node dynamically.
struct Node *temp =
        (struct Node *)malloc(sizeof(struct Node));
     
// Assigning the data.
temp -> data = data;
 
// Adjusting the links.
temp -> next = last -> next;
last -> next = temp;
last = temp;
     
return last;
}
```
3. Others:
- Create a node, say T. 
- Search for the node after which T needs to be inserted, say that node is P. 
- Make T -> next = P -> next; 
- P -> next = T.

# Deletion:
```
// Function to delete a given node
// from the list
void deleteNode(Node** head, int key)
{
 
    // If linked list is empty
    if (*head == NULL)
        return;
 
    // If the list contains only a
    // single node
    if ((*head)->data == key && (*head)->next == *head) {
        free(*head);
        *head = NULL;
        return;
    }
 
    Node *last = *head, *d;
 
    // If head is to be deleted
    if ((*head)->data == key) {
 
        // Find the last node of the list
        while (last->next != *head)
            last = last->next;
 
        // Point last node to the next of
        // head i.e. the second node
        // of the list
        last->next = (*head)->next;
        free(*head);
        *head = last->next;
        return;
    }
 
    // Either the node to be deleted is
    // not found or the end of list
    // is not reached
    while (last->next != *head && last->next->data != key) {
        last = last->next;
    }
 
    // If node to be deleted was found
    if (last->next->data == key) {
        d = last->next;
        last->next = d->next;
        free(d);
    }
    else
        cout << "no such keyfound";
}
```
# Advantages of Circular Linked Lists: 
- Any node can be a starting point.
- Useful for implementation of a queue
- Circular lists are useful in applications to repeatedly go around the list. For example, when multiple applications are running on a PC, it is common for the operating system to put the running applications on a list and then cycle through them, giving each of them a slice of time to execute, and then making them wait while the CPU is given to another application. 

# Disadvantages of circular linked list:
- It is possible for the code to go into an infinite loop if it is not handled carefully.
- It is harder to find the end of the list and control the loop.
- Reversing a circular list is more complicated than singly or doubly reversing a circular list.

# Applications of circular linked lists:
- Multiplayer games use this to give each player a chance to play.
- A circular linked list can be used to organize multiple running applications on an operating system. These applications are iterated over by the OS.

# 

