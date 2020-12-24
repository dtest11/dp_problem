```go


// 卖股票， 只能进行一次交易， 先买入 后卖出
func maxProfit(prices []int) int {
	var dp = make([][][]int, len(prices)) // [i][J][K] 第I 天，持有K个股票,至今最多进行了J 次交易
	// p[2][3][0] 的含义：今天是第二天，我现在手上没有持有股票，至今最多进行 3 次交易
	// 动态转移方程
	for I := 0; I < len(prices); I++ {
		for J := 1; J < 2; J++ {
			for K := 0; K <= 1; K++ {
				dp[I][J][K] = 0
			}
		}
	}
	// base case
	//dp[-1][1][0] = 0//
	//dp[-1][1][1] = math.MinInt64
	// dp[i][0][0] = 0         // 解释：因为 k 是从 1 开始的，所以 k = 0 意味着根本不允许交易，这时候利润当然是 0 。
	// dp[i][0][1] = -infinity // 解释：不允许交易的情况下，是不可能持有股票的，用负无穷表示这种不可能。
	// 对于这个题目J = 1， 持有一个股票

	for I := 0; I < len(prices); I++ {
		if I-1 == -1 {
			dp[I][1][1] = -prices[I]
		}
		dp[I][1][0] = MAX(dp[I-1][1][0], dp[I-1][1][1]+prices[I]) // 今天手里没有股票
		dp[I][1][1] = MAX(dp[I-1][1][1], dp[I-1][1][0]-prices[I]) // 今天手里股票
	}
	// 最后的结果就是 dp[I-1][K][0]
	I := len(prices)
	return dp[I-1][1][0]
}


```