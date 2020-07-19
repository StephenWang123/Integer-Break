# Integer Break

## Description
Given a positive integer _n_, break it into the sum of **at least** two positive integers and maximize the product of those integers. Return the maximum product you can get.

Examples:\
2 -> 1 * 1 = **1**\
3 -> 2 * 1 = **2**\
4 -> 2 * 2  = **4**\
5 -> 3 * 2  = **6**\
10 -> 3 * 3 * 4 = **36**\

## Discussion
The brute-force approach to this question would be to list all the combinations of numbers that have a sum of **n**, then find the combination that has the highest product. 

This approach has an exponential runtime O(2<sup>n</sup>), since each subsequent integer **n** requires you to generate twice the number combinations as the previous **n**.

## Solution
The key to efficiently solving this question is knowing that every integer **n** greater than 3 can be built using only 2s and 3s. 

With this in mind, we can get an O(n) solution by storing recurring subproblems in an array.

First we establish indices 0, 1 and 2 as base cases in the array. Then, from indices 3 to n, we can set the current array value as:\
`Max(arr[i - 2] * 2, arr[i - 3] * 3)`

Examples:\
table[0] = 1; // base case\
table[1] = 2; // base case\
table[2] = 3; // base case\
table[3] = 4; // Max (table[1] * 2, table[0] * 3)\
table[4] = 6; // Max (table[2] * 2, table[1] * 3)\
table[5] = 9; // Max (table[3] * 2, table[2] * 3)\




 



## Code
```
public int integerBreak(int n) {
        if (n <= 3)
            return n - 1;
        
        int[] table = new int[n];
        
        table[0] = 1;
        table[1] = 2;
        table[2] = 3;
        
        for (int i = 3; i < n; i++)
            table[i] = Math.max(table[i - 2] * 2, table[i - 3] * 3);
        
        
        return table[n - 1];
}
```

