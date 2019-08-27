### 1. intro
- str 是一個 immutable datatype, 以 a sequence of characters in Unicode 儲存
- 可用 單引號 (') 或 雙引號 (") 或 三雙引號 (""") 建立字串
- 常用的規避序列
  ```
  \     # escape 規避換列字符
  \\    # 反斜線 (\)
  \a    # 響鈴
  \b    # backspace
  \f    # 換頁
  \n    # 換行
  \r    # 回行首
  \t    # 跳格
  \v    # 垂直跳格
  ```
  在使用正規表示法的時候，常常會需要跳脫許多字符，此時可用原始(raw)字串。在引號前加上 r，例如：
  ```
  import re
  phone1 = re.compile(r"^((?:[(]\d+[(])?\s*\d+(?:-\d+)?)$")
  ```
  另外，若字串太長，可用 () 小括號建立一個字串如：
  ```
  s = ("This is the nice way to join two long strings."
      "together; it relies on string literal concatenation.")
  ```

### 2. slice
```
seq[index]          # get the character at index
seq[start:end]      # get the sequence of character from index start to index end
seq[start:end:step] # get the character sequence from index start to index end by interval step
```
index 可以用順向 start from 0 也可用反向的 start from -1
```
| 0 | 1 | 2 | 3 | 4 | index         |
| a | p | p | l | e | string        |
|-5 |-4 |-3 |-2 |-1 | index_reverse |

# another cool example:
s = 'abcdef'
s[::-1] # will print 'fedcba' # 提取每個 character, step = -1 從結尾往回!
```

### 3. operators and methods for str
- immutable sequence, 所有 immutable object 用的 operators 如: 
  in (隸屬), + (連接), += (附加), * (複製), *= 

- str methods 列表
```
s.capitalize()            # 回傳字串 s 第一個字母變大寫
**s.title()               # 回傳字串 s 其中每個單字的第一個字都大寫
s.center(width, char)     # s 被置中於一長度於 width 的字串裡，用 char 填補空白
s.ljust(width, char)      # 類似 s.center() 但 s 置左
s.rjust(width, char)      # 類似 s.center() 但 s 置右
**s.count(t, start, end)  # 回傳字串 t 在字串 s[start:end] 中出現的次數
s.encode(encoding, err)   # 回傳一個 bytes 物件, 會使用 encoding 指定的編碼方式表示
s.endswith(x,start,end)   # 回傳 boolean of 字串 s[start:end] 是否以字串 x 結束
s.startswith(x,start,end) # 回傳 boolean of 字串 s[start:end] 是否以字串 x 開始
s.expandtabs(size)        # s 的空格(以 8 或 size 的倍數)取代為跳格 \t
**s.find(t,start,end)     # 回傳 t 在字串 s[start:end] 中最左邊的位置, return -1 if not found
s.rfind(t,start,end)      # 回傳 t 在字串 s[start:end] 中最右邊的位置, return -1 if not found
s.index(t,start,end)      # 類似 s.find(t,start,end), exception ValueError if not found
s.isalnum()               # 回傳 boolean of 字串 s 非空字串且每個 character 皆為文數字
s.isalpha()               # 回傳 boolean of 字串 s 非空字串且每個 character 皆為字母
s.isdecimal()             # 回傳 boolean of 字串 s 非空字串且每個 character 皆為 Unicode 數字 (以 10 為底)
s.isdigit()               # 回傳 boolean of 字串 s 非空字串且每個 character 皆為 ASC II 數字
s.isnumeric()             # 回傳 boolean of 字串 s 非空字串且每個 character 皆為數值形式的 Unicode (可以是數字或小數)
**s.isidentifier()        # 回傳 boolean of 字串 s 非空字串且是一個有效的 identifier
s.islower()               # 回傳 boolean of 至少有一個可小寫的字母, 且所有小寫都是小寫了
s.isupper()               # 回傳 boolean of 至少有一個可大寫的字母, 且所有大寫都是大寫了
s.isprintable()           # 可否印出
s.isspace()               # 回傳 boolean of 字串 s 非空字串且所有字都是空白字母
s.istitle()               # 回傳 boolean of 字串 s 非空字串且首字母大寫的標題
**s.join(seq)             # 連接序列 seq 中的每個 item 於字串 s 後方
s.lower()                 # 字串 s 轉小寫
s.upper()                 # 字串 s 轉大寫
s.partition(t)            # 
**s.replace(t, u, n)      # 字串 s 出現 t 的地方換成 u, 最多取代 n 次
**s.split(t, n)           # 字串 s 以 t 切割, 最多切割 n 次
s.splitlines(f)           # 回傳 list, 以 \n 當作終止符號切割字串 s, if f==True, 保留終止符號
**s.strip(chars)          # 移除字串 s 前後的空白
s.swapcase()              # 大小寫互換
s.zfill(w)                # 若字串 s 長度小於 w, 則加入前導的零使長度為 w
```

### 4. Useful methods on str
```
"<[unbracketed]>".strip("[](){}<>") # 可以同時移除多個 characters
```
#### str.format(arguments)
1. arguments 會依序放入 {} 的位置
```
"This book, named {}, is one of my favorite books {}".format("Compounded-eye Man", ":)")
```
2. 可以使用 (key = value) pair
```
"This book, named {name}, is one of my favorite books {emoji}".format(name="Compounded-eye Man",emoji=":)")
```
3. 可以使用 array + 指定 index
```
arr = ["Compounded-eye Man",":)"]
"This book, named {0[0]}, is one of my favorite books {0[1]}".format(arr)
```
4. 可以使用 dict + 給定 key
```
dict = (name="Compounded-eye Man",emoji=":)")
"This book, named {0[name]}, is one of my favorite books {0[emoji]}".format(dict)
```
5. 可以存取 attribute
```
import math, sys
"math.pi == {0.pi} and sys.maxunicode == {1.maxunicode}".format(math,sys)
```
6. 使用 \*\* (mapping unpacking)
```
name = "Compounded-eye Man"
emoji = ":)"
"This book, named {name}, is one of my favorite books {emoji}".format(**locals())
```
另外，只要是 mapping datatype (例如: dict) 就可以使用此方法
```
dict = (name="Compounded-eye Man",emoji=":)")
"This book, named {name}, is one of my favorite books {emoji}".format(**dict)
```
