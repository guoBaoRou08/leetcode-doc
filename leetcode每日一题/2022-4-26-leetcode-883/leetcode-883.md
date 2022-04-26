**每日一题**

#### [883. 三维形体投影面积](https://leetcode-cn.com/problems/projection-area-of-3d-shapes/)

难度简单86收藏分享切换为英文接收动态反馈

在 `n x n` 的网格 `grid` 中，我们放置了一些与 x，y，z 三轴对齐的 `1 x 1 x 1` 立方体。

每个值 `v = grid[i][j]` 表示 `v` 个正方体叠放在单元格 `(i, j)` 上。

现在，我们查看这些立方体在 `xy` 、`yz` 和 `zx` 平面上的*投影*。

**投影** 就像影子，将 **三维** 形体映射到一个 **二维** 平面上。从顶部、前面和侧面看立方体时，我们会看到“影子”。

返回 *所有三个投影的总面积* 。



**示例 1：**

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/08/02/shadow.png)

```
输入：[[1,2],[3,4]]
输出：17
解释：这里有该形体在三个轴对齐平面上的三个投影(“阴影部分”)。
```

**示例 2:**

```
输入：grid = [[2]]
输出：5
```

**示例 3：**

```
输入：[[1,0],[0,2]]
输出：8
```

 

**提示：**

- `n == grid.length == grid[i].length`
- `1 <= n <= 50`
- `0 <= grid[i][j] <= 50`

**题干截图**
![输入图片说明](%E5%9B%BE%E7%89%87/%E6%AF%8F%E6%97%A5%E4%B8%80%E9%A2%981.png)

![输入图片说明](%E5%9B%BE%E7%89%87/%E6%AF%8F%E6%97%A5%E4%B8%80%E9%A2%982.png)


**代码分析**


思路与算法

根据题意，x 轴对应行，y 轴对应列，z 轴对应网格的数值。

因此：

1. xy 平面的投影面积等于网格上非零数值的数目；

2. yz 平面的投影面积等于网格上每一列最大数值之和；
3. zx 平面的投影面积等于网格上每一行最大数值之和。

返回上述三个投影面积之和。

![输入图片说明](%E5%9B%BE%E7%89%87/%E5%88%86%E6%9E%90%E8%A7%A3%E5%9B%BE.png)

**代码截图**

![输入图片说明](%E5%9B%BE%E7%89%87/%E4%BB%A3%E7%A0%81%E6%88%AA%E5%9B%BE.png)

![输入图片说明](%E5%9B%BE%E7%89%87/%E4%BB%A3%E7%A0%81%E8%A7%A3%E5%9B%BE1.png)
**解题源码**

`

```
package leetcode.editor.cn;

import java.util.Arrays;

//Java：三维形体投影面积
 class P883ProjectionAreaOf3dShapes{
    public static void main(String[] args) {
        Solution solution = new P883ProjectionAreaOf3dShapes().new Solution();
        int [ ][ ]  arr2 = {{3,2,2},{2,1,2},{2,2,2}};
        System.out.println("输入：" );
        for(int i = 0; i < arr2.length; i++) {
            for(int j = 0; j < arr2[i].length; j++) {
                System.out.print(arr2[i][j] + " ");
            }
            System.out.println();
        }
        System.out.println("\n");
        int num = solution.projectionArea(arr2);
        System.out.println("\n");
        System.out.println("输出：" + num);
        // TO TEST
    }
    //leetcode submit region begin(Prohibit modification and deletion)
    class Solution {
        public int projectionArea(int[][] grid) {
            //获得二维数组长度
            int n = grid.length;
            //初始化表面积
            int xyArea = 0, yzArea = 0, zxArea = 0;
            //因为是正方体两次循环长度都相等
            for (int i = 0; i < n; i++) {
                //初始化想向量yz高度，向量xz高度
                int yzHeight = 0, zxHeight = 0;
                //遍历每个一维数组长度，获得这个点在三维空间高度
                for (int j = 0; j < n; j++) {
                    //上表面积为每个不为0得坐标个数，不为0 就+1，为0加0
                    xyArea += grid[i][j] > 0 ? 1 : 0;
                    //向量yz高度为y列每一个列得最大值
                    yzHeight = Math.max(yzHeight, grid[i][j]);
                    //向量xz高度为x行每一个行得最大值
                    zxHeight = Math.max(zxHeight, grid[j][i]);
                }
                //行列累加
                yzArea += yzHeight;
                zxArea += zxHeight;
            }


            return xyArea + yzArea + zxArea;//返回总数

        }
    }

//leetcode submit region end(Prohibit modification and deletion)

}
```



`

**输出结果**

![输入图片说明](%E5%9B%BE%E7%89%87/%E6%B5%8B%E8%AF%95%E7%94%A8%E4%BE%8B.png)


**官方测试**


![输入图片说明](%E5%9B%BE%E7%89%87/%E5%AE%98%E6%96%B9%E6%B5%8B%E8%AF%95.png)
