# Microsoft
#include <iostream> using namespace std; // Representation of a node struct Node { 	int data; 	Node* next; }; // Function to insert node void insert(Node** root, int item) { 	Node* temp = new Node; 	Node* ptr; 	temp->data = item; 	temp->next = NULL;  	if (*root == NULL) 		*root = temp; 	else { 		ptr = *root; 		while (ptr->next != NULL) 			ptr = ptr->next; 		ptr->next = temp; 	} }  void display(Node* root) { 	while (root != NULL) { 		cout << root->data << " "; 		root = root->next; 	} }  Node *CreateLinkedList(int *arr, int n) { 	cout<<"\nLinked List Created Successfully"; 	cout<<"\nElements of Linked List are:"; 	Node *root = NULL; 	for (int i = 0; i < n; i++) 		insert(&root, *(arr+i)); return root; }   int main() { 	int arr[]={11,12,13,14,15}; 	int n = sizeof(arr) / sizeof(arr[0]); 	Node* root = CreateLinkedList(arr, n); 	display(root); 	return 0; }

Second implementation(Reversing a linked list):
#include <iostream>
using namespace std;

/* Link list node */
struct Node {
	int data;
	struct Node* next;
	Node(int data)
	{
		this->data = data;
		next = NULL;
	}
};

struct LinkedList {
	Node* head;
	LinkedList() { head = NULL; }

	/* Function to reverse the linked list */
	void reverse()
	{
		// Initialize current, previous and
		// next pointers
		Node* current = head;
		Node *prev = NULL, *next = NULL;

		while (current != NULL) {
			// Store next
			next = current->next;

			// Reverse current node's pointer
			current->next = prev;

			// Move pointers one position ahead.
			prev = current;
			current = next;
		}
		head = prev;
	}

	/* Function to print linked list */
	void print()
	{
		struct Node* temp = head;
		while (temp != NULL) {
			cout << temp->data << " ";
			temp = temp->next;
		}
	}

	void push(int data)
	{
		Node* temp = new Node(data);
		temp->next = head;
		head = temp;
	}
};

int main()
{
	/* Start with the empty list */
	LinkedList ll;
	ll.push(20);
	ll.push(4);
	ll.push(15);
	ll.push(85);

	cout << "Given linked list\n";
	ll.print();

	ll.reverse();

	cout << "\nReversed Linked list \n";
	ll.print();
	return 0;
}


Third implementation(Deleting/or Destroying a linked list):
// C++ program to delete a linked list
#include <bits/stdc++.h>
using namespace std;

/* Link list node */
class Node
{
	public:
	int data;
	Node* next;
};

/* Function to delete the entire linked list */
void deleteList(Node** head_ref)
{

/* deref head_ref to get the real head */
Node* current = *head_ref;
Node* next;

while (current != NULL)
{
	next = current->next;
	free(current);
	current = next;
}

/* deref head_ref to affect the real head back
	in the caller. */
*head_ref = NULL;
}

/* Given a reference (pointer to pointer) to the head
of a list and an int, push a new node on the front
of the list. */
void push(Node** head_ref, int new_data)
{
	/* allocate node */
	Node* new_node = new Node();

	/* put in the data */
	new_node->data = new_data;

	/* link the old list off the new node */
	new_node->next = (*head_ref);

	/* move the head to point to the new node */
	(*head_ref) = new_node;
}

/* Driver code*/
int main()
{
	/* Start with the empty list */
	Node* head = NULL;

	/* Use push() to construct below list
	1->12->1->4->1 */
	push(&head, 1);
	push(&head, 4);
	push(&head, 1);
	push(&head, 12);
	push(&head, 1);

	cout << "Deleting linked list";
	deleteList(&head);

	cout << "\nLinked list deleted";
}
