**SLIDING WINDOW:**
--

**Limitations:**
--

-> if the array is not sorted then the data should be completely positive or completely negative\
-> if the array is sorted then the data can be mixed 

we maintain a window that has a variable size and we consider some bounds to help mainuplate window size:\
-> when window is below the bound we can keep increasing the size of window from the right\
-> if it goes beyond the bound then we decrease then window size from left until it satisfies the bounds again

