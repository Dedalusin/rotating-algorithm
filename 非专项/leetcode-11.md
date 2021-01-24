题目:
> 给你 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0) 。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。
  
个人题解:
```java
 public int maxArea(int[] height) {
        int[] dp = new int[height.length];
        if (height.length < 2) return 0;
        dp[0] = 0;
        dp[1] = Math.min(height[0], height[1]);
        for (int i = 2; i < height.length; i++){
            if (height[i] == 0) {
                dp[i] = dp[i-1];
                continue;
            }
            int delta = i - dp[i-1]/height[i];
            if (delta <= 0) dp[i] = dp[i-1];
            for (int j = 0; j < delta; j++){
                int state = (i - j) * Math.min(height[i], height[j]);
                dp[i] = Math.max(dp[i-1], Math.max(state, dp[i]));
            }
        }
        return dp[dp.length - 1];
    }
```
这里我主要是朝着对于O(n^2)的暴力算法进行优化，结果应该是O(n) ~ O(n^2)之间
  
在官方题解中，使用了双指针，p1 = 0 ,p2 = length-1相向移动，很明显，由于移动大的那个指针，每次移动的结果必然会减小或者不变，方向错误，所以每次移动指针为两者小的那个。
O(n)即可得到结果。
