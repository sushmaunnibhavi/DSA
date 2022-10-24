# Representation:
```
class Node {
public:
    int data;
   
    // Pointer to next node in DLL
    Node* next;
   
    // Pointer to previous node in DLL
    Node* prev;
};
```

# Insertion:
1. At beginning:
```
void push(Node** head_ref, int new_data)
{
    /* 1. allocate node */
    Node* new_node = new Node();
 
    /* 2. put in the data */
    new_node->data = new_data;
 
    /* 3. Make next of new node as head
    and previous as NULL */
    new_node->next = (*head_ref);
    new_node->prev = NULL;
 
    /* 4. change prev of head node to new node */
    if ((*head_ref) != NULL)
        (*head_ref)->prev = new_node;
 
    /* 5. move the head to point to the new node */
    (*head_ref) = new_node;
}
```
2. After given node:
```
void insertAfter(Node* prev_node, int new_data)
{
    /*1. check if the given prev_node is NULL */
    if (prev_node == NULL) {
        cout << "the given previous node cannot be NULL";
        return;
    }
 
    /* 2. allocate new node */
    Node* new_node = new Node();
 
    /* 3. put in the data */
    new_node->data = new_data;
 
    /* 4. Make next of new node as next of prev_node */
    new_node->next = prev_node->next;
 
    /* 5. Make the next of prev_node as new_node */
    prev_node->next = new_node;
 
    /* 6. Make prev_node as previous of new_node */
    new_node->prev = prev_node;
 
    /* 7. Change previous of new_node's next node */
    if (new_node->next != NULL)
        new_node->next->prev = new_node;
}
```
3. At end:
```
void append(Node** head_ref, int new_data)
{
    /* 1. allocate node */
    Node* new_node = new Node();
 
    Node* last = *head_ref; /* used in step 5*/
 
    /* 2. put in the data */
    new_node->data = new_data;
 
    /* 3. This new node is going to be the last node, so
        make next of it as NULL*/
    new_node->next = NULL;
 
    /* 4. If the Linked List is empty, then make the new
        node as head */
    if (*head_ref == NULL) {
        new_node->prev = NULL;
        *head_ref = new_node;
        return;
    }
 
    /* 5. Else traverse till the last node */
    while (last->next != NULL)
        last = last->next;
 
    /* 6. Change the next of last node */
    last->next = new_node;
 
    /* 7. Make last node as previous of new node */
    new_node->prev = last;
 
    return;
}
```
# Deletion:
1. Steps:
  - If the node to be deleted is the head node then make the next node as head.
  - If a node is deleted, connect the next and previous node of the deleted node.
2. Algo:
  - Let the node to be deleted be del.
  - If node to be deleted is head node, then change the head pointer to next current head.
    ```
    if headnode == del then
      headnode =  del.nextNode
    ```
  - Set prev of next to del, if next to del exists.
    ```
    if del.nextNode != none 
      del.nextNode.previousNode = del.previousNode
    ```
  - Set next of previous to del, if previous to del exists.
    ```
    if del.previousNode != none 
      del.previousNode.nextNode = del.next
    ```
# Reverse a dll:
- Traverse the linked list using a pointer
- Swap the prev and next pointers for all nodes
- At last, change the head pointer of the doubly linked list
```
void reverse(Node** head_ref)
{
    Node* temp = NULL;
    Node* current = *head_ref;
 
    /* swap next and prev for all nodes of
    doubly linked list */
    while (current != NULL) {
        temp = current->prev;
        current->prev = current->next;
        current->next = temp;
        current = current->prev;
    }
 
    /* Before changing the head, check for the cases like
       empty list and list with only one node */
    if (temp != NULL)
        *head_ref = temp->prev;
}
```
