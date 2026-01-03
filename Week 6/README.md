**【第 6 週｜Stack / Queue】**

**【UVA 514 – Rails】**

**關鍵字：**
stack、simulation、LIFO

**核心邏輯：**

* 題目在模擬火車進出站的過程
* 火車依序以 1 → n 進站
* 站內是一個 **stack（後進先出）**
* 目標是判斷：是否能用 stack 操作，產生指定的輸出順序
* 做法：
  + 依序將火車推入 stack
  + 當 stack 頂端等於目標序列的下一個數字時，就 pop

**常見錯誤：**

* 沒有依照 1→n 的順序 push 火車
* 在 stack 為空時嘗試 pop
* 輸出格式錯誤（Yes / No 大小寫）

**C 骨架：**

```c
while (read n && n != 0) {
  while (read target sequence) {
    if (first number == 0) break;

    stack empty;
    nextTrain = 1;
    ok = true;

    for each target value x {
      while (nextTrain <= n && (stack empty or stack top != x)) {
        push nextTrain onto stack;
        nextTrain++;
      }

      if (stack top == x) {
        pop stack;
      } else {
        ok = false;
      }
    }

    print Yes or No;
  }
}
```

**小練習：**

* 輸出實際的 push / pop 操作順序
* 改成使用 queue，結果會有何不同？

**【UVA 10935 – Throwing cards away I】**

**關鍵字：**
queue、FIFO、simulation

**核心邏輯：**

* 使用 **queue（先進先出）** 模擬丟牌過程
* 重複以下操作直到只剩一張牌：
  1. 丟棄最前面的牌
  2. 將新的最前面牌移到隊尾
* 最後輸出：
  1. 丟棄過的牌
  2. 剩下的最後一張牌

**常見錯誤：**

* 用 stack 實作（方向完全錯）
* 丟牌與移牌的順序顛倒
* 輸出格式錯誤（逗號與空白）

**C 骨架：**

```c
while (scanf("%d", &n) == 1 && n) {
  queue q;
  for (int i = 1; i <= n; ++i) q.push(i);
  printf("Discarded cards:");
  while (q.size() > 1) {
    printf(" %d", q.front());
    q.pop();
    q.push(q.front());
    q.pop();
    if (q.size() > 1) printf(",");
  }
  printf("\nRemaining card: %d\n", q.front());
}
```

**小練習：**

* 改成一次丟 2 張牌
* 改成「丟一張、移兩張」

**【UVA 1062 – Containers】**

**關鍵字：**
greedy、stack top、character comparison

**核心邏輯：**

* 每個字母代表一個貨櫃
* 將貨櫃依序放到「最左邊可放的堆」
* 規則：
  + 只能放在 **堆頂字母 ≥ 目前字母** 的堆
  + 若沒有任何堆可放，建立新堆
* 最後堆的數量即為答案

**常見錯誤：**

* 每個堆真的用一個完整 stack（其實只需要堆頂）
* 放錯堆，導致堆數不是最小
* 忽略字母大小的比較規則

**C 骨架：**

```c
while (scanf("%s", s) == 1) {
    int piles = 0;
    int top_len = 0;

    for (int i = 0; s[i]; i++) {
        char c = s[i];
        int j;
        for (j = 0; j < top_len; j++) {
            if (top[j] >= c) {
                top[j] = c;
                break;
            }
        }
        if (j == top_len) {
            top[top_len++] = c;
            piles++;
        }
    }
    printf("%d\n", piles);
}
```

**小練習：**

* 改成「只能放在堆頂字母 ≤ 目前字母」
* 輸出每一堆的最終內容

**【UVA 11988 – Broken Keyboard】**

**關鍵字：**
deque、linked list、cursor simulation

**核心邏輯：**

* 題目模擬鍵盤游標行為：
  + [：游標移到最前面
  + ]：游標移到最後面
* 輸入字元依游標位置插入
* 關鍵在於：
  + 需要支援「頭插」與「尾插」
  + 同時維持中間文字的相對順序

**常見錯誤：**

* 直接用字串插入導致 O(n²) TLE
* 忘記清空暫存字串
* 處理多個 [ ] 時邏輯混亂

**C 骨架：**

```c
while reading each line:
  L = list of strings
  buffer = string
  insertAtFront = false
  for each character c in line:
    if c == '[':
      flush buffer to L
      insertAtFront = true
    else if c == ']':
      flush buffer to L
      insertAtFront = false
    else:
      buffer += c
  flush buffer to L
  print strings in L in order
```

**小練習：**

* 新增指令 {，表示游標移到中間
* 嘗試不用 linked list，只用陣列模擬

**【UVA 978 – Lemmings Battle!】**

**關鍵字：**
priority queue、max heap、simulation

**核心邏輯：**

* 綠軍與藍軍各有一批戰士
* 每一回合：
  + 各取出最強的戰士進行戰鬥
  + 較弱者死亡
  + 較強者若有剩餘戰力，回到隊伍中
* 使用 **max heap** 快速取得最強戰士

**常見錯誤：**

* 用排序陣列，每回合重新排序導致 TLE
* 忘記將存活戰士放回 heap
* 同一回合未同步處理多場戰鬥

**C 骨架：**

```c
for each test case {

    read number of battlefields B;
    read number of green soldiers;
    read number of blue soldiers;

    create maxHeap green;
    create maxHeap blue;

    while (green is not empty AND blue is not empty) {

        fight up to B pairs of soldiers;

        store surviving soldiers in temporary list;

        push survivors back into their respective heaps;
    }

    print winner;
    print remaining soldiers;
}
```

**小練習：**

* 改成使用 min heap，結果會如何？
* 記錄每一回合的戰鬥結果並輸出
