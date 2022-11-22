MAITRI RADHESH 
CSU ID #2831749

Task1: MIN-Heap

import java.util.Scanner; 
import java.io.IOException;
  
public class PQueue {   
    private int[] Heap;   
    private int index;   // let size of the the Heap be index
    private int size;   // let the maximum number of nodes be size 
  
    private static final int FRONT = 1;   
    public PQueue(int size)  {   
        this.size = size;   
        this.index = 0;   
        Heap = new int[this.size + 1];   
    }   
  
    private int parent(int posn)  {   // let position of the nodes be posn
        return posn / 2;   
    }   
  
    private void swap(int firstNode, int secondNode)  {   
        int temp;   
        temp = Heap[firstNode];   
        Heap[firstNode] = Heap[secondNode];   
        Heap[secondNode] = temp;   
    }     

    private boolean isEmpty(int posn)  {   
        if ((posn * 2) + 1 >= size || (posn * 2)  >= size) {   
            return true;   
        }   
        return false;   
    }   

    public void insert(int data)  {   
        if (index>= size) {   
            return;   
        }   
        Heap[index] = data;   
        int current = index;   
  
        while (Heap[current] <Heap[parent(current)]) {    
            swap(current, parent(current));   
            current = parent(current);   
        } 
        index++;
    }   
    
    public int removeMin()  {   
        int pop = Heap[FRONT];   
        Heap[FRONT] =Heap[index--];   
        heapdown();   
        return pop;   
    }   
  
  	private void heapdown(){
		minHeapify(FRONT); 
	}
	
    private void minHeapify(int posn)  {   
        if (!isEmpty(posn)) {   
            if (Heap[posn] > Heap[2*(posn)] || Heap[posn] > Heap[2*(posn) + 1]) {  
                if (Heap[2*(posn)] <Heap[2*(posn) + 1]) {   
                    swap(posn, 2*(posn));   
                    minHeapify(2*(posn));   
                }   
                else {   
                    swap(posn, 2*(posn) + 1);   
                    minHeapify(2*(posn) + 1);   
                }   
            }   
        }   
    }   
  
    public void displayHeap()  {   
        System.out.println("PARENT NODE" + "\t" + "LEFT CHILD NODE" + "\t" + "RIGHT CHILD NODE");  
        for (int k = 1; k <= index / 2; k++) {   
            System.out.print(" " + Heap[k] + "\t\t\t\t" + Heap[2 * k] + "\t\t\t\t" + Heap[2 * k + 1]);   
            System.out.println();   
        }   
    }   
  
    private void bottom_up()  {   
        for (int posn = (index / 2); posn >= 1; posn--) {   
            minHeapify(posn);   
        }   
    }   
 
    private void heapup(Scanner sc){
        boolean response;
        response = sc.nextBoolean();
        do{
            System.out.println("Do you want to insert any other element? ");
            System.out.println("Please enter 'true' or 'false' ");
        if (response){
            System.out.println("Please Enter the element that you want to insert:");
            int element = sc.nextInt();
            insert(element);
            bottom_up();
            System.out.println("After inserting the element "+ element +", the Minimum heap is:");  
            displayHeap();
        }
        else{
            System.out.println("No further changes in the Heap");
            }
        }
        while (response != false);
    }
 
    public static void main(String[] args) throws IOException {   
        int heapSize;  
        Scanner sc = new Scanner(System.in); 
        boolean response;
        System.out.println("Please Enter the size of the Minimum Heap:");  
        heapSize = sc.nextInt();  
        PQueue MinHeapheapObj = new PQueue(heapSize);  
        for(int i = 1; i<= heapSize; i++) {  
            System.out.print("Enter element " +i+ " : ");  
            int data = sc.nextInt();  
            MinHeapheapObj.insert(data);  
        }  
        MinHeapheapObj.bottom_up();   
        System.out.println("The Minimum Heap is :");   
        MinHeapheapObj.displayHeap();
        do{
           System.out.println("Do you want to remove the Minimum element?");
            System.out.println("Please enter 'true' or 'false' ");
            response = sc.nextBoolean();
            if (response){
                System.out.println("After removing the minimum element (i.e. the Root Node) "+ MinHeapheapObj.removeMin()+", the Minimum heap is:");   
                MinHeapheapObj.displayHeap();
            }
            else{
            System.out.println("No further deletions in the Heap");
            }
        }
        while (response != false); 
        MinHeapheapObj.heapup(sc);
        sc.close();
    }
}

Code to Compile: javac HeapQueue.java
Code to run: java HeapQueue

Output:
Please Enter the size of the Minimum Heap:
9
// uses the insert function to take input values
Enter element 1 : 56
Enter element 2 : 32
Enter element 3 : 67
Enter element 4 : 12
Enter element 5 : 22
Enter element 6 : 45
Enter element 7 : 31
Enter element 8 : 83
Enter element 9 : 71
The Minimum Heap is :
PARENT NODE	LEFT CHILD NODE	RIGHT CHILD NODE
 22				32				31
 32				67				45
 31				56				83
 67				71				0
Do you want to remove the Minimum element?
Please enter 'true' or 'false' 
true
After removing the minimum element (i.e. the Root Node) 22, the Minimum heap is:
PARENT NODE	LEFT CHILD NODE	RIGHT CHILD NODE
 0				32				31
 32				67				45
 31				56				83
 67				71				0
Do you want to remove the Minimum element?
Please enter 'true' or 'false' 
true
After removing the minimum element (i.e. the Root Node) 0, the Minimum heap is:
PARENT NODE	LEFT CHILD NODE	RIGHT CHILD NODE
 31				32				56
 32				67				45
 56				71				83
Do you want to remove the Minimum element?
Please enter 'true' or 'false' 
false
No further deletions in the Heap

Task 2: 
(a) Heap-Sort:

import java.util.Scanner; 

public class MinHeap {   
    private int[] Heap;   
    private int index;   // let size of the the Heap be index
    private int size;   // let the maximum number of nodes be size 
  
    private static final int FRONT = 1;   
    public MinHeap(int size)  {   
        this.size = size;   
        this.index = 0;   
        Heap = new int[this.size + 1];   
    }   
  
    private int parent(int posn)  {   // let position of the nodes be posn
        return posn / 2;   
    }   
  
    private void swap(int firstNode, int secondNode)  {   
        int temp;   
        temp = Heap[firstNode];   
        Heap[firstNode] = Heap[secondNode];   
        Heap[secondNode] = temp;   
    }     

    private boolean isEmpty(int posn)  {   
        if ((posn * 2) + 1 >= size || (posn * 2)  >= size) {   
            return true;   
        }   
        return false;   
    }   

    public void insert(int data)  {   
        if (index>= size) {   
            return;   
        }   
        Heap[index] = data;   
        int current = index;   
  
        while (Heap[current] <Heap[parent(current)]) {    
            swap(current, parent(current));   
            current = parent(current);   
        } 
        index++;
    }   
    
    private void minHeapify(int posn)  {   
        if (!isEmpty(posn)) {   
            if (Heap[posn] >Heap[2*(posn)] || Heap[posn] >Heap[2*(posn) + 1]) {  
                if (Heap[2*(posn)] <Heap[2*(posn) + 1]) {   
                    swap(posn, 2*(posn));   
                    minHeapify(2*(posn));   
                }   
                else {   
                    swap(posn, 2*(posn) + 1);   
                    minHeapify(2*(posn) + 1);   
                }   
            }   
        }   
    }   
  
    public void displayHeap()  {   
        System.out.println("PARENT NODE" + "\t" + "LEFT CHILD NODE" + "\t" + "RIGHT CHILD NODE");  
        int j;
        for (j = 1; j <= index / 2; j++) {   
            System.out.print(" " + Heap[j] + "\t\t\t\t" + Heap[2 * j] + "\t\t\t\t" + Heap[2 * j + 1]);   
            System.out.println();   
        }   
    }   

    private void heapSort()  {   
        for (int posn = (index / 2); posn >= 1; posn--) {   
            minHeapify(posn);   
        }   
    }   
 
    public static void main(String[] args) {   
        int heapSize;  
        Scanner sc = new Scanner(System.in);  
        System.out.println("Please Enter the size of the Minimum Heap:");  
        heapSize = sc.nextInt();  
        MinHeap MinHeapheapObj = new MinHeap(heapSize);  
        for(int i = 1; i<= heapSize; i++) {  
            System.out.print("Enter element " +i+ " : ");  
            int data = sc.nextInt();  
            MinHeapheapObj.insert(data);  
        }  
        MinHeapheapObj.heapSort();   
        System.out.println("The Minimum Heap is :");   
        MinHeapheapObj.displayHeap();  
        sc.close();
    }
}

Code to Compile: javac HeapSort.java
Code to run: java HeapSort

Output:
Please Enter the size of the Minimum Heap:
7
Enter element 1 : 45
Enter element 2 : 12
Enter element 3 : 34
Enter element 4 : 89
Enter element 5 : 27
Enter element 6 : 31
Enter element 7 : 98
The Minimum Heap is :
PARENT NODE	LEFT CHILD NODE	RIGHT CHILD NODE
 27				31				89
 31				45				34
 89				98				0

(b). Quick-Sort:
import java.io.*;
import java.util.*;
import java.util.Random;
    
public class QuickSort {
    
    public static void swapping(int[] A, int s, int i) {
        int temp;
        temp = A[s];
        A[s] = A[i];
        A[i] = temp;
    }
    
    public static void quickSort(int[] A, int l, int r) {
        if (l < r) {
            int partition = LomutoPartition(A, l, r); 
            quickSort(A, l, partition - 1);
            quickSort(A, partition + 1, r); 
        }
    }

    public static int LomutoPartition(int[] A, int l, int r) {
        int p = A[l]; 
        int s = l; 
        for(int i = l+1; i <= r; i++) { 
            if (A[i] < p) {
                s++;
                
                swapping(A, s, i);
            }
        }
        swapping(A, l, s); 
        return s; 
    }
    
    public static void main(String[] args) {
        Random random = new Random();
        Scanner sc=new Scanner(System.in);  
        
        int a =0;
        System.out.println("QuickSort using Random Numbers: ");
        System.out.println("Enter the number of elements you want to store:");  
        a=sc.nextInt(); 
        int []B = new int[a];
        for(int i = 0; i < a; i++) {
            B[i] = random.nextInt(100);
        }
        System.out.println("Array Before sorting: ");
        System.out.println(Arrays.toString(B));
        System.out.println("Array After sorting: ");
        quickSort(B, 0, a - 1);
        System.out.println(Arrays.toString(B));
    }
}

Code to Compile: javac QuickSort.java
Code to run: java QuickSort

Output:
QuickSort using Random Numbers: 
Enter the number of elements you want to store:
10
Array Before sorting: 
[58, 64, 51, 72, 51, 89, 11, 76, 48, 91]
Array After sorting: 
[11, 48, 51, 51, 58, 64, 72, 76, 89, 91]

Task 3: Time Complexity:

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Random;
import java.util.Arrays;

public class sorting {
    
    private static int[] A;
    private static int[] arrCopy;
    private static BufferedReader read;
    private static Random randomGenerator;
    private static int size;
    private static int random;

    private static void printArray(String msg) {
    	System.out.print(msg + " [" + A[0]);
        for(int i=1; i<size; i++) {
            System.out.print(", " + A[i]);
        }
        System.out.println("]");
    }
    
    public static void swap(int i, int j){
        int temp;
        temp=A[i];
        A[i]=A[j];
        A[j]=temp; 
    }
    
    public static void heapify(int i, int n) { 
        int min = i;
        int left = 2*i;
        int right = 2*i+1;
        if(left < n && A[left] > A[min]) 
            min = left;
        if(right < n && A[right] > A[min]) 
            min = right;
        if(min != i) {  
            swap(i, min);
            heapify(min, n);
        }
    }
    
    public static void heapsort(){
        for (int i = size/2; i >= 0; i--) 
            heapify(i, size);
        for(int i= size-1; i > 0;i--) {
            swap(0, i);       
            heapify(0, i);   
        }
    }
    
    private static void quicksort(int l, int r) {
	    int i = l, j = r;
	    int pivot = A[r];
	    while (i <= j) {
    	      while (A[i] < pivot) 
    	        i++;
    	      while (A[j] > pivot) 
    	        j--;
    	      if (i <= j) {
    	        swap(i, j);
    	        i++;
    	        j--;
    	      }
        }
    	if (l < j)
    	      quicksort(l, j);
    	if (i < r)
    	      quicksort(i, r);
    }

    public static void timeoutput(String input) {
        long startTime; 
        long endTime;
        System.out.println();
        // Heap sort      
        for (int i=0; i<size; i++) A[i] = arrCopy[i];
        if (size < 101) printArray("in");
        startTime = System.currentTimeMillis();
        heapsort();
        endTime = System.currentTimeMillis();
        if (size < 101) printArray("out");
        System.out.println("Heapsort takes: " + (endTime-startTime) + " ms.");
        // Quick sort
        for (int i=0; i<size; i++) A[i] = arrCopy[i];
        if (size < 101) printArray("in");
        startTime = System.currentTimeMillis();
        quicksort(0, size-1);
        endTime = System.currentTimeMillis();
        if (size < 101) printArray("out");   
        System.out.println("Quicksort takes: " + (endTime-startTime) + " ms.");
    }
    
    public static void main(String[] args) {
        read = new BufferedReader(new InputStreamReader(System.in));
        randomGenerator = new Random();
        try {
            System.out.print("Please enter the size of the array : ");
            size = Integer.parseInt(read.readLine());
        } catch(Exception ex){
            ex.printStackTrace();
        }
        A = new int[size];
        arrCopy = new int[size];
	    random = size*10;
        for(int i=0; i<size; i++) 
           A[i] = arrCopy[i] = randomGenerator.nextInt(random);    
        timeoutput("random");
    }
}

Code to Compile: javac TimeComplexity.java
Code to run: java TimeComplexity

Output:

Please enter the size of the array : 50000

Heapsort takes: 21 ms.
Quicksort takes: 20 ms.

From the output we can infer that the Quick sort Algorithm is faster than the Heap sort algorithm.
