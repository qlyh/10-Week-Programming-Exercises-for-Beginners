**【第 2 週｜條件判斷與流程控制】**

**【UVA 11764 – Jumping Mario】**

**關鍵字：**
adjacent comparison、counting

**核心邏輯：**

* 題目給一串瑪利歐跳躍的高度
* 只需要比較「**相鄰兩次高度的變化**」
* 若後一次高度 > 前一次 → high jump
* 若後一次高度 < 前一次 → low jump
* 統計 high 與 low 的次數即可

**常見錯誤：**

* 把所有高度存進陣列，其實沒有必要
* 忘記第一個高度只是參考起點，不算跳躍
* 將「相等高度」誤算成跳躍

**C 骨架：**

```c
int T, n, prev, cur, high, low;
scanf("%d", &T);
for (int tc = 1; tc <= T; tc++) {
  scanf("%d %d", &n, &prev);
  high = low = 0;
  for (int i = 1; i < n; i++) {
    scanf("%d", &cur);
    if (cur > prev) high++;
    else if (cur < prev) low++;
    prev = cur;
  }
  printf("Case %d: %d %d\n", tc, high, low);
}
```

**小練習：**

* 再統計「連續上升最長次數」
* 思考是否仍然不需要使用陣列

**【UVA 12250 – Language Detection】**

**關鍵字：**
string comparison、if-else

**核心邏輯：**

* 輸入是一個單字，代表問候語
* 根據單字內容判斷語言
* 使用字串比對（strcmp）即可
* 若輸入為 #，表示結束

**常見錯誤：**

* 使用 == 比較字串
* 忘記處理結束符號 #
* 忘記輸出格式中的 Case 編號

**C 骨架：**

```c
int caseNum = 1;
char s[100];

while (scanf("%s", s) == 1 && strcmp(s, "#") != 0) {
  printf("Case %d: ", caseNum++);
  if (strcmp(s, "HELLO") == 0) {
    printf("ENGLISH\n");
  } else if (strcmp(s, "HOLA") == 0) {
    printf("SPANISH\n");
  } else {
    printf("UNKNOWN\n");
  }
}
```

**小練習：**

* 新增 2 種語言
* 改成忽略大小寫輸入

**【UVA 12468 – Zapping】**

**關鍵字：**
circular distance、absolute value

**核心邏輯：**

* 頻道範圍是 0～99，形成一個環狀結構
* 從 a 轉到 b 有兩種方向：
  + 正向距離：abs(a - b)
  + 反向距離：100 - abs(a - b)
* 取兩者較小者

**常見錯誤：**

* 忘記考慮「反方向」
* 沒有使用 min() 比較兩種距離

**C 骨架：**

```c
while (scanf("%d %d", &a, &b) == 2 && (a != -1 || b != -1)) {
  int d = abs(a - b);
  printf("%d\n", d < 100 - d ? d : 100 - d);
}
```

**小練習：**

* 將頻道數改成 0～999
* 改成「只能往一個方向轉」

**【UVA 10469 – To Carry or not to Carry】**

**關鍵字：**
bitwise operation、XOR

**核心邏輯：**

* 題目描述的是「不進位加法」
* 在二進位中：
  + 不進位加法 = XOR
* 直接輸出 a ^ b 即可

**常見錯誤：**

* 用十進位加法模擬
* 嘗試逐位處理但邏輯過於複雜

**C 骨架：**

```c
unsigned long long a, b;
while (scanf("%llu %llu", &a, &b) == 2)
    printf("%llu\n", a ^ b);
```

**小練習：**

* 不使用 ^，自行用位元邏輯模擬 XOR

**【UVA 119 – Greedy Gift Givers】**

**關鍵字：**
mapping、simulation

**核心邏輯：**

* 題目本質是「名字 → 餘額」的對應關係
* 先記錄所有人名與初始餘額（0）
* 每個人送禮時：
  + 自己扣錢
  + 收禮者平均分配金額
* 最後依原輸入順序輸出結果

**常見錯誤：**

* 名字對應錯誤（找不到正確 index）
* 忘記餘數金額要留在送禮者身上
* 輸出順序錯誤（應依原人名順序）

**C 骨架：**

```c
  read n
  read names[0..n-1]
  init balance[0..n-1] = 0

  for each giver {
    read giverName, totalMoney, k
    find giver index g
    if (k > 0) {
      each = totalMoney / k
      balance[g] -= each \* k
      for k receivers {
        read receiverName
        find receiver index r
        balance[r] += each
      }
    }
  }
  print names[i], balance[i]
```

**小練習：**

* 額外輸出「送出最多錢的人」
* 改成用結構體 struct Person 儲存資料
