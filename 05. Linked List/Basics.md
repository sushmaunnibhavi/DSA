# Why linked list?
  - Size of array fixed
  - Insertion of a new element / Deletion of a existing element in an array of elements is expensive
  
# Cons:
  - Random access is not allowed
  - Extra memory space for a pointer is required with each element of the list
  - Not cache friendly. Since array elements are contiguous locations, there is locality of reference which is not there in case of linked lists.

# Difference b/w linked list and array:
![image](https://user-images.githubusercontent.com/29684959/197130538-6c9e0ce0-cc7a-48c8-b498-e1eea265b574.png)

# Representation of linked list:
```
class Node
{
    public:
    int data;
    Node *next;
};
```

# Inserting a node:
1. At front:
   ```
   //Given a reference (pointer to pointer) to the head of a list and an int, inserts a new node on the front of the list.
   void push Node** head_ref, int new_data)
   {
      // 1. allocate node
       Node* new_node = new Node();
 
      // 2. put in the data
       new_node->data = new_data;
 
      // 3. Make next of new node as head
      new_node->next = (*head_ref);
 
      // 4. Move the head to point to the new node
      (*head_ref) = new_node;
    
   }
   Time complexity: O(1)
   ```
   
2. Add a node after a given node: 
   - Firstly, check if the given previous node is NULL or not.
   - Then, allocate a new node and
   - Assign the data to the new node
   - And then make the next of new node as the next of previous node. 
   - Finally, move the next of the previous node as a new node.
```
// Given a node prev_node, insert a new node after the given prev_node
void insertAfter(Node* prev_node, int new_data)
{
 
    // 1. Check if the given prev_node is NULL
    if (prev_node == NULL) {
        cout << "The given previous node cannot be NULL";
        return;
    }
 
    // 2. Allocate new node
    Node* new_node = new Node();
 
    // 3. Put in the data
    new_node->data = new_data;
 
    // 4. Make next of new node as
    // next of prev_node
    new_node->next = prev_node->next;
 
    // 5. move the next of prev_node
    // as new_node
    prev_node->next = new_node;
}

Time complexity:O(1), since prev_node is already given as argument in a method, no need to iterate over list to find prev_node
```

3. Add a node at the end: 
  ```
// Given a reference (pointer to pointer) to the head of a list and an int, appends a new node at the end
void append(Node** head_ref, int new_data) 
{ 
   
    // 1. allocate node
    Node* new_node = new Node();
   
    // Used in step 5
    Node *last = *head_ref;
   
    // 2. Put in the data
    new_node->data = new_data; 
   
    // 3. This new node is going to be 
    // the last node, so make next of 
    // it as NULL
    new_node->next = NULL; 
   
    // 4. If the Linked List is empty,
    // then make the new node as head
    if (*head_ref == NULL) 
    { 
        *head_ref = new_node; 
        return; 
    } 
   
    // 5. Else traverse till the last node
    while (last->next != NULL)
    {
        last = last->next; 
    }
   
    // 6. Change the next of last node
    last->next = new_node; 
    return; 
}
Time complexity: O(N)
  ```
  
# Deleting a node:
1. Beginning:
```
Point head to the next node i.e. second node
    temp = head
    head = head->next
    
Make sure to free unused memory
    free(temp); or delete temp;
```
2. Middle:
```
Keeps track of pointer before node to delete and pointer to node to delete
    temp = head;
    prev = head;
    for(int i = 0; i < position; i++)
    {
        if(i == 0 && position == 1)
            head = head->next;
            free(temp)
        else
        {
            if (i == position - 1 && temp)
            {
                prev->next = temp->next;
                free(temp);
            }
            else
            {
                prev = temp;
                if(prev == NULL) // position was greater than number of nodes in the list
                    break;
                temp = temp->next; 
            }
        }
    }
```
3. End:
```
Point head to the previous element i.e. last second element
    Change next pointer to null
    struct node *end = head;
    struct node *prev = NULL;
    while(end->next)
    {
        prev = end;
        end = end->next;
    }
    prev->next = NULL;
    
Make sure to free unused memory
    free(end); or delete end;
```
# Recursive method of node deletion:
```
// Deletes the node containing 'info' part as val and alter the head of the linked list (recursive method)
void deleteNode(node*& head, int val)
{
 
    // Check if list is empty or we
    // reach at the end of the
    // list.
    if (head == NULL) {
        cout << "Element not present in the list\n";
        return;
    }
 
    // If current node is the
    // node to be deleted
    if (head->info == val) {
        node* t = head;
 
        // If it's start of the node head
        // node points to second node
        head = head->link;
 
        // Else changes previous node's
        // link to current node's link
        delete (t);
        return;
    }
    deleteNode(head->link, val);
}

Time Complexity: O(n)
```
  
  


