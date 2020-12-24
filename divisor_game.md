回到主题，我们用DP来求解这个问题，首先new一个长度为N+1的数组，dp[i]表示i这个数是否可以赢，如果为true则N=i可以赢，为false则输。

N=1，爱丽丝就肯定会输，所以我们首先让dp[1]=false;

然后我们从i=2开始，一直遍历到i=N

按照题意，我们让j每次从1到i-1的区间里取数，且需要满足

选出任一 x，满足 0 < x < N 且 N % x == 0 。
这个条件，如果发现dp[j]=false，那么dp[i]就一定会赢。


# me 

```text

爱丽丝和鲍勃一起玩游戏，他们轮流行动。爱丽丝先手开局。

最初，黑板上有一个数字 N 。在每个玩家的回合，玩家需要执行以下操作：

选出任一 x，满足 0 < x < N 且 N % x == 0 。
用 N - x 替换黑板上的数字 N 。
如果玩家无法执行这些操作，就会输掉游戏。

只有在爱丽丝在游戏中取得胜利时才返回 True，否则返回 false。假设两个玩家都以最佳状态参与游戏

```
1. dp table 参数说明
dp[i] : 表示i 这个数是否可以赢，如果可以赢的话，就是true,否则就是false
dp[i] = true, i 这个数Alice 可以赢
dp[i] = false, i 这个数Alice 不能赢

2. 动态方程
对于 i （Alice）可以从1-N 取值，那么 j(Bob) 只能从 i-1 中取值X， 并且有个限制条件
(0<X < i) && i % X  == 0 ,在这个条件下，如果BOB 输一次(dp[i]，那么Alice 就会赢dp[i]=true,
最后需要判断DP[N] 是否是true

3. base case 
dp[1] = false
dp[2] = true


```go

package main

func divisorGame(N int) bool {
	var dp = make(map[int]bool)
	dp[0] = false
	dp[1] = false
	dp[2] = true
	for n := 3; n < N; n++ {
		for x := 0; x < n; x++ {
			if n%x == 0 && dp[n-x] == false {
				dp[n] = true
				break
			}
		}
	}
	return dp[N]
}

```