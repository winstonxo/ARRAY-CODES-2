
                                STEP BY STEP CODE ANALYSIS:
PROBLEM [1] analysis ; 
1. Class: Person
The Person class is designed to store and manage basic student information. 
+1

Member Variables

Name: A variable to store the student's full name. 
+1


Student ID: A variable to store the unique identification number for the student. 
+1


Age: A variable to store the student's age. 
+1

2. Member Functions
init()

Purpose: This function initializes the member variables of the Person class with input values. 
+1

Operations:

Copies the provided input name into the class variable for the student's name. 
+1

Saves the input student ID into the class variable for the student ID. 
+1

Saves the input age into the class variable for the student's age. 
+1

printStudentInfo()

Purpose: This function displays the current information stored in the Person object. 
+1

Operations:

Prints the Name, Student ID, and Age of the student. 
+1

Ensures the output format matches the specified expected results for consistency. 
+1

getID()

Purpose: To retrieve the student's identification number. 
+1


Returns: The student ID currently stored in the object. 
+1

getAge()

Purpose: To retrieve the student's age. 
+1


Returns: The age value currently stored in the object. 
+1

getName()

Purpose: To retrieve the student's name. 
+1


Returns: The name string currently stored in the object. 
+1

3. Global Function: personSwap()
void personSwap(...)

Purpose: This function facilitates the exchange of data between two Person objects. 
+1


Inputs: Receives two Person objects as parameters. 
+1

Operations:

Swaps the Name between the two objects. 
+1

Swaps the Student ID between the two objects. 
+1

Swaps the Age between the two objects. 
+1


Outcome: After execution, both input objects will have exchanged all of their stored student information. 
+1


PROBLEM [2] analysis;

1. Two-Tier Dynamic Allocation
Since you cannot we cant a simple static array, we must build the 10x10 grid in two steps:

Step A: Allocate an array of 10 "pointers." Think of these as 10 folders, each intended to hold a row.

Step B: For each of those 10 folders, allocate an array of 10 integers.

2. Initializing with memset
Once the memory is allocated, it may contain "garbage" data (old numbers left over from previous tasks).

The Action: Use the memset utility. This tells the computer to look at a specific block of memory and set every single byte to zero. This represents an "Empty" seat.

3. Data Replication with memcpy
If you need to copy the entire seat map (for a backup or a new arrangement):

The Logic: Instead of using a loop to copy every seat one by one, use memcpy.

The Action: This function takes the "Source" address and the "Destination" address and performs a high-speed, bulk copy of the entire memory block.

4. Grid Visualization (print_seat)
The display function must turn the raw numbers into a clean 10x10 grid.

The Formatting Rule: To maintain a perfect square shape, every number must be two digits. If a seat is empty (0) or has a single-digit ID (7), you must force the display to show 00 or 07.

The Traversal: Use a nested loop (rows and columns) to visit every seat and print it.

5. Reverse-Order Deallocation (Cleanup)
This is the most critical step. Because manually you "asked" for memory, you must manually "return" it.

The Order Matters: You cannot delete the "folders" (row pointers) while they are still holding the "rows" (integers).

The Process: 1.  Loop through and delete each of the 10 rows individually.
2.  Once the rows are gone, delete the main array of pointers.

Outcome: All memory is returned to the system, preventing a "Memory Leak."


  PROBLEM [3] ANALYSIS ;


Step 1: Initialize the Master Pointer List
To store multiple words, you first create a "list of lists." In C/C++, this is represented as a double pointer (char**).

The Logic: Think of this as a shelf that only holds addresses. You allocate enough space on this "shelf" to hold a specific number of pointers. At this stage, no actual words exist yet—only the capacity to point to where they will eventually live.

Step 2: Adding a Word (Allocation & Copying)
When you want to add a word (e.g., "Apple"), you cannot simply point to a temporary variable. You must create permanent space on the heap.

The Calculation: Use a string length utility to find the size. You must allocate exactly length + 1 bytes. The +1 is for the Null Terminator (\0), which tells the computer where the word ends.

The Action: Once you have a new block of memory of the exact size, use a string copy function (strcpy) to move the characters from your source into this new heap-allocated block.

The Link: Store the address of this new block into one of the slots in your Master Pointer List.

Step 3: Searching for a Word
Since you are dealing with raw pointers, you cannot use an "equals" operator (==) to compare strings (that would only compare their memory addresses).

The Action: Use a string comparison utility (strcmp). This function looks at the characters inside the memory blocks one by one. If it returns 0, you have found a match.

Step 4: Modifying a Word
Modifying is more complex than simply overwriting. If the new word is longer than the old one, it won't fit in the existing memory block.

The Safe Approach: 1. Find the index of the word you want to change.
2. Free the memory of the old word.
3. Calculate the size of the new word.
4. Allocate a new block of the correct size.
5. Copy the new word into that block.

Step 5: Deleting a Word and Shifting
This is the most technical part of the assignment. When you delete a word, you cannot leave a "hole" in the middle of your list.

Phase A (The Free): First, you must release the memory for the specific word you are deleting.

Phase B (The Shift): To keep the list continuous, you must use a loop to move every pointer that comes after the deleted word one position to the left.

The Result: The "hole" is filled, and the list remains organized, but it is now one element shorter.

Step 6: Full Memory Deallocation (Cleanup)
Before the program ends, you must return all borrowed memory to the system. This must be done in a bottom-up order.

The Action: You iterate through the Master Pointer List and free each individual word's memory block one by one.

The Final Step: Once all individual words are gone, you free the Master Pointer List itself.

motive: This ensures that no data remains in the system's memory (zero memory leaks).

