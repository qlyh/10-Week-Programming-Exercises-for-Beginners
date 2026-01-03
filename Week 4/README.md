**【第 4 週｜進位制與數字系統】**

**【UVA 389 – Basically Speaking】**

**關鍵字：**
base conversion、string number、simulation

**核心邏輯：**

* 題目給一個「以 base A 表示的數字（字串）」
* 目標是將它轉換成「以 base B 表示」
* 解題可分成兩個階段：
  1. 將 base A 的字串轉成十進位整數
  2. 再將十進位整數轉成 base B
* 轉換過程需逐位處理，不能直接用內建轉型

**常見錯誤：**

* 把輸入當成十進位整數讀取
* 字母與數字對應錯誤（A=10, B=11, …）
* 忘記處理輸出寬度（題目常限制字元數）

**C 骨架：**

char s[50];

int baseA, baseB;

while (scanf("%s %d %d", s, &baseA, &baseB) == 3) {

long long value = 0;

// base A -> decimal

for (each character c in s) {

digit = convert c to value;

value = value \* baseA + digit;

}

// decimal -> base B

if (value == 0)

output '0';

else {

while (value > 0) {

digit = value % baseB;

push digit into array;

value /= baseB;

}

reverse and output result;

}

}

**小練習：**

* 禁用十進位中繼，直接嘗試 base A → base B
* 加入錯誤判斷：若 digit ≥ baseA 則輸出 error

**【UVA 10931 – Parity】**

**關鍵字：**
binary representation、bit count、parity

**核心邏輯：**

* 將十進位整數轉成二進位表示
* 在轉換過程中統計 1 出現的次數
* 1 的總數即為 parity
* 輸出時需同時顯示二進位字串與 parity

**常見錯誤：**

* 只計算 parity，忘記輸出二進位表示
* 二進位順序顛倒（低位先算，高位後印）
* 未處理 n = 0 的特殊情況

**C 骨架：**

while (scanf("%d", &n) == 1 && n != 0) {

int bits[50], cnt = 0, idx = 0;

while (n > 0) {

bits[idx++] = n % 2;

if (n % 2 == 1)

cnt++;

n /= 2;

}

print bits in reverse order;

print cnt;

}

**小練習：**

* 改用位元運算（n & 1、n >> 1）
* 輸出二進位長度（bit-length）

**【UVA 10019 – Funny Encryption Method】**

**關鍵字：**
bit counting、number representation

**核心邏輯：**

* 題目要求計算兩個數值：
  1. n 的二進位表示中 1 的個數
  2. 將 n 當作十進位數字字串，轉成十六進位後，再計算其二進位中 1 的個數
* 本質是「**同一個數，用不同表示方式，再做 bit count**」

**常見錯誤：**

* 誤以為要真的做加密或 XOR
* 混淆十進位、二進位、十六進位的角色
* bit count 計算錯誤

**C 骨架：**

int bitcount(int x) {

int cnt = 0;

while (x > 0) {

cnt += x & 1;

x >>= 1;

}

return cnt;

}

while (scanf("%d", &n) == 1) {

int count1 = bitcount(n);

// treat n as decimal digits, convert to hex value

int hexValue = convert decimal digits of n to hex;

int count2 = bitcount(hexValue);

printf("%d %d\n", count1, count2);

}

**小練習：**

* 改成比較二進位與八進位表示
* 使用內建函式與手寫 bit count 比較效能

**【UVA 10190 – Divide, But Not Quite Conquer!】**

**關鍵字：**
simulation、sequence、validation

**核心邏輯：**

* 從 n 開始反覆除以 m
* 每一步必須「整除」且結果必須大於 1
* 若最後剛好得到 1，輸出整個序列
* 否則輸出 Boring!

**常見錯誤：**

* 忘記檢查是否整除
* 中途產生 0 或非整數仍繼續運算
* 邊算邊印，導致格式難以控制

**C 骨架：**

while (scanf("%lld %lld", &n, &m) == 2) {

long long seq[100];

int len = 0;

bool ok = true;

seq[len++] = n;

while (n > 1) {

if (n % m != 0) {

ok = false;

break;

}

n /= m;

seq[len++] = n;

}

if (ok && seq[len-1] == 1)

print seq;

else

print "Boring!";

}

**小練習：**

* 若限制序列長度最多為 20，應如何修改？
* 改成「除以 m 或減 1」的混合規則

**【UVA 10943 – How do you add?】**

**關鍵字：**
dynamic programming、partition

**核心邏輯：**

* 題目在問：
  + 將整數 n 拆成 k 個非負整數相加的「方法數」
* 定義 DP 狀態：
  + dp[i][j]：用 i 個數字加總為 j 的方法數
* 使用遞推關係建立 DP 表
* 所有結果需對 1,000,000 取模

**常見錯誤：**

* DP 陣列大小不足
* 忘記取模導致 overflow
* 對 DP 狀態定義混亂

**C 骨架：**

int dp[101][101];

initialize dp[0][0] = 1;

for (int i = 1; i <= k; i++) {

for (int j = 0; j <= n; j++) {

for (int x = 0; x <= j; x++) {

dp[i][j] += dp[i-1][j-x];

dp[i][j] %= 1000000;

}

}

}

print dp[k][n];

**小練習：**

* 改成每個數字至少為 1
* 使用滾動陣列優化空間複雜度