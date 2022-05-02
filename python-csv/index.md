# Python 中如何处理 CSV 文件



本文主要介绍了 Python 开发当中如何处理 CSV 文件。由于平时开发中经常会使用到相关知识，故作小记以备不时之需。

## 1. 参数说明
delimiter：分隔符，默认值 ','。

quotechar：如果某个 item 中包含了分隔符，应该用 quotechar 把它包裹起来。

doublequote：如果某个 item 中出现了 quotechar 那么可以把整个内容用 quotechar 包裹，并把 quotechar double 一下用来做区分。

escapechar：如果不用 doublequote 的方法还可以用 escapechar 来辅助。

lineterminator：每一行的结束符，默认的是 \r\n。

quoting：可以选择任何时候都使用 quotechar 来包裹内容，或者是需要用到的时候再用，或者不用。

skipinitialspace：否忽略分隔符后面跟着的空格。


## 2. 读取 csv 文件

### 示例 1

```python
import csv

with open('xlxiao-data.csv') as csv_file:
    reader = csv.reader(csv_file)
    for row in reader:
        print row
```

- 注意：这里<font color=#FF0099>**使用的是 csv.reader， row 是 list 类型。**</font>


### 示例 2

```python
import csv

with open('xlxiao-data.csv') as csv_file:
    reader = csv.DictReader(csv_file)
    for row in reader:
        print row['name'], row['age']
```

- 注意：
  - 这里<font color=#FF0099>**使用的是 csv.DictReader， row 是 dict 类型。**</font>
  - 使用 csv.DictReader 读取的文件<font color=#FF0099>**必须包含 header。**</font>


## 3. 写入 csv 文件

### 示例 1

```python
import csv

with open('xlxiao-data.csv', 'w') as csv_file:
    writer = csv.writer(csv_file)
    writer.writerow(['xlxiao', '20'])
```

### 示例 2

```python
import csv

with open('xlxiao-data.csv', 'w') as csv_file:
    fieldnames = ['name', 'age']
    writer = csv.DictWriter(csv_file, fieldnames=fieldnames)

    writer.writeheader()
    writer.writerow({'name': 'xlxiao', 'age': 20})
```

## 4. 如何解决中文乱码问题

### 示例

```python
import csv
import codecs

with open('xlxiao-data.csv', 'w') as csv_file:
    csv_file.write(codecs.BOM_UTF8)
    writer = csv.writer(csv_file)
    writer.writerow(['xlxiao', '20'])
```

- <font color=#FF0099>**对文件进行 UTF8 编码**</font>，即可解决中文编码问题。

## 5. 参考文档
[1] https://docs.python.org/3/library/csv.html#id3.

[2] https://www.jianshu.com/p/0b0337df165a.
