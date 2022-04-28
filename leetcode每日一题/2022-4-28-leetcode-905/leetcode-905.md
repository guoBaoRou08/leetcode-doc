**每日一题**

- - [905. 按奇偶排序数组](https://leetcode-cn.com/problems/sort-array-by-parity/)

    难度简单248收藏分享切换为英文接收动态反馈

    给你一个整数数组 `nums`，将 `nums` 中的的所有偶数元素移动到数组的前面，后跟所有奇数元素。

    返回满足此条件的 **任一数组** 作为答案。

     

    **示例 1：**

    ```
    输入：nums = [3,1,2,4]
    输出：[2,4,3,1]
    解释：[4,2,3,1]、[2,4,1,3] 和 [4,2,1,3] 也会被视作正确答案。
    ```

    **示例 2：**
  
    ```
    输入：nums = [0]
    输出：[0]
    ```

     
  
    **提示：**
  
    - `1 <= nums.length <= 5000`
    - `0 <= nums[i] <= 5000`

**题干截图**



**代码分析**



思路与算法

详细见代码注释。

主要是运用双指针

给出两种指针分析：

1. 双指针，遇到奇数加到数组后边，偶数加到数组前边
2. 运用追击左右交换，原地交换数值。



**代码截图**



**解题源码**

`

```
package leetcode.editor.cn;

import java.util.Arrays;


//Java：按奇偶排序数组
 class P905SortArrayByParity{
    public static void main(String[] args) {
        Solution solution = new P905SortArrayByParity().new Solution();
        // TO TEST
        int [ ]  arr = {3,2,2,0,85,3,1,7,5,8,88,3};
        System.out.println("输入："+Arrays.toString(arr));
        System.out.println("输出（双指针，遇到奇数加到数组前边，偶数加到数组后边）：\n"+ Arrays.toString(solution.sortArrayByParity(arr)));
        System.out.println("输出（双指针原地修改：）：\n"+ Arrays.toString(solution.sortArrayByParity2(arr)));
    }
    //leetcode submit region begin(Prohibit modification and deletion)
    class Solution {
        public int[] sortArrayByParity2(int[] nums) {
            //数组长度
            int arrLen = nums.length;
            int[] res = new int[arrLen];
            int left = 0, right = arrLen - 1;//左面位置，右面开始位置
            //循环遍历
            for(int i = 0; i <arrLen;++i){
                //判断奇偶性
                if (nums[i] % 2 == 0) {
                    //为偶数则放到前面
                    res[left] = nums[i];
                    //左面计数加1
                    left++;
                } else {
                    //为奇数则放到后面
                    res[right] = nums[i];
                    //右面计数减1
                    right--;
                }
            }
            //返回数组
            return res;
        }

        public int[] sortArrayByParity(int[] nums) {
            //初始左位置，右位置
            int intiLoc = 0,arrLen = nums.length - 1;
            //判断两指针是否相遇或已经相遇过了
            while( intiLoc<arrLen ){
                //循环判断初始指针指向的数是否是偶数
                while(intiLoc < nums.length && nums[intiLoc] % 2 == 0)
                    //偶数则位置指针向右移动
                    intiLoc++;
                //循环判断末尾指针指向的数是否是奇数
                while(arrLen >= 0 && nums[arrLen] % 2 == 1)
                    //奇数则位置指针向左移动
                    arrLen--;
                //两者还未相遇则进入判断
                if( intiLoc<arrLen ){
                    //交换奇偶数字，前面已经判断到这里必要交换
                    nums[intiLoc] += nums[arrLen];
                    nums[arrLen] = nums[intiLoc] - nums[arrLen];
                    nums[intiLoc] -=  nums[arrLen];
                }
                //整体向相遇移动
                intiLoc++;
                arrLen--;
            }
            //返回结果
            return nums;
        }
    }


//leetcode submit region end(Prohibit modification and deletion)

}
```



`

**输出结果**



**官方测试**



