**【第 5 週｜排序與貪心】**

**【UVA 11462 – Age Sort】**

**關鍵字：**
counting sort、frequency array

**核心邏輯：**

* 輸入是一大批年齡資料，但**年齡範圍固定且很小（1～99）**
* 不需要真的排序整個陣列
* 使用「計數排序」：
  + 用陣列記錄每個年齡出現的次數
  + 再依年齡由小到大輸出

**常見錯誤：**

* 使用一般排序（qsort）導致 TLE
* 忘記清空計數陣列
* 輸出格式多一個空白或少空白

**C 骨架：**

while (scanf("%d", &n) == 1 && n != 0) {

int cnt[100] = {0};

for (int i = 0; i < n; i++) {

scanf("%d", &age);

cnt[age]++;

}

for (int a = 1; a <= 99; a++) {

while (cnt[a]--) {

print age a with proper spacing;

}

}

}

**小練習：**

* 改成輸出「出現次數最多的年齡」
* 若年齡範圍改為 1～100000，該怎麼做？

**【UVA 11777 – Automate the Grades】**

**關鍵字：**
sorting、conditional logic

**核心邏輯：**

* 題目給多個成績來源
* 其中三個小考只取「最高的兩個」平均
* 最後加總後依分數區間輸出等第

**常見錯誤：**

* 三個小考沒有先排序就直接取
* 等第區間判斷錯誤（>= 與 > 混用）
* 忘記每筆測資都要輸出 Case 編號

**C 骨架：**

scanf("%d", &T);

for (int tc = 1; tc <= T; tc++) {

int t1, t2, f, a;

int quiz[3];

read inputs;

sort quiz[3];

int quiz\_avg = (quiz[1] + quiz[2]) / 2;

int total = t1 + t2 + f + a + quiz\_avg;

determine grade by total;

print result;

}

**小練習：**

* 改成「取最高三個小考」
* 將等第區間改為由使用者輸入

**【UVA 11369 – Shopaholic】**

**關鍵字：**
greedy、sorting、grouping

**核心邏輯：**

* 題目規則：
  + 每買 3 件商品，第 3 件免費（取最便宜的那件）
* 為了最大化折扣：
  + 先將價格由大到小排序
  + 每 3 件一組，將第 3 件加入折扣

**常見錯誤：**

* 未排序就分組，導致折扣不最大
* 排序方向錯誤（應由大到小）
* 忘記重設折扣總額

**C 骨架：**

scanf("%d", &T);

while (T--) {

scanf("%d", &n);

read price array;

sort price descending;

discount = 0;

for (int i = 2; i < n; i += 3) {

discount += price[i];

}

printf("%d\n", discount);

}

**小練習：**

* 改成「買 4 件，第 4 件免費」
* 若免費的是「最貴的那件」，策略是否改變？

**【UVA 10258 – Contest Scoreboard】**

**關鍵字：**
simulation、struct、custom sort

**核心邏輯：**

* 模擬 ACM 競賽計分板
* 每個隊伍需記錄：
  + 解題數
  + 總罰時
  + 每題是否已解、錯誤次數
* 最後依以下規則排序：
  + 解題數多者優先
  + 罰時少者優先
  + 隊伍編號小者優先

**常見錯誤：**

* 同一題在已解後仍累加罰時
* 未處理「只交過但沒解題」的隊伍
* 排序條件順序錯誤

**C 骨架：**

struct Team {

int solved;

int penalty;

bool submitted;

int wrong[10];

bool solvedProb[10];

};

initialize all teams;

while (read submission) {

update team status;

}

sort teams by:

solved desc,

penalty asc,

team id asc;

print scoreboard;

**小練習：**

* 新增「最後一次 AC 時間」作為排序條件
* 改成即時輸出目前排行榜

**【UVA 10954 – Add All】**

**關鍵字：**
priority queue、greedy、Huffman-like

**核心邏輯：**

* 每次取出「最小的兩個數」相加
* 將和再放回集合中
* 重複直到只剩一個數
* 所有加總成本的總和即為答案

**常見錯誤：**

* 每次重新排序整個陣列，效率太差
* 使用一般陣列導致 TLE
* 忘記在每次合併後累加成本

**C 骨架：**

while (scanf("%d", &n) == 1 && n != 0) {

priority\_queue pq;

for (i = 0; i < n; i++) {

scanf("%d", &x);

push x into pq;

}

long long cost = 0;

while (pq.size() > 1) {

a = pop smallest;

b = pop smallest;

sum = a + b;

cost += sum;

push sum into pq;

}

printf("%lld\n", cost);

}

**小練習：**

* 不使用 priority queue，自行實作 min-heap
* 改成每次取「最小三個數」合併