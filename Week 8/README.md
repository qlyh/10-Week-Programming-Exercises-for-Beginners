**【第 8 週｜遞迴與回溯】**

本週核心概念：
**用遞迴描述狀態空間，並用回溯（backtracking）枚舉所有可能解**。
重點在於：**狀態定義、終止條件、以及「做—遞迴—還原」的流程**。

**【UVA 750 – 8 Queens Chess Problem】**

**關鍵字：**
backtracking、constraint checking、8 queens

**核心邏輯：**

* 在 8×8 棋盤上放 8 個皇后
* 任兩個皇后不可在同一列、同一行或同一對角線
* 題目通常固定某一列的皇后位置
* 使用回溯：
  + 一列一列嘗試放皇后
  + 每次放置前檢查是否衝突
  + 若衝突則回退

**常見錯誤：**

* 對角線衝突判斷錯誤
* 忘記在回溯時「還原狀態」
* 列印結果格式不符合題目要求

**C 骨架：**

int col[9];

bool usedCol[9], diag1[20], diag2[20];

void dfs(int r) {

if (r == 9) {

print solution;

return;

}

for (int c = 1; c <= 8; c++) {

if (!usedCol[c] && !diag1[r+c] && !diag2[r-c+8]) {

mark used;

col[r] = c;

dfs(r + 1);

unmark used;

}

}

}

**小練習：**

* 改成 N-Queens（N 由輸入給定）
* 計算解的總數而不列印所有解

**【UVA 10344 – 23 Out of 5】**

**關鍵字：**
permutation、recursion、expression evaluation

**核心邏輯：**

* 給 5 個整數
* 需排列這 5 個數，並在中間插入 + - \*
* 只要有任一組運算結果為 23，即輸出 Possible
* 解題分成兩層回溯：
  1. 枚舉數字排列
  2. 枚舉運算子組合

**常見錯誤：**

* 只排列數字，忘記運算子也要嘗試
* 運算順序錯誤（必須依題目規定由左到右）
* 使用浮點數導致誤差

**C 骨架：**

bool used[5];

bool dfs(int depth, int value) {

if (depth == 5)

return value == 23;

for (int i = 0; i < 5; i++) {

if (!used[i]) {

used[i] = true;

if (dfs(depth+1, value + a[i]) ||

dfs(depth+1, value - a[i]) ||

dfs(depth+1, value \* a[i]))

return true;

used[i] = false;

}

}

return false;

}

**小練習：**

* 改成目標值由使用者輸入
* 新增除法運算（需注意整除）

**【UVA 10018 – Reverse and Add】**

**關鍵字：**
recursion/iteration、palindrome、string number

**核心邏輯：**

* 對一個數字做以下操作：
  1. 將數字反轉
  2. 與原數相加
* 重複直到得到回文數
* 輸出操作次數與最終回文數

**常見錯誤：**

* 使用 int 導致溢位
* 回文判斷錯誤
* 未正確計算步數

**C 骨架：**

while (scanf("%s", s) == 1) {

count = 0;

while (!isPalindrome(s)) {

reverse s to r;

s = addStrings(s, r);

count++;

}

print count and s;

}

**小練習：**

* 限制最多執行 1000 次
* 改成只用整數（觀察 overflow 風險）

**【UVA 10918 – Tri Tiling】**

**關鍵字：**
dynamic programming、recurrence、tiling

**核心邏輯：**

* 題目計算用 2×1 骨牌鋪滿 2×n 的方法數
* 只有 n 為偶數時才有解
* 使用 DP：
  + dp[n] 表示鋪滿 2×n 的方法數
* 利用遞推關係逐步計算

**常見錯誤：**

* 對奇數 n 仍嘗試計算
* DP 初始條件設錯
* 使用遞迴導致 TLE

**C 骨架：**

dp[0] = 1;

dp[2] = 3;

for (int i = 4; i <= maxN; i += 2) {

dp[i] = 3 \* dp[i-2];

for (int j = i-4; j >= 0; j -= 2) {

dp[i] += 2 \* dp[j];

}

}

**小練習：**

* 推導並寫出 dp 的遞推式證明
* 改成只計算 dp[n]（不預算整表）

**【UVA 291 – The House Of Santa Claus】**

**關鍵字：**
graph traversal、DFS、edge marking

**核心邏輯：**

* 題目給一張固定的小圖
* 需要列舉「走過每一條邊一次且僅一次」的所有路徑
* 使用 DFS 回溯：
  + 每條邊只能走一次
  + 走完後需標記為未使用以便回溯

**常見錯誤：**

* 使用節點標記而非邊標記
* 忘記回溯時解除標記
* 路徑輸出順序錯誤

**C 骨架：**

int path[10];

bool usedEdge[20];

void dfs(int node, int depth) {

if (depth == totalEdges) {

print path;

return;

}

for each edge e from node {

if (!usedEdge[e]) {

usedEdge[e] = true;

path[depth] = nextNode;

dfs(nextNode, depth + 1);

usedEdge[e] = false;

}

}

}

**小練習：**

* 改成只輸出路徑數量
* 將圖改成由輸入給定