MINIMUM STACK / MINIMUM QUEUE
--

**AIM:**
```sh
-> finding smallest element of the stack in O(1)
-> finding smallest element of the queue in O(1)
-> find min in all subarrays of a fixed length in an array in O(n)
```
1. STACK MODIFICATION:
---
```cpp
    stack<pair<int,int>> st;
```
-> pair.first = element itself\
-> pair.second = min in the stack starting from this element and below


--> Adding an element:
```cpp
int new_min = st.empty() ? new_elem : min(new_elem,st.top().second);
st.push({new_elem,new_min});
```
--> Removing an element:
```cpp
int removed_element = st.top().first;
st.pop();
```
--> Finding the minimum:
```cpp
int minimum = st.top().second;
```
2. QUEUE MODIFICATION:
---
>METHOD 1
```cpp
     deque<int> q;
```
--> only store elements in the queue that are needed to determine the minimum that too in non decreasing order\
--> if a new element is to be added, we remove all trailing elements of the queue that are larger than the new element, and then add the new element to the queue\
--> while removing element we have to take care that if element to be removed is present at head then only remove it, else we will end up accidently removing a min element which was not supposed to be removed

**IMPLEMENTATION:**\
--> finding the minimum:
```cpp
int minimum = q.front();
```
--> adding an element:
```cpp
while (!q.empty() && q.back() > new_element)
  q.pop_back();
q.push_back(new_element);
```
--> removing an element:
```cpp
if(!q.empty() && q.front() == remove_element)
  q.pop_front();
```
---> on avg all these operation only take O(1) time (because every element can only be pushed and popped once). ?://

>METHOD 2
```cpp
  deque<pair<int,int>> q;
  int cnt_added = 0;
  int cnt_removed = 0;
```
-> pair.first = element itself\
-> pair.second = index at which it was added\
-> modified version of method 1 which helps in removing element without knowing the element to be removed\
-> we remove element from head if it is the oldest element present in the queue among all other elements present

--> finding the minimum:
```cpp
int minimum = q.front().first;
```
--> adding an element:
```cpp
while(!q.empty() && q.back().first>new_element)
  q.pop_back();
q.push_back({new_element,cnt_added});
cnt_added++;
```
--> removing an element:
```cpp
if(!q.empty() && q.front().second == cnt_removed)
  q.pop_front();
cnt_removed++;
```
>METHOD 3
```cpp
   stack<pair<int,int>> s1,s2;
```
-> idea is to stimulate queue using two stacks both stack will be of the modified form\
-> add new elements to stack s1 and remove elements from stack s2\
-> at any time if the stack s2 is empty, we will move all elements from s1 to s2(order will get reversed as older elements will come to top and newer to bottom)\
-> min of queue is min both both the stacks\
-> all operations performed in O(1) on avg ( each element will be once added to stack s1, once transferred to s2, and once popped from s2) ?://

--> finding the minimum:
```cpp
if(s1.empty()||s2.empty())
  minimum = s1.empty()?s2.top().second:s1.top().second;
else
  minimum = min(s1.top().second, s2.top().second);
 ```
 --> adding element:
 ```cpp
int minimum = s1.empty()?new_element:min(new_element, s1.top().second);
s1.push({new_element, minimum});
```
--> removing an element:
```cpp
if(s2.empty()){
  while(!s1.empty()){
    int element = s1.top().first;
    s1.pop();
    int minimum = s2.empty()?element: min(element, s2.top().second);
    s2.push({element,minimum});
  }
}
int remove_element = s2.top().first;
s2.pop();
```

3. FINDING MINIMUM OF ALL SUBARRAYS OF FIXED LENGTH:
---

-> We can solve this by using any of the modified queue and sliding window technique\
-> take first m elements (size of subarray)\
-> now start taking min and adding new element and removing oldest until we can repeat the process\
**COMPLEXITY:** O(n)

