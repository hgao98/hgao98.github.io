# 题

## 1846. 减小和重新排列数组后的最大元素

+ 法一

    + 思路

        + 理想情况是，数组升序排列后进行修改，第一个数为1，后面每个数比前一个数大1，最终最大值与数组长度相等。

        + 特殊情况，原数组升序排列后，某处索引index处（index从0开始）的值不能达到(index+1)，也就是arr[index] < index+1，计算其差值的绝对值

        + 统计所有不能达到(index+1)的差值绝对值，求max，即为最终数组最大值与理想最大值（即数组长度）的差值。

    + code

        ```java
        class Solution {
            public int maximumElementAfterDecrementingAndRearranging(int[] arr) {
                int len = arr.length;
                Arrays.sort(arr);
                int maxDiff = 0;
                for(int i=0; i<len; i++){
                    if(arr[i] < i+1){
                        maxDiff = Math.max(maxDiff, i + 1 - arr[i]);
                    }
                }

                return len-maxDiff;
            }
        }
        ```

+ 法二[官方：排序 + 贪心]

    + [思路](https://leetcode-cn.com/problems/maximum-element-after-decreasing-and-rearranging/solution/jian-xiao-he-zhong-xin-pai-lie-shu-zu-ho-mzee/)

    + code

        ```java
        class Solution {
        public:
            int maximumElementAfterDecrementingAndRearranging(vector<int> &arr) {
                int n = arr.size();
                sort(arr.begin(), arr.end());
                arr[0] = 1;
                for (int i = 1; i < n; ++i) {
                    arr[i] = min(arr[i], arr[i - 1] + 1);
                }
                return arr.back();
            }
        };
        ```