# MasterDP
Master dynamic programming from beginner to Advance

# 🚀 Dynamic Programming Training Workbook (Java + Problems)

Welcome to the **Dynamic Programming (DP) Roadmap**!  
This repo is a step-by-step guide to mastering DP — from basics to contest-hard problems — with **Java pseudocode templates + curated practice problems**.

---

## 📑 Table of Contents
1. [1D DP (Linear DP)](#-1d-dp-linear-dp)
2. [2D DP (Matrix & Subsequence DP)](#-2d-dp-matrix--subsequence-dp)
3. [Knapsack Variants](#-knapsack-variants)
4. [Interval DP](#-interval-dp)
5. [Digit DP](#-digit-dp)
6. [Bitmask DP](#-bitmask-dp)
7. [Tree DP](#-tree-dp)
8. [Advanced DP Optimizations](#-advanced-dp-optimizations)
9. [Training Strategy](#-training-strategy)

---

## 🧩 1D DP (Linear DP)

👉 Based on arrays, strings, or single index states.  
**Key Idea**: Break into smaller subproblems and reuse results.

### 🔑 Common Problems
- Fibonacci  
- Climbing Stairs  
- Min/Max Cost Path  

### 📜 Pseudocode
```java
// Top-down (Memoization)
int[] dp;
int fib(int n) {
    if (n <= 1) return n;
    if (dp[n] != -1) return dp[n];
    return dp[n] = fib(n-1) + fib(n-2);
}

// Bottom-up (Tabulation)
int fibBU(int n) {
    int[] dp = new int[n+1];
    dp[0] = 0; dp[1] = 1;
    for (int i=2; i<=n; i++)
        dp[i] = dp[i-1] + dp[i-2];
    return dp[n];
}


```


###🎯 Practice

LeetCode 70 – Climbing Stairs🟢

LeetCode 198 – House Robber🟡

CSES – Dice Combinations🟡

AtCoder DP A – Frog 1🟡

Codeforces 550A – Two Substrings 🔴

###🧩 2D DP (Matrix & Subsequence DP)

👉 When the state depends on two indices.
Common: Grid paths, subsequences, substrings.

###📜 Pseudocode
// Example: Unique Paths
```java
int uniquePaths(int m, int n) {
    int[][] dp = new int[m][n];
    for (int i=0; i<m; i++) dp[i][0] = 1;
    for (int j=0; j<n; j++) dp[0][j] = 1;

    for (int i=1; i<m; i++)
        for (int j=1; j<n; j++)
            dp[i][j] = dp[i-1][j] + dp[i][j-1];
    return dp[m-1][n-1];
}
```
###🎯 Practice

LeetCode 62 – Unique Paths🟢
LeetCode 1143 – Longest Common Subsequence🟡
AtCoder DP B – Frog 2🟡
CSES – Grid Paths🟡
LeetCode 72 – Edit Distance🔴

###🎒 Knapsack Variants

👉 Central to DP contests.

0/1 Knapsack (take/don’t take)

Unbounded Knapsack (take unlimited)

Subset Sum, Coin Change

###📜 Pseudocode (0/1 Knapsack)
```java
int knapsack(int[] wt, int[] val, int W) {
    int n = wt.length;
    int[][] dp = new int[n+1][W+1];
    for (int i=1; i<=n; i++) {
        for (int w=0; w<=W; w++) {
            dp[i][w] = dp[i-1][w];
            if (wt[i-1] <= w)
                dp[i][w] = Math.max(dp[i][w], val[i-1] + dp[i-1][w - wt[i-1]]);
        }
    }
    return dp[n][W];
}
```

###🎯 Practice

LeetCode 416 – Partition Equal Subset Sum 🟡
LeetCode 518 – Coin Change II 🟡
AtCoder DP D – Knapsack 1 🟡
CSES – Money Sums 🔴
Codeforces 1288C – Two Arrays 🔴

###📐 Interval DP

👉 Subproblems defined on intervals [l, r].
Common: Matrix Chain Multiplication, Palindrome Partitioning.

📜 Pseudocode
```java
// Matrix Chain Multiplication
int[][] dp;
int mcm(int[] arr, int i, int j) {
    if (i == j) return 0;
    if (dp[i][j] != -1) return dp[i][j];
    int ans = Integer.MAX_VALUE;
    for (int k=i; k<j; k++) {
        int cost = mcm(arr, i, k) + mcm(arr, k+1, j) + arr[i-1]*arr[k]*arr[j];
        ans = Math.min(ans, cost);
    }
    return dp[i][j] = ans;
}
```

###🎯 Practice

LeetCode 132 – Palindrome Partitioning II🟡🔴
LeetCode 312 – Burst Balloons🔴
AtCoder DP N – Slimes🟡🔴
Codeforces 607A – Chain Reaction🔴

###🔢 Digit DP

👉 Count numbers under digit constraints.
State: (pos, tight, sum, …)

📜 Pseudocode
```java
int[][][] dp;
int solve(String num, int pos, int tight, int sum) {
    if (pos == num.length()) return sum >= 0 ? 1 : 0;
    if (dp[pos][tight][sum] != -1) return dp[pos][tight][sum];
    int limit = (tight==1) ? (num.charAt(pos)-'0') : 9;
    int res = 0;
    for (int d=0; d<=limit; d++)
        res += solve(num, pos+1, (tight==1 && d==limit)?1:0, sum-d);
    return dp[pos][tight][sum] = res;
}

```
###🎯 Practice

LeetCode 1012 – Numbers With Repeated Digits 🔴
Codeforces 1036C – Classy Numbers 🔴
CSES – Counting Numbers 🔴

###🎭 Bitmask DP

👉 DP over subsets.
Common: Traveling Salesman, Assignment problems.

📜 Pseudocode
```java
// Assignment Problem
int[][] cost;
int[] dp;
int solve(int mask) {
    int n = cost.length;
    if (mask == (1<<n)-1) return 0;
    if (dp[mask] != -1) return dp[mask];
    int ans = Integer.MAX_VALUE;
    int k = Integer.bitCount(mask);
    for (int j=0; j<n; j++) {
        if ((mask & (1<<j)) == 0)
            ans = Math.min(ans, cost[k][j] + solve(mask | (1<<j)));
    }
    return dp[mask] = ans;
}
```

###🎯 Practice

LeetCode 698 – Partition to K Equal Sum Subsets 🟡🔴
AtCoder DP O – Matching 🟡🔴
CSES – Traveling Salesman Problem 🔴
Codeforces 1184C2 – Heidi and the Turing Test 🔴

###🌳 Tree DP

👉 State defined over a tree’s nodes.
Common: Subtree sizes, DP on children.

📜 Pseudocode
```java
ArrayList<Integer>[] g;
int[] dp;

void dfs(int u, int p) {
    dp[u] = 1;
    for (int v : g[u]) {
        if (v == p) continue;
        dfs(v, u);
        dp[u] += dp[v]; // example: subtree size
    }
}
```


###🎯 Practice

AtCoder DP P – Independent Set 🟡
CSES – Tree Distances I 🟡🔴
CSES – Tree Distances II 🔴
Codeforces 600E – Lomsat gelral 🔴

###⚡ Advanced DP Optimizations

👉 For contest-hard problems:

Divide & Conquer DP

Convex Hull Trick (Slope Optimization)

DP + Segment Tree / BIT

###📌 Sources:

Codeforces EDU DP Optimization Course

AtCoder DP W/X/Y/Z

###🎯 Training Strategy

Start with basics → 1D DP + 2D DP (Climbing Stairs, LCS).

Master Knapsack → subset sum, coin change, bounded/unbounded.

Move to Interval DP (Palindrome Partitioning, Slimes).

Add Bitmask & Tree DP for contest-level practice.

Finally explore Digit DP + Advanced Optimizations.
