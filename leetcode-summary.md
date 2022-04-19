# 分类

## 数组

### 双指针

+ 有序数组的题，考虑用双指针。或者任何可以转化为有序集合遍历的问题，考虑用双指针优化（如二分法）

#### 快慢指针

#### 左右指针

##### 1. 二分法

+ 数组中的值并不连续，结果可能在某两个相邻值中间

    + 思路

        判断跳出二分法循环时，结果应如何选取

    + 例题：

        + 275. H 指数 II

            + code

                ```java
                class Solution {
                    public int hIndex(int[] citations) {
                        int len = citations.length;
                        if(len == 1){
                            return citations[0]==0?0:1;
                        }
                        int left=0, right=len-1;
                        int mid = 0;
                        int smallerNum, realSmallerNum;

                        while(left <= right){
                            mid = (left + right)/2;

                            if(len - mid <= citations[mid]){
                                right = mid-1;
                            } else{
                                left = mid+1;
                            }
                        }

                        return len - left;
                    }
                }
                ```

            + 思路：

                + 跳出二分法循环时的状态分析

                    跳出二分法循环时（即刚经历了left==right，此时left==right+1），根据代码导致left==right+1有两种方式：

                    1. `left = mid+1`

                        此时left==right，并且判断`len - mid > citations[mid]`，不包含等于的情况，也就是说结果应在当前索引(left==right)的右侧，采取`left=mid+1`的操作，随后left>right，跳出二分法循环。

                    2. `right = mid-1`

                        此时left==right，并且判断`len - mid <= citations[mid]`，包含等于的情况，也就是说结果应在当前索引(left==right)的左侧或者当前索引就是结果，然后采取`right=mid-1`的操作，随后left>right，跳出二分法循环。

                    此时left==right+1，且结果应在(right,left]。

                    结果不可能是当前right，因为left当前位置要么是0，要么是经过当前right的位置右移才到达left当前的位置，所以right的位置要么越界，要么已经被判断过不满足。

                    之所以结果可能为当前left，是因为right左移经过的数包含了相等的情况，所以依旧有可能。

                + 通过跳出二分法时的状态，分析结果

                    现在知道h在(right,left]区间内，根据题目要求，可知h=len-left。

##### 2. 两数和

有序数组，求两数和

##### 3. 反转数组

不借助额外空间

##### 4. 滑动窗口

+ 窗口扩大、缩小的判断条件

+ 先扩大窗口到满足要求，然后移动窗口（通过从另一侧缩小窗口）

## 动态规划

1. 自顶向下/自底向上


2. 遍历顺序（一维/二维）

    + 正序
    + 倒叙
    + 从中间向两边

3. 动态数组尺寸

    + 是否+1?

4. 状态压缩