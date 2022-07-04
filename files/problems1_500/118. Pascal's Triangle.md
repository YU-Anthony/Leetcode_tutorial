## Question
Given an integer numRows, return the first numRows of Pascal's triangle.
In Pascal's triangle, each number is the sum of the two numbers directly above it as shown:

![](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

## Example
```bash
Input: numRows = 5
Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```
```bash
Input: numRows = 1
Output: [[1]]
```
## Solution
Actually, the description has given us the key to solve this question: **each number is the sum of the two numbers directly above it as shown**. Given x<sub>{i,j}</sub> as an example, you only need to get the sum of x<sub>{i-1,j}</sub> and x<sub>{x-1,j-1}</sub>. One thing should be note here is the determination of the first and last element of each row and assigns a value of 1.

```python
class Solution:
    def generate(self, numRows):
        res = []
        for i in range(numRows):
            row = []
            for j in range(0,i+1):
                if j == 0 or j ==i:
                    row.append(1)
                else:
                    row.append(res[i-1][j]+res[i-1][j-1])
            res.append(row)
        return res

```