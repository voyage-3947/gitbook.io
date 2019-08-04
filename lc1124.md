## 1124. Longest Well-Performing Interval

We are given hours, a list of the number of hours worked per day for a given employee.

A day is considered to be a tiring day if and only if the number of hours worked is (strictly) greater than 8.

A well-performing interval is an interval of days for which the number of tiring days is strictly larger than the number of non-tiring days.

Return the length of the longest well-performing interval.

Example: 
Input: hours = [9,9,6,0,6,6,9]
Output: 3
Explanation: The longest well-performing interval is [9,9,6].

## Idea
Greedy.
- Turn into an array with only 1 and -1. 
- Traverse from first day, keep sum.
- If sum > 0, from first day to now, # of 1 > # of -1.
- If sum - 1 has been found, from sum - 1 to now, # of 1 > # of -1.

```
int longestWPI(vector<int> &h){
	int res = 0, sum = 0;
    unorder_map<int, int> m; //num -> first exist position
	for(int i = 0; i < h.size(); i++){
		h[i] > 8 ? sum += 1: sum -= 1;
		if(sum > 0) res = i + 1;
		if(m.find(sum) == m.end()) m[sum] = i;// not exist yet
		if(m.find(sum - 1) != m.end()) res = max(res, i - m[sum - 1]);
	}
    return res;
}
```


Examples:

1  1  -1   -1  -1   -1  1


1  2  1    0   -1   -2  -1
-------
1  2  2+m[0] 

1 1 1 -1 -1 -1 -1 1 1  1 1 1

1 2 3 2   1  0  -1  0  1  2  3  4
------------------------------
          4+1                diff + m[2]







-1    -1    -1      1       1

-1    -2    -3     -2      -1

0      0     0    max(res, pos - m[sum - 1])











