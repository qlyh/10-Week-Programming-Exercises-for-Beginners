\*\*【第 10 週｜綜合練習與檢核】\*\*



本週核心概念：  

\*\*不是新技巧，而是「選對資料結構 + 正確模擬 + 穩定輸出格式」\*\*。  

這 5 題非常適合：



\- 期末考

\- 綜合練習

\- 分組討論題



\*\*【UVA 10008 - What's Cryptanalysis?】\*\*



\*\*關鍵字：\*\*  

frequency counting、sorting、case-insensitive



\*\*核心邏輯：\*\*



\- 統計文章中每個英文字母出現的次數

\- 規則：

&nbsp; - 只計算英文字母

&nbsp; - 不分大小寫

\- 輸出時需依：

&nbsp; - 出現次數由大到小

&nbsp; - 若次數相同，依字母順序



\*\*常見錯誤：\*\*



\- 沒有忽略大小寫

\- 將非字母字元納入統計

\- 排序條件只寫一半



\*\*C 骨架：\*\*



int cnt\\\[26\\] = {0};



read n lines;



for each line {



for each character c {



if is letter:



cnt\\\[toUpper(c) - 'A'\\]++;



}



}



build array of (letter, count);



sort by:



count desc,



letter asc;



print result;



\*\*小練習：\*\*



\- 改成同時輸出百分比

\- 只輸出出現次數 ≥ 5 的字母



\*\*【UVA 299 - Train Swapping】\*\*



\*\*關鍵字：\*\*  

bubble sort、inversion count



\*\*核心邏輯：\*\*



\- 題目在問：

&nbsp; - 將火車依序排序成遞增

&nbsp; - 最少需要交換幾次

\- 本質就是計算「反序數量（inversion）」

\- 使用 bubble sort 模擬即可



\*\*常見錯誤：\*\*



\- 忘記每次交換都要計數

\- 排序方向錯誤

\- 誤以為需要最佳化排序演算法



\*\*C 骨架：\*\*



read T;



for each test case {



read n;



read array a\\\[\\];



swaps = 0;



for i = 0 to n-1:



for j = 0 to n-2:



if a\\\[j\\] > a\\\[j+1\\]:



swap;



swaps++;



print swaps;



}



\*\*小練習：\*\*



\- 改用 merge sort 計算 inversion

\- 輸出實際的交換過程



\*\*【UVA 10107 - What is the Median?】\*\*



\*\*關鍵字：\*\*  

running median、sorted container



\*\*核心邏輯：\*\*



\- 逐筆讀入數字

\- 每輸入一個數字，就要輸出目前的中位數

\- 簡單作法（適合大一）：

&nbsp; - 將所有數字存入陣列

&nbsp; - 每次插入後排序

&nbsp; - 取中位數



\*\*常見錯誤：\*\*



\- 只在最後輸出一次中位數

\- 中位數位置計算錯誤（奇偶）

\- 使用 int 導致 overflow



\*\*C 骨架：\*\*



int a\\\[10000\\], n = 0;



while (scanf("%d", \&x) == 1) {



a\\\[n++\\] = x;



sort a\\\[0..n-1\\];



if (n % 2 == 1)



print a\\\[n/2\\];



else



print (a\\\[n/2 - 1\\] + a\\\[n/2\\]) / 2;



}



\*\*小練習：\*\*



\- 改用兩個 heap 優化時間複雜度

\- 同時輸出最大值與最小值



\*\*【UVA 11044 - Searching for Nessy】\*\*



\*\*關鍵字：\*\*  

math observation、ceiling division



\*\*核心邏輯：\*\*



\- 題目背景是聲納掃描

\- 每個聲納可覆蓋 3×3 區域

\- 實際可用的格子為：

&nbsp; - (n-2) × (m-2)

\- 答案為：

&nbsp; - ceil((n-2)/3) × ceil((m-2)/3)



\*\*常見錯誤：\*\*



\- 忘記扣掉邊界

\- 使用整數除法導致少算

\- 嘗試用模擬而非數學公式



\*\*C 骨架：\*\*



read T;



while (T--) {



read n, m;



int rows = (n - 2 + 2) / 3;



int cols = (m - 2 + 2) / 3;



print rows \\\* cols;



}



\*\*小練習：\*\*



\- 改成每個聲納覆蓋 4×4

\- 輸出實際放置的位置



\*\*【UVA 12403 - Save Setu】\*\*



\*\*關鍵字：\*\*  

command processing、accumulation



\*\*核心邏輯：\*\*



\- 維護一個帳戶總金額

\- 兩種指令：

&nbsp; - donate x：增加金額

&nbsp; - report：輸出目前總額

\- 完全不需要額外資料結構



\*\*常見錯誤：\*\*



\- 金額未累加

\- 輸入字串讀取錯誤

\- 忘記處理多筆指令



\*\*C 骨架：\*\*



read T;



total = 0;



while (T--) {



read command;



if command == "donate":



read x;



total += x;



else if command == "report":



print total;



}



\*\*小練習：\*\*



\- 新增 withdraw 指令

\- 記錄每一次操作的歷史紀錄

