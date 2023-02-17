# Bug 1 Core Aborted

## A) How is your program acting differently than you expect it to?
- The program is not running and is stopping completely and not telling me where my error is. It's not producing any output and instead just says "Aborted (core dump)"

## B) Brainstorm a few possible causes of the bug
- I am freeing something that I shouldn't be freeing
- Maybe I didn't malloc enough space where I should've
- Maybe I am accessing something I shouldn't be

## C) How you fixed the bug and why the fix was necessary
- I was freeing a temporary variable that stored key information that I used to produce the outcome of my function. I realized this and deleted the line of code where I was freeing my variable and it fixed the core aborted error. Since I was freeing this when I shouldn't have, it was causing a core dump and killing my program since I needed the information inside of this variable for the result and attempted to access it again after I freed it.


# Bug 2 Segmentation Fault

## A) How is your program acting differently than you expect it to?
- The program isn't running HTIterator_Get() at all and it should be retrieving the value at a specific node, but it's not retrieving anything and is stopping our code from running completely

## B) Brainstorm a few possible causes of the bug
- Maybe we freed something we weren't supposed to and then tried to access it again
- Maybe we needed to make something a pointer and we didn't make it as the proper type that it should've been
- Maybe we need to free somewhere and it's causing issues because we're keeping track of something that we shouldn't be

## C) How you fixed the bug and why the fix was necessary
- We searched through our code and found that in our HTIterator_get() function, we were calling LLIterator_Get on a double pointer instead of passing in a regular pointer along with its address location. This was a crucial mistake and we fixed it by removing one of the pointers to our variable. The fix was necessary because we kept running into the error message "temp may be used uninitalized" when it was a double pointer, and by passing in the address instead as a single pointer to LLIterator_Get, the temp is initialzed and fixed the issues.


# Bug 3 Another Segfault

## A) How is your program acting differently than you expect it to?
- We expected the program to run and execute the tests, but it was pausing after the test
  suite came across our HTIteratorNext method.

## B) Brainstorm a few possible causes of the bug
- moving to the next node when there is none in our method
- maybe our fields are still connected to something they shouldn't be after we move them up
  and down the buckets in HTIteratorNext()
- Maybe we needed to be freeeing the iterator we created after using it

## C) How you fixed the bug and why the fix was necessary
- We went to office hours and had some assistance with looking for our error. We realized that
  after we allocated space for our iterator that we were using to traverse the new bucket after we moved it
  down the list, we weren't freeing it if we needed to move down another bucket again. This was causing a memory issue and we needed to fix it to get our code to run and have the proper space each time. This was a key component in fixing the segfault, but another issue we faced with this same segfault was that we weren't repointing the linked list if it was invalid to the invalid index. This was making our program think the index was something we were pointing to prior, so we needed to repoint it to the invalid index to fix the error.
