**【第 3 週｜陣列與字串處理】**

**【UVA 10035 – Primary Arithmetic】**

**關鍵字：**
digit simulation、carry、string

**核心邏輯：**

* 題目在模擬「直式加法的進位過程」
* 不需要真的算總和，只需要統計「進位發生的次數」
* 從個位數開始逐位相加：
  + a\_digit + b\_digit + carry
  + 若結果 ≥ 10，則產生一次進位
* 直到所有位數處理完畢

**常見錯誤：**

* 只判斷 a\_digit + b\_digit >= 10，忘記考慮前一位 carry
* 使用整數運算導致位數對齊困難
* 當進位數為 0 時仍輸出錯誤訊息

**C 骨架：**

```c
char a[1000], b[1000];

while (scanf("%s %s", a, b) == 2 && (strcmp(a, "0") || strcmp(b, "0"))) {
  int i = strlen(a) - 1, j = strlen(b) - 1, carry = 0, count = 0;

  while (i >= 0 || j >= 0) {
    int da = (i >= 0) ? a[i--] - '0' : 0;
    int db = (j >= 0) ? b[j--] - '0' : 0;

    if (da + db + carry >= 10) {
      count++;
      carry = 1;
    } else {
      carry = 0;
    }
  }
  print carry count result;
}
```

**小練習：**

* 改成輸出「每一位是否產生進位」
* 嘗試不用字串，直接用整數實作（觀察難度差異）

**【UVA 10300 – Ecological Premium】**

**關鍵字：**
accumulation、loop

**核心邏輯：**

* 每一筆資料包含：
  + 農場大小
  + 動物數量
  + 環保等級
* 題目公式實際上只需要：
  + size × eco\_value
* 動物數量不影響結果，只是干擾資訊

**常見錯誤：**

* 將動物數量誤用進計算
* 使用不必要的陣列儲存所有資料
* 忘記重設每個測資的總和

**C 骨架：**

```c
int T, f;
long long size, animal, eco, sum;

scanf("%d", &T);

while (T--) {
  scanf("%d", &f);
  sum = 0;
  while (f--) {
    scanf("%lld %lld %lld", &size, &animal, &eco);
    sum += size * eco;
  }
  printf("%lld\n", sum);
}
```

**小練習：**

* 輸出每一個農場的個別補助金
* 改成在最後只輸出最高補助的農場

**【UVA 10082 – WERTYU】**

**關鍵字：**
character mapping、array lookup

**核心邏輯：**

* 題目要求把鍵盤上輸入的字元，轉換成「左邊那一個鍵」
* 可以把整個鍵盤排列存成一個字串
* 對每個輸入字元：
  + 找到它在鍵盤字串中的位置
  + 輸出前一個字元

**常見錯誤：**

* 沒有處理空白字元
* 當輸入字元是鍵盤最左邊時發生越界
* 忘記逐行讀取（空白會被吃掉）

**C 骨架：**

```c
char keyboard[] = "`1234567890-=QWERTYUIOP[]\\ASDFGHJKL;'ZXCVBNM,./";
char line[1000];

while (fgets(line, sizeof(line), stdin)) {
  for (int i = 0; line[i]; i++) {
    if (line[i] == ' ') {
      putchar(' ');
    } else {
      for (int k = 0; keyboard[k]; k++) {
        if (keyboard[k] == line[i]) {
          putchar(keyboard[k - 1]);
          break;
        }
      }
    }
  }
}
```

**小練習：**

* 改成輸出「右邊那一個鍵」
* 支援小寫字母輸入

**【UVA 10922 – 2 the 9s】**

**關鍵字：**
string number、digit sum、digital root

**核心邏輯：**

* 題目要判斷一個數是否為 9 的倍數
* 使用「位數和」的性質：
  + 將所有數字相加
  + 若結果 ≥ 10，繼續對結果做位數和
* 計算進行位數和的次數，即為 9-degree

**常見錯誤：**

* 只檢查一次位數和
* 對結果為 9 的情況未正確輸出 degree
* 使用整數導致超大數無法處理

**C 骨架：**

```c
char s[1000];

while (scanf("%s", s) == 1 && strcmp(s, "0") != 0) {
  int sum = digit_sum(s);
  int degree = 1;

  while (sum >= 10) {
    sum = digit_sum_of_number(sum);
    degree++;
  }

  if (sum == 9) {
    printf("result based on degree\n"); // Replace with actual printing logic
  } else {
    printf("other result\n"); // Replace with actual printing logic
  }
}
```
**小練習：**

* 改成判斷是否為 3 的倍數
* 輸出每一輪位數和的中間結果

**【UVA 10188 – Automated Judge Script】**

**關鍵字：**
string processing、exact match、format check

**核心邏輯：**

* 題目比較「標準輸出」與「使用者輸出」
* 判斷順序為：
  1. 完全相同 → Accepted
  2. 抽取所有數字後相同 → Presentation Error
  3. 其他 → Wrong Answer
* 因此必須同時保留：
  1. 原始輸出內容
  2. 只含數字的版本

**常見錯誤：**

* 忘記逐行讀取（換行會影響比對）
* 比對時多算或少算空白
* 沒有先檢查完全相同的情況

**C 骨架：**

```c
read n
read n lines of correct output into array A
read m
read m lines of user output into array B

if A and B are exactly equal:
  print "Accepted"
else if the digits extracted from A equal the digits extracted from B:
  print "Presentation Error"
else:
  print "Wrong Answer"
```

**小練習：**

* 改成只比較「英文字母」
* 新增一種判定狀態（例如：Too Much Output）
