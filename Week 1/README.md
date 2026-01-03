**【第 1 週｜基本輸入輸出與數學模擬】**

**【UVA 100 – The 3n + 1 Problem】**

**關鍵字：**
range、cycle length、max

**核心邏輯：**

* 題目本質是在做「**區間內每個 n 的模擬**」
* 對單一 n：
  + 不斷進行 3n + 1（若 n 為奇數）或 n / 2（若 n 為偶數）
  + 直到 n 變成 1，並計算總步數（cycle length）
* 對整個區間：
  + 計算每個 n 的 cycle length
  + 取其中的最大值輸出

**常見錯誤：**

* 忘記處理 i > j 的情況（需要先交換）
* 使用遞迴實作，導致 stack overflow
* 以為需要把整個區間的結果存起來（其實只要即時計算最大值即可）

**C 骨架：**

```c
while (scanf("%d %d", &i, &j) == 2) {
  int L = min(i, j);
  int R = max(i, j);
  int maxLen = 0;

  for (int n = L; n <= R; n++) {
    int len = simulate(n);
    if (len > maxLen) {
      maxLen = len;
    }
  }
  printf("%d %d %d\n", i, j, maxLen);
}
```

**小練習：**

* 限制最大模擬步數為 1000
* 若超過 1000 步就停止，觀察輸出結果與原題差異

**【UVA 113 – Power of Cryptography】**

**關鍵字：**
n-th root

**核心邏輯：**

* 題目已知 k^n = p
* 直接反推 k = p^(1/n)
* 因為使用浮點數計算，必須取最接近的整數

**常見錯誤：**

* 使用 int 或 long long 直接計算次方，造成 overflow
* 忘記使用 round() 修正浮點誤差，導致 WA

**C 骨架：**

```c
while (scanf("%d %lf", &n, &p) == 2)
  printf("%lld\n", (long long) round(pow(p, 1.0 / n)));
```

**小練習：**

* 禁用 pow()
* 改用 binary search 找出符合 k^n ≈ p 的整數 k

**【UVA 11150 – Cola】**

**關鍵字：**
exchange、simulation

**核心邏輯：**

* 以「空瓶換可樂」為情境進行模擬
* 每 3 個空瓶可以換 1 瓶可樂
* 喝完後產生新的空瓶，持續累積並重複兌換

**常見錯誤：**

* 忘記把餘數空瓶保留下來繼續使用
* 借瓶的邏輯處理錯誤

**C 骨架：**

```c
while (scanf("%d", &n) == 1) {
    int drink = 0;
    while (n >= 3) {
        drink += n / 3;
        n = n / 3 + n % 3;
    }
    printf("%d\n", drink);
}
```

**小練習：**

* 將規則改成「4 瓶空瓶換 1 瓶可樂」

**【UVA 10970 – Big Chocolate】**

**關鍵字：**
minimum cuts

**核心邏輯：**

* 每切一刀，巧克力塊數只會增加 1
* 從 1 塊切到 m × n 塊，總共需要 m × n − 1 刀
* 直接使用公式即可，無需模擬

**常見錯誤：**

* 嘗試用遞迴或實際模擬切割過程，導致程式過於複雜

**C 骨架：**

```c
while (scanf("%lld %lld", &m, &n) == 2) {
	printf("%lld\n", m \* n - 1);
}
```

**小練習：**

* 若每次切割「最多只能切成 3 塊」，是否仍存在封閉公式？

**【UVA 11479 – Is this the easiest problem?】**

**關鍵字：**
triangle validity

**核心邏輯：**

* 讀入三邊長後先進行排序
* 若最小兩邊和 a + b > c，才構成合法三角形
* 再依邊長關係分類（三角形類型）

**常見錯誤：**

* 使用 int 儲存邊長，導致加法 overflow
* 未先排序就直接判斷

**C 骨架：**

```c
read a, b, c
sort three values
if (a + b <= c)
	print "Invalid"
else
	classify triangle
```

**小練習：**

* 增加「直角三角形」的判斷條件
