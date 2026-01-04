**【第 7 週｜Map / Set 與資料記錄】**

本週核心概念：
**如何用資料結構「記錄、統計、分類」資料**
在純 C 語言情境下，重點放在「**陣列＋排序＋掃描**」來取代 map / set 的功能。

**【UVA 10252 – Common Permutation】**

**關鍵字：**
frequency array、character counting

**核心邏輯：**

* 給定兩行字串
* 要找出「兩個字串中共同出現的字母」，且：
  + 每個字母輸出 min(出現次數1, 出現次數2) 次
* 只需處理小寫字母 a～z
* 使用兩個長度為 26 的計數陣列即可

**常見錯誤：**

* 忘記將計數陣列清空
* 使用巢狀迴圈比對字元，效率太差
* 輸出順序錯誤（必須依字母順序）

**C 骨架：**

char s1[1000], s2[1000];

int cnt1[26], cnt2[26];

while (fgets(s1, sizeof(s1), stdin) &&

fgets(s2, sizeof(s2), stdin)) {

initialize cnt1, cnt2 to 0;

for each character c in s1:

cnt1[c - 'a']++;

for each character c in s2:

cnt2[c - 'a']++;

for i = 0 to 25:

repeat min(cnt1[i], cnt2[i]) times:

print character (i + 'a');

print newline;

}

**小練習：**

* 改成同時支援大寫與小寫
* 輸出共同字母的總數

**【UVA 10420 – List of Conquests】**

**關鍵字：**
string parsing、counting、sorting

**核心邏輯：**

* 每一行輸入代表一位人物
* 第一個單字是「國家名稱」，後面名字可忽略
* 目標是統計「每個國家出現的次數」
* 作法（純 C）：
  1. 將所有國家名稱存入陣列
  2. 排序
  3. 掃描統計連續相同字串

**常見錯誤：**

* 把整行當作 key（導致國家＋人名一起算）
* 未正確處理換行字元
* 忘記依字典序輸出

**C 骨架：**

int n;

char country[2000][50];

scanf("%d", &n);

consume newline;

for (i = 0; i < n; i++) {

read entire line;

extract first word as country[i];

}

sort country array;

count = 1;

for (i = 1; i <= n; i++) {

if (i < n and country[i] == country[i-1])

count++;

else {

print country[i-1], count;

count = 1;

}

}

**小練習：**

* 同時統計「名字首字母」出現次數
* 改成忽略大小寫的國家名稱

**【UVA 11286 – Conformity】**

**關鍵字：**
combination key、sorting、frequency

**核心邏輯：**

* 每位學生選 5 門課
* 課程順序不重要，只在乎「組合」
* 解題重點：
  + 將 5 個課程編號先排序
  + 組合排序後才能作為「相同 key」
* 統計每種組合出現次數
* 找出最大次數，並加總所有同樣最大次數的組合人數

**常見錯誤：**

* 未先排序 5 個課程
* 只輸出最大次數，忘記加總人數
* 使用字串 key 時格式不一致

**C 骨架：**

int course[5];

string keyList[10000];

for each student {

read 5 course numbers;

sort course[5];

create key from course[5];

store key in keyList;

}

sort keyList;

maxCount = currentCount = 1;

total = 0;

for each key in keyList {

if same as previous:

currentCount++;

else:

update maxCount and total;

currentCount = 1;

}

print total;

**小練習：**

* 改成學生選 6 門課
* 輸出「最冷門」的課程組合

**【UVA 10945 – Mother Bear】**

**關鍵字：**
string cleaning、palindrome

**核心邏輯：**

* 題目判斷一句話是否為回文
* 規則：
  + 只考慮英文字母
  + 忽略大小寫
* 處理步驟：
  + 清洗字串（過濾非字母、轉小寫）
  + 用雙指標判斷回文

**常見錯誤：**

* 未過濾標點符號與空白
* 大小寫未統一
* 指標移動邏輯錯誤

**C 骨架：**

char line[1000], clean[1000];

while (fgets(line, sizeof(line), stdin)) {

if (line == "DONE")

break;

build clean string:

keep only letters

convert to lowercase;

left = 0, right = strlen(clean) - 1;

while (left < right) {

if (clean[left] != clean[right])

not palindrome;

left++; right--;

}

print result;

}

**小練習：**

* 改成保留數字也參與判斷
* 輸出最長回文子字串

**【UVA 755 – 487–3279】**

**關鍵字：**
string mapping、normalization、duplicate detection

**核心邏輯：**

* 將電話號碼中的字母轉成數字（依電話鍵盤對應）
* 移除 -，統一成 7 位數字格式
* 對所有號碼進行排序
* 找出重複出現的號碼及其出現次數

**常見錯誤：**

* 字母對應數字錯誤
* 未移除破折號
* 忘記排序導致重複偵測困難

**C 骨架：**

char phone[10000][10];

for each input string s {

convert letters to digits;

remove '-';

store normalized phone number;

}

sort phone numbers;

count = 1;

for (i = 1; i <= n; i++) {

if (i < n and phone[i] == phone[i-1])

count++;

else if (count > 1)

print phone[i-1], count;

count = 1;

}

**小練習：**

* 改成輸出所有號碼（包含不重複）
* 支援更多字母對應規則