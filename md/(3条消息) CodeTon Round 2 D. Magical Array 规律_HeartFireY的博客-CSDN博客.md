> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/yanweiqi1754989931/article/details/126098144)

题目分析
----

给定 n n n个初始值相同的数组，共有两种操作：

*   操作 1 1 1：选择一对 ( i , j ) (i, j) (i,j)， a [ i − 1 ] a[i - 1] a[i−1]加 1 1 1， a [ i ] a[i] a[i]减去 1 1 1， a [ j ] a[j] a[j]减去 1 1 1， a [ j + 1 ] a[j + 1] a[j+1]加 1 1 1。
*   操作 2 2 2：选择一对 ( i , j ) (i, j) (i,j)， a [ i − 1 ] a[i - 1] a[i−1]加 1 1 1， a [ i ] a[i] a[i]减去 1 1 1， a [ j ] a[j] a[j]减去 1 1 1， a [ j + 2 ] a[j + 2] a[j+2]加 1 1 1。

只有一个数组被执行了若干次 2 2 2操作，问哪个数组被执行了操作 2 2 2，操作了多少次

令 s [ ] s[] s[]表示数组 a [ ] a[] a[]的前缀和，我们对两个操作在前缀和上进行分析：

*   操作 1 1 1：剥离未收到影响的区间： [ 1 , i − 2 ] , [ i + 1 , j − 1 ] , [ j + 2 , n ] [1, i - 2],[i+ 1, j - 1], [j + 2, n] [1,i−2],[i+1,j−1],[j+2,n]，我们将数组和表示为前缀分段和加和式：  
    s [ i − 2 ] + ( s [ j − 1 ] − s [ i ] ) + ( s [ n ] − s [ j + 1 ] ) + a [ i − 1 ] + a [ i ] + a [ j ] + a [ j + 1 ] s[i - 2] + (s[j - 1] - s[i]) + (s[n] - s[j + 1]) + a[i - 1] + a[i] + a[j] + a[j + 1] s[i−2]+(s[j−1]−s[i])+(s[n]−s[j+1])+a[i−1]+a[i]+a[j]+a[j+1]  
    经过 1 1 1次操作后：因为受影响元素连续，因此前缀和元素受到 − 1 -1 −1影响后立即受到 + 1 +1 +1影响，不变  
    s [ i − 2 ] + ( s [ j − 1 ] − s [ i ] ) + ( s [ n ] − s [ j + 1 ] ) + ( a [ i − 1 ] + 1 ) + ( a [ i ] − 1 ) + ( a [ j ] − 1 ) + ( a [ j + 1 ] + 1 ) s[i - 2] + (s[j - 1] - s[i]) + (s[n] - s[j + 1]) + (a[i - 1] + 1) + (a[i] - 1) + (a[j] - 1) + (a[j + 1] + 1) s[i−2]+(s[j−1]−s[i])+(s[n]−s[j+1])+(a[i−1]+1)+(a[i]−1)+(a[j]−1)+(a[j+1]+1)  
    发现前缀和数组总和不受影响
    
*   操作 2 2 2：同上，先写出加和式：  
    s [ i − 2 ] + ( s [ j − 1 ] − s [ i ] ) + ( s [ n ] − s [ j + 2 ] ) + ( s [ j + 1 ] − s [ j ] ) + a [ i − 1 ] + a [ i ] + a [ j ] + a [ j + 2 ] s[i - 2] + (s[j - 1] - s[i]) + (s[n] - s[j + 2]) + (s[j + 1] - s[j]) + a[i - 1] + a[i] + a[j] + a[j + 2] s[i−2]+(s[j−1]−s[i])+(s[n]−s[j+2])+(s[j+1]−s[j])+a[i−1]+a[i]+a[j]+a[j+2]  
    经过 1 1 1次操作后，我们先分析收到影响的元素： a [ i − 1 ] , a [ i ] , a [ j ] , a [ j + 2 ] a[i - 1], a[i], a[j], a[j + 2] a[i−1],a[i],a[j],a[j+2]，但发现由于受影响的元素不连续，因此 s [ j + 1 ] , s [ j + 2 ] s[j + 1], s[j + 2] s[j+1],s[j+2]会受影响，但收到的影响在 a [ j + 2 ] a[j + 2] a[j+2]处抵消，也就是 s [ j + 2 ] s[j + 2] s[j+2]上的 − 1 -1 −1影响被消除。那么：  
    s [ i − 2 ] + ( s [ j − 1 ] − s [ i ] ) + ( s [ n ] − s [ j + 2 ] ) + ( ( s [ j + 1 ] − 1 ) − s [ j ] ) + ( a [ i − 1 ] + 1 ) + ( a [ i ] − 1 ) + ( a [ j ] − 1 ) + ( a [ j + 1 ] + 1 ) s[i - 2] + (s[j - 1] - s[i]) + (s[n] - s[j + 2]) + ((s[j + 1] - 1) - s[j]) + (a[i - 1] + 1) + (a[i] - 1) + (a[j] - 1) + (a[j + 1] + 1) s[i−2]+(s[j−1]−s[i])+(s[n]−s[j+2])+((s[j+1]−1)−s[j])+(a[i−1]+1)+(a[i]−1)+(a[j]−1)+(a[j+1]+1)  
    发现前缀和数组总和被 − 1 -1 −1。
    
*   操作 2 2 2对总和的影响，我们可以从式子的角度分析：  
    ∑ i = 1 n ∑ j = 1 i a [ j ] \sum^{n}_{i = 1}\sum^{i}_{j = 1} a[j] i=1∑n​j=1∑i​a[j]  
    对 a [ x ] a[x] a[x]元素 + 1 +1 +1， a [ x + 1 ] − 1 a[x + 1] - 1 a[x+1]−1  
    ∑ i = 1 x − 1 ∑ j = 1 i a [ j ] + ∑ i = x x ∑ j = 1 i a [ j ] + ∑ i = x n 1 + ∑ i = x + 1 n ∑ j = 1 i a [ j ] − ∑ i = x + 1 n 1 = ( ∑ i = 1 n ∑ j = 1 i a [ j ] ) + 1 \sum_{i = 1}^{x - 1}\sum_{j = 1}^{i}a[j] + \sum_{i = x}^{x}\sum_{j = 1}^{i}a[j] + \sum_{i = x}^{n}1 + \sum_{i = x + 1}^{n}\sum_{j = 1}^{i}a[j] - \sum_{i = x + 1}^{n}1 = (\sum^{n}_{i = 1}\sum^{i}_{j = 1} a[j]) + 1 i=1∑x−1​j=1∑i​a[j]+i=x∑x​j=1∑i​a[j]+i=x∑n​1+i=x+1∑n​j=1∑i​a[j]−i=x+1∑n​1=(i=1∑n​j=1∑i​a[j])+1  
    再分析 a [ y ] − 1 a[y]-1 a[y]−1, a [ x + 2 ] a[x + 2] a[x+2]元素 + 1 +1 +1:  
    ∑ i = 1 x − 1 ∑ j = 1 i a [ j ] + ∑ i = x x ∑ j = 1 i a [ j ] − ∑ i = x n 1 + ∑ i = x + 1 n ∑ j = 1 i a [ j ] + ∑ i = x + 2 n 1 = ( ∑ i = 1 n ∑ j = 1 i a [ j ] ) − 2 \sum_{i = 1}^{x - 1}\sum_{j = 1}^{i}a[j] + \sum_{i = x}^{x}\sum_{j = 1}^{i}a[j] - \sum_{i = x}^{n}1 + \sum_{i = x + 1}^{n}\sum_{j = 1}^{i}a[j] + \sum_{i = x + 2}^{n}1 = (\sum^{n}_{i = 1}\sum^{i}_{j = 1} a[j]) - 2 i=1∑x−1​j=1∑i​a[j]+i=x∑x​j=1∑i​a[j]−i=x∑n​1+i=x+1∑n​j=1∑i​a[j]+i=x+2∑n​1=(i=1∑n​j=1∑i​a[j])−2  
    发现影响为： − 1 -1 −1。那么根据以上结论，可以找出被影响的数组及操作次数。
    
    同理，操作一影响为 0 0 0。
    
    Code
    ----
    
    ```
    `#include <bits/stdc++.h>
    #pragma gcc optimize("O2")
    #pragma g++ optimize("O2")
    #define int long long
    #define endl '\n'
    using namespace std;
    
    const int N = 1e6 + 10;
    
    int flag[N];
    
    inline void solve(){
        int n, m; cin >> n >> m;
        memset(flag, 0, (n + 5) * sizeof(int));
        int **a = (int **)malloc((n + 2) * sizeof(int**));
        int i, j;
        for (i = 0; i <= n; i++) {
            a[i] = (int*)malloc((m + 2) * sizeof(int));
        }
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++) cin >> a[i][j];
        }
        for(int i = 1; i < m; i++){
            int minn = *min_element(a[j] + 1, a[j] + 1 + n);
            for(int j = 1; j <= n; j++){
                flag[j] += (a[j][i] -= minn);
                a[j][i + 1] += a[j][i];
            } 
        }
        int pos = 1;
        for(int i = 2; i <= n; i++)
            if(flag[pos] > flag[i]) pos = i;
        if(pos == 1) cout << pos << ' ' << flag[2] - flag[1] << endl;
        else cout << pos << ' ' << flag[1] - flag[pos] << endl;
    }
    
    signed main(){
        ios_base::sync_with_stdio(false), cin.tie(0);
        int t = 1; cin >> t;
        while(t--) solve();
        return 0;
    }` ![](https://csdnimg.cn/release/blogv2/dist/pc/img/newCodeMoreWhite.png)
    
    *   1
    *   2
    *   3
    *   4
    *   5
    *   6
    *   7
    *   8
    *   9
    *   10
    *   11
    *   12
    *   13
    *   14
    *   15
    *   16
    *   17
    *   18
    *   19
    *   20
    *   21
    *   22
    *   23
    *   24
    *   25
    *   26
    *   27
    *   28
    *   29
    *   30
    *   31
    *   32
    *   33
    *   34
    *   35
    *   36
    *   37
    *   38
    *   39
    *   40
    *   41
    *   42
    
    
    ```