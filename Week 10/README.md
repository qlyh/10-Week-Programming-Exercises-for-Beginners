# 第 10 週｜綜合練習與檢核
本週核心概念：**不是新技巧，而是「選對資料結構 + 正確模擬 + 穩定輸出格式」**

這 5 題非常適合：期末考、綜合練習、分組討論題

---

##【UVA 10008 - What's Cryptanalysis?】

**關鍵字**：frequency counting、sorting、case-insensitive

**核心邏輯**
- 統計文章中每個英文字母出現的次數
- 規則：
  - 只計算英文字母
  - 不分大小寫
- 輸出排序：
  - 依出現次數由大到小
  - 次數相同時依字母順序（A→Z）

**常見錯誤**
- 未忽略大小寫
- 將非字母字元納入統計
- 排序條件寫不完整（只排序 count 或只排序 letter）

**C 語言骨架**
```c
int cnt[26] = {0};
/* read n lines */
for each line {
  for each char c in line {
    if (isalpha(c)) cnt[toupper(c) - 'A']++;
  }
}
build array of (letter, count);
sort by: count desc, letter asc;
print result;
```

**小練習**
- 同時輸出百分比
- 只輸出出現次數 ≥ 5 的字母

---

##【UVA 299 - Train Swapping】##

**關鍵字**：bubble sort、inversion count

**核心邏輯**
- 題目問最少需交換幾次把序列排序（遞增）
- 本質是計算反序（inversions）
- 用 bubble sort 模擬即可（每次交換計數）

**常見錯誤**
- 忘記每次交換都要計數
- 排序方向錯誤
- 誤以為一定要用更複雜的最佳化演算法

**C 語言骨架**
```c
read T;
for each test case {
  read n;
  read array a[];
  swaps = 0;
  for (i = 0; i < n; i++)
    for (j = 0; j < n-1; j++)
      if (a[j] > a[j+1]) { swap(a[j], a[j+1]); swaps++; }
  print swaps;
}
```

**小練習**
- 改用 merge sort 計算 inversions（O(n log n)）
- 輸出實際的交換過程

---

##【UVA 10107 - What is the Median?】##

**關鍵字**：running median、sorted container

**核心邏輯**
- 逐筆讀入數字，每輸入一個就輸出目前的中位數
- 簡單作法（適合入門）：把數字放陣列，每次插入後排序，取中位數

**常見錯誤**
- 只在結尾輸出一次中位數
- 中位數位置計算錯誤（奇/偶）
- 使用 int 可能導致 overflow（視題目數值範圍）

**C 語言骨架**
```c
int a[10000], n = 0;
while (scanf("%d", &x) == 1) {
  a[n++] = x;
  sort(a, a + n);
  if (n % 2 == 1) print a[n/2];
  else print (a[n/2 - 1] + a[n/2]) / 2;
}
```

**小練習**
- 改用兩個 heap（max-heap, min-heap）優化時間
- 同時輸出最大值與最小值

---

##【UVA 11044 - Searching for Nessy】##

**關鍵字**：math observation、ceiling division

**核心邏輯**
- 每個聲納可覆蓋 3×3 區域
- 可用格子數為 (n-2) × (m-2)
- 所需聲納數為 ceil((n-2)/3) × ceil((m-2)/3)

**常見錯誤**
- 忘記扣掉邊界（-2）
- 使用整數除法導致少算
- 用模擬代替簡潔數學公式

**C 語言骨架**
```c
read T;
while (T--) {
  read n, m;
  int rows = (n - 2 + 2) / 3; // ceil((n-2)/3)
  int cols = (m - 2 + 2) / 3;
  print rows * cols;
}
```

**小練習**
- 改成每個聲納覆蓋 4×4
- 輸出實際放置位置（格點）

---

##【UVA 12403 - Save Setu】##

**關鍵字**：command processing、accumulation

**核心邏輯**
- 維護一個帳戶總金額
- 指令：
  - "donate x"：增加金額
  - "report"：輸出目前總額
- 不需要複雜資料結構

**常見錯誤**
- 金額未累加
- 輸入字串解析錯誤
- 忘記多筆指令處理

**C 語言骨架**
```c
read T;
long long total = 0;
while (T--) {
  read command;
  if (command == "donate") {
    read x; total += x;
  } else if (command == "report") {
    print total;
  }
}
```

**小練習**
- 新增 withdraw 指令
- 記錄每次操作的歷史紀錄
