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
### 2. 
