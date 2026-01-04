**【第 9 週｜模擬與綜合應用】**

本週核心概念：
**把前面學過的條件判斷、字串、排序、資料結構整合在一起做完整模擬**。
重點在於：**讀題拆規則、正確記錄狀態、依規則做比較與輸出**。

**【UVA 10141 – Request for Proposal】**

**關鍵字：**
simulation、multi-criteria selection、string handling

**核心邏輯：**

* 題目給多個 proposal，每個 proposal 有：
  + 價格
  + 滿足需求數量（compliance）
* 選擇規則為：
  + **滿足需求數量最多者優先**
  + 若相同，**價格較低者優先**
* 實作時：
  + 不需要存下所有 proposal
  + 只需在讀入時維護「目前最佳 proposal」

**常見錯誤：**

* 沒有正確跳過需求描述行
* 比較順序顛倒（先比價格再比需求）
* 忘記處理多組測資與輸出空行格式

**C 骨架：**

```c
int caseNum = 1;

while (read n and p, not both zero) {
  Skip n requirement lines;
  bestCompliance = -1;
  bestPrice = INF;

  for each proposal:
    Read name, price, and compliance;
    Skip compliance lines;

    if (compliance > bestCompliance || (compliance == bestCompliance && price < bestPrice)) {
      Update best proposal;
    }
  Print case header and best proposal name;
}
```

**小練習：**

* 新增第三順位條件（例如：名字字典序）
* 輸出所有與最佳 proposal 同等級的選項

**【UVA 10905 – Children's Game】**

**關鍵字：**
custom sort、string concatenation、greedy

**核心邏輯：**

* 題目要求排列數字，使得串接後的整體數值最大
* 比較規則不是單看數值大小，而是：
  + 比較字串 a + b 與 b + a 的大小
* 排序完成後，依序串接所有字串即為答案

**常見錯誤：**

* 直接以整數大小排序
* 比較時忘記使用字串串接
* 未處理前導零的情況

**C 骨架：**

```c
char s[N][20];
read n;
read n strings into s;
sort s using comparator: (a+b) > (b+a);
for i = 0 to n-1:
  print s[i];
print newline;
```

**小練習：**

* 改成輸出「最小」的串接數
* 將輸入改為可能包含負號的數字

**【UVA 11005 – Cheapest base】**

**關鍵字：**
base conversion、cost calculation、simulation

**核心邏輯：**

* 題目給每個 digit（0–35）的成本
* 對同一個數字 n，嘗試不同 base（2～36）
* 將 n 轉成該 base 表示後：
  + 累加每一位 digit 的成本
* 找出成本最低的 base（可能有多個）

**常見錯誤：**

* 忘記重設每個 base 的成本總和
* digit 對應錯誤（A=10, B=11, …）
* 只輸出一個 base，忽略並列最低的情況

**C 骨架：**

```c
read cost[0..35];
read query_count;

for each query n {
  minCost = INF;
  for base = 2 to 36 {
    costSum = 0;
    temp = n;
    while (temp > 0) {
      digit = temp % base;
      costSum += cost[digit];
      temp /= base;
    }
    minCost = min(minCost, costSum);
  }
  print all bases with cost == minCost;
}
```

**小練習：**

* 若 n = 0，成本應如何計算？
* 改成只考慮 base 2～16

**【UVA 10424 – Love Calculator】**

**關鍵字：**
string processing、digit sum、ratio calculation

**核心邏輯：**

* 將名字中的字母轉換成數值（A=1, B=2, …）
* 對兩個名字各自計算總和
* 將總和反覆做「位數和」直到剩一位數
* 用較小值 ÷ 較大值 × 100，得到百分比

**常見錯誤：**

* 忘記忽略非字母字元
* 大小寫未統一處理
* 百分比計算未轉成浮點數

**C 骨架：**

```c
while (read name1 and name2) {
  sum1 = letter_sum(name1);
  sum2 = letter_sum(name2);
  sum1 = reduce_to_single_digit(sum1);
  sum2 = reduce_to_single_digit(sum2);
  ratio = (float)min(sum1, sum2) / max(sum1, sum2) * 100;
  printf("%.2f", ratio);
}
```

**小練習：**

* 改成輸出整數百分比（四捨五入）
* 額外輸出每個名字的中間計算過程

**【UVA 11332 – Summing Digits】**

**關鍵字：**
digit sum、iteration、digital root

**核心邏輯：**

* 題目要求將數字反覆做位數和
* 直到結果只剩下一位數
* 每一輪都可以視為一次簡單的模擬

**常見錯誤：**

* 只做一次位數和就停止
* 使用遞迴但未設定終止條件
* 使用整數導致超大數讀取失敗

**C 骨架：**

```c
while (scanf("%s", s) == 1 && s != "0") {
  while (length(s) > 1) {
    sum = 0;
    for each digit d in s:
    sum += d;
    convert sum back to string s;
  }
  print s;
}
```

**小練習：**

* 改成同時輸出「進行了幾輪位數和」
* 嘗試用數學公式計算（digital root）
