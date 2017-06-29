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
