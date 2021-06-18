package algs24;

import java.util.Arrays;


import stdlib.StdIn;
import stdlib.StdOut;
// Above: Given import statements.

/**
 *  The PtrHeap class represents a priority queue of generic keys.
 */

// Given class and Node definitions.
public class PtrHeap<K extends Comparable<? super K>> {

static class Node<K> {
K value;
Node<K> parent;
Node<K> lchild;
Node<K> rchild;

}

//These variables were implemented for ease of use.
private K[] pq;
private int N;
private int MAXN;

//A few given variables
private int size;
private Node<K> root;

// Detection to see if a node is the root of the heap (the location at the top of the heap)
boolean isRoot(Node<K> n){ return n == root; }

// Given exch method to swap two nodes in the heap using a temporary node.
void exch(Node<K> n1, Node<K> n2) {
// only swap items of nodes
Node<K> tmp = new Node<K>();
tmp.value = n1.value;
n1.value = n2.value;
n2.value = tmp.value;
}

/* Self-Implemented method to find the last spot in the list and returns the Node with default values. 
   This is useful because it allows other methods to call the find method without having to re-type it each time.
*/
public Node<K> find(int n){
	 String bin = Integer.toBinaryString(n);
	 Node<K> x = root;
	 Node<K> hold = new Node<K>();
	 for(int i = 1; i < bin.length(); i++) {
	 if(bin.charAt(i) == '0' && x.lchild != null) x = x.lchild;
	 else if (bin.charAt(i) == '0' && x.lchild == null) x.lchild = hold;
	 else if (bin.charAt(i) == '1' && x.rchild != null) x = x.rchild;
	 else x.rchild = hold;
	 }
	 hold.parent = x;
	 return hold;
	 }
   
   
// Self-Implemented method similar to the find method, but is implemented to be called by the delmax method
public Node<K> findLast(int n) {
	 String bin = Integer.toBinaryString(n);
	 Node <K> x = root;
	 for(int i = 1; i < bin.length(); i++) {
	 if(bin.charAt(i) == '0' && x.lchild != null) x = x.lchild;
	 else if (bin.charAt(i) == '1' && x.rchild != null) x = x.rchild;
	 }
	 return x;
	 }

// Self-Implemented void method to swim a node by comparing it to its parents. If the node has a greater value than the parent nodes,
// it will move it up in the heap.
private void swim(Node<K> n) {
	Node<K> curr = n;
	while (curr != root && less(curr.parent.value, curr.value )) {
		exch(curr, curr.parent);
		curr = curr.parent;
	}
	
}


// Self-implemented void method to sink a node by comparing a node's values to its children. If the children are greater,
// the parent is swapped with it child.
private void sink(Node<K> n) {
	Node<K> curr = n;
	if(n == null);
	else {
	while(curr.lchild!=null && curr.rchild!= null) {
		if(less(curr.value, curr.lchild.value) && less(curr.value, curr.rchild.value)) {
			break;
		}
		Node<K> big = new Node<K>();
		if(less(curr.lchild.value,curr.rchild.value)) {
			big = curr.lchild;
		} else {
			big = curr.rchild;
		}
		exch(curr, big);
		curr = big;
	}
	}
}


// Given void method to print the Heap for debugging.
private void printHeap(Node<K> n){
if(n == null)  return ;
System.out.print(n.value+" ");
printHeap(n.lchild);
printHeap(n.rchild);
}


@SuppressWarnings("unchecked")

// Method implemented to create the priority queue
public PtrHeap() {
	MAXN = size;
	pq = (K[])new Comparable[size + 1];
	N = 0;
	root = null;
	
}
   

// Method implemented to check if the size of the heap is 0.
public boolean isEmpty() {
	return size == 0;
}
//Given less method to detect for comparing key values.
boolean less(K u, K v) { return (u.compareTo(v) < 0);} 

/** Return the number of items on the priority queue. */
public int size() {
	//return the size variable because it indicates the number of keys.
return size; }


/**
* Objective for insert: Return the largest key on the priority queue.
* Throw an exception if the priority queue is empty.
*/
public K max() {
	// Exception case
if(root == null) throw new IllegalArgumentException();

// Root is always the largest value, so it is returned:
return root.value;
}

/** Add a new key to the priority queue. */
public void insert(K x) {
	// To insert a value, the value gets added to the bottom and swam up after passing error catch cases.
	
	
	size++;
  
  // Catch for size 1 heaps.
	if(size == 1) {
	  Node<K> newRoot = new Node<K>();
	  newRoot.value = x;
	  newRoot.parent = newRoot;
	  root = newRoot;
	}
  
  // Catch for if the root has an empty left child.
	else if (root.lchild == null) {
	  Node<K> l = new Node<K>();
	  l.value = x;
	  l.parent = root;
	  root.lchild = l;
	  swim(l);
	}
  
  // Catch for if the root has an empty right child.
	else if (root.rchild == null) {
	  Node<K> r = new Node<K>();
	  r.value = x;
	  r.parent = root;
	  root.rchild = r;
	  swim(r);
	}
  
  // Otherwise, insert is run as normal
	else {
	  Node<K> insert = find(size);
	  insert.value = x;
	  swim(insert);
	}
	
}
	


/**
* Objective ofr delMax: Delete and return the largest key on the priority queue.
* Throw an exception if the priority queue is empty.
*/

// Implemented by swapping the first (root) and last values on the heap, sinking the new root, and deleting the last value.
// Since this is a maximum heap, the maximum value will always be stored in the root.
public K delMax() {

  // Detection for size 0.
	if (size == 0) return null;
  
  
	K max = max();
	Node<K> last = findLast(size);
  
  // Exchange the first and last nodes
	exch(root, last);
  
  // Use the parent of the last value to delete the new, swapped root value.
	Node<K> par = last.parent;
	if (par.lchild == last) par.lchild = null;
	else par.rchild = null;
  
  // Decrement size and sink the root. Return the deleted value.
	size--;
	sink(root);
	return max;
}


// Given method for debugging, since it will display the heap.
private void showHeap() {
	printHeap(root);
	System.out.println();
}

//Given main method
public static void main(String[] args) {
	PtrHeap<String> pq = new PtrHeap<>();
	StdIn.fromString("10 20 30 40 50 - - - 05 25 35 - - - 70 80 05 - - - - ");
	while (!StdIn.isEmpty()) {
		StdOut.print ("pq:  "); pq.showHeap();
		String item = StdIn.readString();
		if (item.equals("-")) StdOut.println("max: " + pq.delMax());
		else pq.insert(item);
  }
  StdOut.println("(" + pq.size() + " left on pq)");

}

}
