### 1. 資料型態 data type
- 例如: str, int, 和其他基本的數值型態都是 immutable
  ```
  a = 'abc'
  a[0]       # 印出 'a'
  a[0] = 'b' # 產生 error due to the immutable property
  ```

### 2. Objective reference
- 在 python 中，變數 variable 等於 物件參照 objective reference
- Operator '=' 將 objective reference 指到 RHS
- Dynamic typing 表示 objective reference 可以隨時指向不同資料型態的物件 (object)
- Objective reference 的名稱，被稱為 identifier，不能是任何 python 的關鍵字，大小寫有區別
  ```
  For example, LIMIT != Limit != limit
  ```

### 3. Collection in Python to Store A Group of Data
- tuple (immutable) vs. list (mutable)
- 只儲存 objective reference，建立時是建立 copy of objective reference
- Collection 本身也是 objective! 創造 list of lists 是容易的!
  ```
  "one",    # 印出 ("one",)
            # 過程中 "one" 這個 object 被建立，之後 objective reference 被放入 tuple 中！
  ```
- object 的特色是可以有 method，例如: objectName.methodName(arguments) 

### 4. 邏輯運算 logical computation
- Identity operator 用途為檢查兩個 objective reference 是否指向同一個 object， 或是否為 None。
  - 只需比較記憶體位址，猛快！
  ```
  # case 1
  a = ["Retention", 3, None]
  b = ["Retention", 3, None]
  a is b    # False

  # case 2
  b = a
  a is b    # True
  ```

- Comparison operator 比較 "值"。例如: < 小於, <= 小於等於, == 等於, != 不等於, >= 大於等於, > 大於
  ```
  # case 1
  a = 2
  b = 6
  a < b, a <= b, a == b, a != b, a >= b, a > b 
  (True, True, False, True, False, False)

  # case 2
  a = "path"
  b = "path"
  a is b    # False
  a == b    # True
  ```

- Membershipt operator 對於 sequence, collection 的資料型態，可以用 in 來測試 membership
  - in 是採用 linear search，對大的 collection 不利，但對於 dictionary, set 極快！
  ```
  p = (4, "br", -33)
  2 in p    # False
  "br" in p # True
  ```

- Logical operator 提供三種 and, or, not
  - and, or 為短路邏輯 (short-circuit logic)
  ```
  five = 5
  four = 4
  zero = 0
  five and four # 印出 4
  four and five # 印出 5
  zero and five # 印出 0
  ```

### 5. 控制流程, 有 if, while 和 for
- if 判斷式 (得到 a boolean value)
  ```
  if bool_expr1:
    suite1
  elif bool_expr2:
    suite2   
  else:
    pass    # do nothing
  ```
- while 讓一個 suite 執行多次，取決於 while loop 內的 bool_expr
  ```
  while True:
    item = get_next_item()
    if not item:
      break
    process_item(item)
  ```
- for ... in 
  - 重複利用 in 關鍵字
    ```
    for variable in iterable:
      suite
    ```
  - iterable 可以被迭代的資料型態，如: str (by character), list, tuple, collection
    ```
    countries = ["TW","US","KR","CN"]
    for country in countries:
      print(country)
    ```
- Exception 是一個 object，try_suite 若無例外產生則 except block 會被略過。若 except 在第 k 行 statement 發生，那麼 k 行後的 statements 都不會被執行。
  ```
  try:
    try_suite
  except exception1 as variable1: # variable 為文字訊息
    exception_suite1
  ...
  except exceptionN as variabelN:
    exception_suiteN
  ```
  
  
  
### 6. 算術運算符 +, -, *, /
- augmented assignment 如: +=, \*=, -=, ...
  - immutable object (i.e. int) 使用 augmented assignment
    ```
      a = 2
      a += 8  # new an object = 10, and redirect objective reference a to the new object
              # the original object (value = 2) will be collected as garbage
    ```
  - str, list 使用 augmented assigment (operator overloading)
    ```
    name = "Jimmy"
    name + "Chang"  # print "JimmyChang"
    name += "Chang" # print "Jimmy Chang"
    # list 使用 augmented assignment 時會將 iterable object 的每個資料項附加到清單中，若用 append 則可將 argment 當作當一資料項附加
    seed = ["s1","s2"]
    seed += 5     # error
    seed += [5]   # seed = ["s1","s2",5]
    seed += "got" # seed = ["s1","s2",5,"g","o","t"] because "got" is iterable
    ```
### 7. Input/Output
- input\(\) 取得使用者或從檔案導入\(EOF\)的輸入，按下 enter 鍵後完成輸入的動作
  ```
  total = 0
  count = 0
  while True:
    try:
      line = input()
      if line:
        number = int(line)
        total += number
        count += 1
    except ValueError as err:
      print(err)
      continue
    except EOFError:
      break
  if count:
    print("count=", count, "total=", total, "mean=", total/count)
  ```
python sum.py < data.dat

### 8. Function and Function Call
- def 會建立一個函式物件
  ```
  def functionName(argument):
    suite
    return a,b,c
  ```
- argument 可有可無。可以有回傳值，預設為 None，可用 return 回傳值
- python module 只是一個包含 python 程式碼的 \.py 檔案
  ```
  import moduleName # ignore extension
  moduleName.functionName # usage

  import random
  random.randit(1,6)
  ```
