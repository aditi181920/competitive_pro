**SLIDING WINDOW MINIMUM/ASCENDING MINIMA ALGORITHM:**
--

**PROBLEM STATEMENT:**

Given an array arr and an integer k, the problem boils down to computing for each index i: min(arr[i],arr[i-1],...arr[i-k+1])
  
**ALGORITHM:**

Slides a window of size k over arr computing at each step the current minimum.\
Psuedocode:
```cpp
for (i=0;i<arr.size();i++){
    remove arr[i-k] from the sliding window
    insert arr[i] into the sliding window
    output the smallest value in the window
}
```
The sliding window algorithm does the remove,insert and output step in amortized constt time.\
The time taken to run the algorithm is O(arr.size())
  
**STARTING FROM SUBOPTIMAL SOLUTION:**

1. SUBOPTIMAL SOLUTION: For all i just loop over all i to i-k+1 indexes [O(nk)]
2. SPEED UP 1: Use a sorted set (multiset) to speed up insert,delete,min value queries all upto logk max. Insert i and delete i-k index element for every i[O(nlogk)] 
3. SPEED UP 2: run-time can now be improved by a constant factor by using a head instead. All the heap operations (except finding the minima) have the same run-time complexity as the multiset versions, however heaps empirically performs better. Since C++ implementation of heaps does not allow arbitrary deletion of elements we can delete lazily. For each element in the priority queue we also store what index it was inserted from. Then when we query what the smallest element is, we discard if its index falls out of range of our current window\
---> Deleting lazily can actually make this algo perform rather badly. If the i/p is from N to 1, then a value is never deleted from the priority queue leading to log(n) insertions. However, on average this is empirically faster than the multiset version

**SLIDING WINDOW MINIMUM ALGORITHM:**

-> by putting in more effort after the idea of lazily deleting element we can get amortized O(1) run-time. \
-> also note we will use a deque here\
**OBSEERVATIONS:**\
--> Let's say we encountered an element x at our current index i\
--> Since x is the latest element anything greater than x present in queue will now never become a min becoz it is greater than x also inserted before x so x will remain valid after they have been removed so x is the last candidate which can be chosen as a min element further\
----> So we can just get rid of all elements greater than x and then push x at the back\
--> Notice that above idea also maintains the sorted property of the queue\
--> the front of queue might have value which shouldn't be in the window anymore but we can use the lazy delete idea here as well\
--> Note that we always insert the latest element and only remove previous element which are not req anymore so we will always obtain our answer in the queue

---> Now each element of arr is inserted into the deque and deleted from the deque atmost once.\
---> This gives a total run-time of O(n) for the algorithm (amortized O(1) per insertion/deletion in deque)
  
**SAMPLE CODE:**
```cpp 
void sliding_window_minimum(std::vector<int> & ARR, int K) {
  // pair<int, int> represents the pair (ARR[i], i)
  std::deque< std::pair<int, int> > window;
  for (int i = 0; i < ARR.size(); i++) {
     while (!window.empty() && window.back().first >= ARR[i])
       window.pop_back();
     window.push_back(std::make_pair(ARR[i], i));

     while(window.front().second <= i - K)
       window.pop_front();

     std::cout << (window.front().first) << ' ';
  }
}
```
--> deque supports constant time insertion, removal and lookups at the front and back of the queue
