# 第一章 培养Python思维

​编程语言的用法习惯是由用户定义的。这么多年来，Python社区使用Pythonic来形容Python这种独特的风格。这种风格并非受编译器的约束或强制形成的，而是在大家使用Python语言及合作的过程中积累下丰富经验，逐渐形成的。Python开发者并不喜欢复杂的代码，他们更喜欢选择简单、高可读，而非复杂的代码。(在你的解析器中输入import this，就可以查看The Zen of Python。)

​熟悉其他编程语言的程序员可能会尝试按照c++、Java或者他们熟悉的任何语言的编码风格去书写Python代码。对于Python小白来说，可能就需要花些时间去熟悉Python所能表达的众多概念。因此，了解Python中最常用的方法(即Python方法)是很重要的，这些模式将影响你编写的每一个程序。

## 第1条 了解你所使用的Python版本

​本书的巨大多数代码都将遵循Python3.7(发布于2018年6月)。此外，本书也会给出一些按照Python3.8(发布于2019年10月)语言规范编写的实例，用以突出展示即将广泛使用的Python3.8新特性。本书将不再包含Python2.

​很多电脑都会搭建包含多个版本的标准CPython运行环境。这就导致，在命令行中运行Python时，默认运行的Python版本并不清除，它有可能启动的是Python2.7，有时也会默认启动一些旧Python版本，例如Python2.6或Python2.5. 你可以使用--version参数，准确的找到所使用的版本号。

~~~shell
$ python --version
Python 2.7.10
~~~

​Python3可以直接用Python3启动：

~~~shell
$ python3 --version
Python 3.8.0
~~~

​你还可以通过检查sys内置模块中的值来确定你在运行时使用的Python版本

~~~python
print(sys.version_info)
sys.version_info(major=3, minor=8, micro=1, releaselevel='final', serial=0)
print(sys.version)
3.8.1 (tags/v3.8.1:1b293b6, Dec 18 2019, 23:11:46) [MSC v.1916 64 bit (AMD64)]
~~~

​Python 3由Python核心开发人员和社区积极维护，并不断得到改进。本书中介绍Python3的各种强大的新特性。大多数最常见的Python开源库都与Python 3兼容，并专注于Python 3。我强烈建议您在所有Python项目中使用ython 3。

​Python2将于2020年1月1日停止维护，所有的bug修复、安全补丁，以及特性特性都会停止维护。在此之后，再使用Python2进行编码将会是一件痛苦的事，因为官方已经不再维护。深度依赖Python2代码库的开发者可以考虑使用2to3(Python预装工具)和six(社区报，参将项目82)工具进行迁移。

**要点**

* Python3 是最新版本的Python，受到了很好的支持，你应该在你的项目中使用Python3进行开发。
* 在命令行运行Python时，一定要确认启动的Python版本是不是你说需要的。
* 避免再使用Python2进行开发，因为它已经于2020年1月1日停止维护。

## 第2条 遵循PEP8 风格指南

​Python Enhancement Proposal \#8，叫作PEP8，它是针对Python代码风格而编订的风格指南。只要你使用正确的语法，代码随便怎么写都可以，但是采用统一的编码风格能够使你的代码更易读、易懂。如果采用和其他Python开发者相同的代码风格，那么你就可以在社区中很顺利与大家完成协作项目。但是，即使您是唯一一个阅读您的代码的人，遵循样式指南也会使您以后更容易更改内容，并可以帮助您避免许多常见错误。

​PEP 8提供了关于如何编写清晰Python代码的丰富细节。它会随着Python语言的发展而不断更新。可以在[这里](https://www.python.org/dev/peps/pep-0008/)阅读完整的指南。以下是一些你应该一定要遵守的规则。

**空格**

​在Python中，空格在语法上是有意义的。Python程序员对空格对代码清晰度的影响特别敏感。遵循以下与空格相关的指导原则:

* 使用空格(space)表示缩进，而不是制表符(tab)
* 和语法相关的每一层缩进都要用4个空格表示
* 每行最多不超多79个字符
* 针对较长的表达式，当延伸到其他行时，应在正常缩进的基础上缩进额外的4个空格
* 在同一个py文件中，方法和类之间间隔两个空行
* 在同一个类中，方法间间隔一个空行
* 在字典中，在每个键和冒号之间不放空格，如果对应的值在同一行，则在其前面放一个空格
* 在变量赋值时，等号左右各放且仅放一个空格
* 对于类型注释，确保变量名和冒号之间没有分隔，并且在类型信息之前使用空格

**命名**

​PEP 8建议对代码中的不同部分采用独特的命名风格。这些约定使得在阅读代码是很容易区分哪个类型对应哪个名称。遵循下面的指导规则：

* 方法、变量及属性采用小写字母来拼写，各单词之间采用下划线连接，例如：lowercase_underscore
* 受保护的实例属性，采用一个下划线开头，例如：_leading_underscore
* 私有实例属性，采用两个下划线开头，例如：__double_leading_underscore
* 类(包括异常)命名时，每个单词的首字母大写，例如：CapitalizedWord
* 模块级别的常量，所有字母大写，各单词之间用下换线连接，例如：all_caps
* 类中的实例方法，应该把第一个参数命名为self，用来表示对象本身
* 类方法的第一个参数，应该命名为cls，用来表示类本身

**表达式与语句**

​The Zen of Python中讲到“每件事都应该有简单的方法，而且最好只有一种”。PEP 8就采用这个理念，来规范表达式和语句的写法。

* 使用内联否定(如果a不是b)代替肯定表达式的否定(如果a不是b)：**将否定逻辑直接内联到运算符中**（如 `is not`、`not in`、`!=`），而不是用 `not` 包裹一个肯定表达式
* 不要通过将长度与0比较来检查空容器或序列(如[]或")(如果len(somelist) == 0)。使用if not somelist这样的写法，因为Python会将空值自动表示为False
* 避免单行if语句、for和while循环，以及除复合语句之外的语句。为了清晰起见，将这些内容分散到多个行中
* 如果不能将表达式放在一行中，可以用圆括号将其括起来，并添加换行符和缩进，以使其更易于阅读
* 多行的表达式，应该用括号括起来，而不是使用\符号续行

**import**

​PEP 8对于怎么在代码中引入模块，给出下面的建议

* 把import 语句(包含from x import y)放在文件开头
* 引入模块时，应该使用绝对名称，而不应该根据相对路径引入。例如，引入bar包中的foo模块，应该完整地写出from bar import foo，即便当前路径为bar包中，也不应该简写成import foo
* 如果一定要用相对名称来编写impot语句，应该明确的写出from . import foo
* 文件中的import语句应该按顺序分成三部分：首先引入标准库中的模块，然后引入第三方模块，最后引入自定义模块。每一种都要按照字母表顺序引入。


​[Pylint](https://www.pylint.org)是一款流行的Python源码静态分析工具。他可以自动检查手册是的代码是否符合PEP 8风格指南，而且还能找出很多常见错误。很多IDE与编译器，也都办好这样的linting工具或者支持类似的插件。


* coding时，应当遵循 PEP 8 风格指南
* 与广大Python coder采用相同的代码风格，以便可以协作完成项目
* 使用一直的代码风格，代码的后续维护更容易


## 第3条 了解bytes与str的区别

​在Python中有两种类型表示字符序列：bytes、str。bytes实例包含的是原始数据，即8位的无符号值(通常按照ASCII编码规范显示)

~~~python
a = b'h\x65llo'
print(list(a))
[104, 101, 108, 108, 111]
print(a)
b'hello'
~~~

​str实例包含的是Unicode码点(code point，也叫代码点)，这些码点与人类语言中的文字字符对应。

~~~python
a = 'a\u0300 propos'
print(list(a))
['a', '̀', ' ', 'p', 'r', 'o', 'p', 'o', 's']
print(a)
à propos
~~~

需要注意的是，str实例并不一定非要用固定的方案编码成二进制数据，bytes实例也不一定非要按照某种固定的方案解码成字符串。要不Unicode数据转换成二进制数据，必须调用str的encode方法。要把二进制数据转换成Unicode数据，必须调用byres的decode方法。调用这些方法的时候，可以明确自己要使用的编码方案，也可以采用系统默认的方案，通常为UTF-8(有时候也不一定，下面会讲)。

​由于两种字符类型的不同，在Python代码中一般分为两种情况：
* 开发者需要操作包含UTF-8编码(或其他编码)的8 bit的原始序列
* 开发者需要操作不含特殊编码的Unicode字符串

​开发者通常需要两个辅助方法来完成不同情况下的转换，并确保输入值的类型与预期类型相符。
第一个辅助方法接受一个bytes 或 str 类型的实例，并返回一个str类型值“

```python
def to_str(bytes_or_str):
    if isinstance(bytes_or_str, bytes):
        value = bytes_or_str.decode('utf-8')
    else:
        value = bytes_or_str
    return value  # Instance of str


if __name__ == '__main__':
    print(repr(to_str(b'foo')))
    print(repr(to_str('bar')))
 
>>>
'foo'
'bar'
```

​第二个辅助方法接受一个bytes 或 str实例，并返回一个bytes类型值：

```python
def to_bytes(bytes_or_str):
    if isinstance(bytes_or_str, str):
        value = bytes_or_str.encode('utf8')
    else:
        value = bytes_or_str
    return value  # Instance of bytes


if __name__ == '__main__':
    print(repr(to_bytes(b'foo')))
    print(repr(to_bytes('bar')))
    
>>>
b'foo'
b'bar'
```

​在Python中处理原始8 bit值和Unicode字符串时，有两个需要注意的大问题。

​第一个问题是，bytes和str看起来以相同的方式工作，但是他们的实例却相互不兼容，所以在传递字符串序列时，必须要注意其类型。

​通过“+”操作，可以连接bytes和bytes类型，或者str和str类型，但是要分别连接两种类型：

```python
print(b'one' + b'two')
print('one' + 'two')

>>>
b'onetwo'
onetwo
```

​不可将str实例与bytes实例进行拼接操作“

```python
print(b'one' + 'two')

>>>
TypeError: can't concat str to bytes
```

​同样，不能将bytes实例和str实例进行拼接操作”

```python
print('one' + b'two')

>>>
TypeError: can only concatenate str (not "bytes") to str
```

​通过二进制操作，你也可以比较bytes和bytes实例，或者str和str类型实例：

```python
assert b'red' > b'blue'
assert 'red' > 'blue'
```

但是，不能比较str实例和bytes实例：

```python
assert 'red' > b'blue'

>>>
TypeError: '>' not supported between instances of 'str' and 'bytes'

```

​同样，不能比较bytes实例和str实例：

```python
assert b'red' > 'blue'

>>>
TypeError: '>' not supported between instances of 'bytes' and 'str'
```

​比较两个字符串完全相同(他们的ASCII编码均表示“foo”)，但分别属于bytes类型和str类型的实例时，通常会返回False：

```python
print(b'foo' == 'foo')

>>>
False
```

​两种类型的实例都可以出现在%操作符的右侧，用来替换左侧那个格式化字符串(format string)里面的%s：

```python
print(b'red %s' % b'blue')
print('red %s' % 'blue')

>>>
b'red blue'
red blue
```

​但是，如果格式字符串中表示bytes实例，就不能传递一个str类型的实例，因为Python不知道这个二进制文本应该用什么格式进行编码：

```python
print(b'red %s' % 'blue')

>>>
TypeError: %b requires a bytes-like object, or an object that implements __bytes__, not 'str'
```

​如果格式化字符串表示str实例，可以传递bytes实例，但是结果与预期不同：

```python
print('red %s' % b'blue')

>>>
red b'blue'
```

​这样写的代码，会让操作系统在bytes实例上面调用__ repr__方法(参见项目75)，然后用这次调用所得到的结果替换格式字符串里面的%s，因此程序会输出b'blue'，而不是预期输出的blue。

​第二个问题发生在操作文件句柄的时候，这里的句柄指的是内置的open方法放回的句柄。这样的句柄默认需要使用Unicode字符串操作，而不能采用原始的bytes。在Python2 中，通常会因此导致出错。例如，将二进制数据写入文件时，这个看似简单的代码就会出错：

```python
with open('data.bin', 'w') as f:
    f.write(b'\xf1\xf2\xf3\xf4\xf5')
    
>>>
TypeError: write() argument must be str, not bytes
```

​这个异常出现的原因是在调用open方法打开文件时采用了要求以文本形式写入的“w”模式，应当采用“wb”模式。当文件以文本模式打开时，write方法接受的包含Unicode数据的str实例，不是包含二进制数据的bytes实例。所以，我们在调用open方法将模式改为“wb”：

```python
with open('data.bin', 'wb') as f:
    f.write(b'\xf1\xf2\xf3\xf4\xf5')
```

​文件读操作时，同样会出现相似的问题。例如，当通过下面的代码尝试读取上面写好的二进制文件时：

~~~python
with open('data.bin', 'r') as f:
	data = f.read()

>>>
UnicodeDecodeError: 'gbk' codec can't decode byte 0xf5 in position 4: incomplete multibyte sequence
~~~

​导致读操作失败的原因是采用了操作文本数据的“r”模式，应当采用操作二进制数据的“rb”模式。当以文本模式操作句柄时，系统会采用默认的文本编码方式处理二进制数据。所以，上面的写法会让系统通过bytes.decode把数据解码成str字符串。然而对于大多数系统来说，默认的编码方案是UTF-8(这里调成了’gbk‘)，所以系统可能会把b'\xf1\xf2\xf3\xf4\xf5'当做UTF-8(这里是“gbk”)格式字符串去解码（但这串二进制并不能被当作 utf-8 来解码），于是就出现上述异常。为了修复这个异常，需要把模式改为“rb”：

```python
with open('data.bin', 'rb') as f:
    data = f.read()
assert data == b'\xf1\xf2\xf3\xf4\xf5'
```

​此外，也可以也可以在调用open方法时，通过encoding参数来指定编码格式，以确保平台特有的行为不会干扰代码运行的结果。例如，假设刚才写的二进制数据表示的是一个采用’cp1252‘标准(一种老式的Windows编码)进行字符串编码，可以这么写：

```python
with open('data.bin', 'r', encoding='cp1252') as f:
    data = f.read()
assert data == 'ñòóôõ'
```

​这样操作，异常虽然消失了，但是返回的字符串与读取原始字节数据非常不同。这个例子，告诉我们，要时刻注意当前操作系统默认的编码标准(可以通过命令查看： python3 -c 'import locale; print(locale.getpreferredencoding())')，看是否与期望的相同。当不太确定的时候，在调用open方法是通过encoding参数指定编码方式。

**要点**
* bytes包含的是 bit 值所组成的序列，str包含的是 Unicode码点 组成的序列
* 使用辅助方法来确保操作过程中输入时所期盼的字符串类型 ，是 8 bit的序列、UTF-8编码的字符串、Unicode码点还是其他
* bytes实例和str实例之间不能混用诸如>、\==、+、%等操作
* 如果想要读取或者写入二进制数据时，应该采用’rb‘ 或者 ’wb'模式
* 如果读取或写入Unicode数据时，应当注意操作系统默认的编码方式。可以通过在调用open方法时，指定encoding参数，来避免出错。

## 第4条 用支持插值的f-string取代C风格的格式字符串与str.format方法

​字符串在Python代码中普遍存在。在用户界面和命令行实用程序中呈现消息时要用，把数据写入文件或socket时要用，在Exception里异常详情时要用(见项目27)，在进行调试时(参见项目80和项目75)同样要用。

​格式化是将预定义的文本和数据值组合成人类可读的消息，并将该消息存储为字符串的过程。Python对字符串格式化处理有四种方法，这些方法都内置带语言和标准库中。这四种方法中，除了一种外，其他三个都存在严重缺项使我们应当理解和避免的，这里将在最后讲另一种方法。
​
Python中字符串格式化通常采用的方法是使用%。这个操作符左侧的文本模板叫做格式字符串(format string)，我们可以在操作符右边写上某个值或由多个值所构成的元组(tuple)，来替换格式字符串中的相关符号。例如，下面这段代码通过%操作符把难以阅读的二进制和十六进制数值，显示成十进制形式：

~~~python
a = 0b10111011
b = 0xc5f
print('Binary is %d, hex is %d' % (a, b))

>>>
Binary is 187, hex is 3167
~~~

​格式字符串中像%d这样的占位符会被右侧的数据替换。这样的格式化语法来自C语言的printf方法，Python语言以及其他编程语言都沿用了类似的方式。所以Python支持printf中%s、%x、%f等占位符，同时也支持控制小数点的位置、并支持填充和对其方式。对于许多Python小白来说都喜欢C风格的字符串格式化，因为他们比较熟悉这种方式并且这种方式比较简单。

​在Python中采用C风格字符串格式化会有四个问题。

​第一个问题是，如果你想改变%右侧元组中值的类型或顺序，可能会出现因类型转换不兼容而报错的问题。例如，下面简单的格式化表达是正确的：

~~~Python
key = 'my_var'
value = 1.234
formatted = '%-10s = %.2f' % (key, value)
print(formatted)

>>>
my_var = 1.23
~~~

​但是，如果交换key和value，运行时就会报错：

```python
key = 'my_var'
value = 1.234
formatted = '%-10s = %.2f' % (value, key)
print(formatted)

>>>
TypeError: must be real number, not str
```

​相似的，不改变右侧参数的位置，改变格式字符串中的位置，同样会报错：

```python
key = 'my_var'
value = 1.234
formatted = '%.2f = %-10s' % (key, value)
print(formatted)

>>>
TypeError: must be real number, not str
```

​为了避免这样的问题出现，就必须经常检查两侧的写法是否兼容。这个过程很容易出错，因为每次改完之后都要手工检查。

​第二个缺点是，在填充模板之前，经常需要先对准备写进去的值进行小的调整，但这样依赖，真个表达式就会很长，让人感觉很混乱。在这里，我列出了我的厨房储藏室的内容，而没有进行内联更改。

```python
pantry = [
    ('avocados', 1.25),
    ('bananas', 2.5),('cherries', 15),
]
for i, (item, count) in enumerate(pantry):
    print('#%d: %-10s = %.2f' % (i, item, count))
    
>>>
#0: avocados   = 1.25
#1: bananas    = 2.50
#2: cherries   = 15.00
```

​现在，我对正在格式化的值做了一些修改，以使打印的消息更有用。这将导致格式化表达式中的元组变得非常长，以至于需要跨多行分割，这损害了可读性:

~~~python
for i, (item, count) in enumerate(pantry):
	print('#%d: %-10s = %d' % (
		i + 1,
		item.title(),
		round(count)))

>>>
#1: Avocados = 1
#2: Bananas = 2
#3: Cherries = 15
~~~


第三个问题是，如果你想在一个格式化字符串中多次使用相同的值，你必须在右边的元组中重复它：

~~~python
template = '%s loves food. See %s cook.'
name = 'Max'
formatted = template % (name, name)
print(formatted)

>>>
Max loves food. See Max cook.
~~~

​如果必须对格式化的值重复一些小的修改，那么这尤其令人恼火，而且容易出错。例如，如果这次要填的是name.title()而不是name本身，就需要提醒自己，把所有的name都改成name.title()。如果有的地方改了，有的地方没改，那输出的结果可能就不一致了：

~~~python
name = 'brad'
formatted = template % (name.title(), name.title())
print(formatted)

>>>
Brad loves food. See Brad cook.
~~~

​为了结果这个问题，Python不仅可以对元组进行%操作，也可以对字典类型进行%操作。格式字符串里面的说明符与dict里面的键以相应的名称对应起来，例如%(keys)s这个说明符，意思就是用字符串(s)来表示dict里面名为key的那个键所对应的值。这里，通过这种方法解决刚才讲到的第一个缺点，也就是用%操作符两侧的顺序不匹配问题：

```python
key = 'my_var'
value = 1.234
old_way = '%-10s = %.2f' % (key, value)
new_way = '%(key)-10s = %(value).2f' % {
    'key': key, 'value': value}  # Original
reordered = '%(key)-10s = %(value).2f' % {
    'value': value, 'key': key}  # Swapped
print(old_way)
print(new_way)
print(reordered)

>>>
my_var     = 1.23
my_var     = 1.23
my_var     = 1.23
```

​在格式化字符串时使用字典也解决了上面讲到的第三个问题，也就是用同一个值替换多个格式化说明符的问题。改用这种写法之后，我们就不用在%右侧重复这个值了：

```python
name = 'Max'
template = '%s loves food. See %s cook.'
before = template % (name, name) # Tuple
template = '%(name)s loves food. See %(name)s cook.'
after = template % {'name': name} # Dictionary
print(before)
print(after)

>>>
Max loves food. See Max cook.
Max loves food. See Max cook.
```

​然而，字典格式化字符串的方法又会带来新的问题。例如上面提到的第二个关于格式化前对值的最小修改问题，字典格式化会让格式化表达式会变得更长，视觉上也更混乱，因为在格式化表达式之前，值的右侧会出现字典键和冒号操作符：

```python
pantry = [
    ('avocados', 1.25),
    ('bananas', 2.5),
    ('cherries', 15),
]
for i, (item, count) in enumerate(pantry):
    before = '#%d: %-10s = %d' % (
        i + 1,
        item.title(),
        round(count))
    after = '#%(loop)d: %(item)-10s = %(count)d' % {
        'loop': i + 1,
        'item': item.title(),
        'count': round(count),
    }
    print(before)
    print(after)

>>>
#1: Avocados   = 1
#1: Avocados   = 1
#2: Bananas    = 2
#2: Bananas    = 2
#3: Cherries   = 15
#3: Cherries   = 15
```

​在格式化表达式时使用字典还会增加冗长，这是Python中c风格表达式格式化的问题#4。每个键必须至少被指定两次 —— 一次是在格式说明符中，一次是在字典中作为键，还有一次可能是在包含字典值的变量名中:

```python
soup = 'lentil'
formatted = 'Today\'s soup is %(soup)s.' % {'soup': soup}
print(formatted)

>>>
Today's soup is lentil.
```

​除了重复的字符外，这种冗余会导致使用字典的格式化表达式很长。这些表达式通常必须跨多行，格式字符串跨多行连接，而字典赋值在格式化中每个值只有一行:

```python
menu = {
    'soup': 'lentil',
    'oyster': 'kumamoto',
    'special': 'schnitzel',
}
template = ('Today\'s soup is %(soup)s, '
            'buy one get two %(oyster)s oysters, '
            'and our special entrée is %(special)s.')
formatted = template % menu
print(formatted)

>>>
Today's soup is lentil, buy one get two kumamoto oysters, and our special entrée is schnitzel.
```

​要理解这个格式表达式将输出什么样的结果，必须在格式字符串和字典的行之间来回观察。这种脱节使得很难发现错误，如果需要在格式化之前对任何值进行小的修改，可读性就会变得更糟。

​一定会有更好的办法才对！

**内置的format方法与str类的format方法**

​Python3中添加了高级字符串格式化(advanced string formatting)机制，它的表达能力比C风格采用的%操作要强。针对单个Python值，通过内置的format方法可以很好的实现所需。例如，通过逗号表示千位分隔符，^表示居中对齐：

```python
a = 1234.5678
formatted = format(a, ',.2f')
print(formatted)
b = 'my string'
formatted = format(b, '^20s')
print('*', formatted, '*')

>>>
1,234.57
*      my string       *
```

​针对str类型，使用内置的format方法可以同时格式化对个值。这种方法，摒弃了C风格的%，而是采用{}充当占位符。默认情况下，格式字符串中的占位符被传递给format方法的相应位置参数替换，这些参数按它们出现的顺序传递：

~~~python
key = 'my_var'
value = 1.234
formatted = '{} = {}'.format(key, value)
print(formatted)

>>>
my_var = 1.234
~~~

​在每个占位符中，你可以选择提供一个冒号，后面跟着格式说明符，以自定义值如何转换为字符串(请参阅帮助('FORMATTING')了解全部选项):

~~~python
key = 'my_var'
value = 1.234
formatted = '{:<10} = {:.2f}'.format(key, value)
print(formatted)
>>>
my_var = 1.23
~~~

​可以这样理解这种格式化的方法：系统把str.format方法接受到的每个值传递给内置的format方法，并找到这个值在字符串中对应的{}，同时将{}里面写的格式也传递给format方法，例如系统处理value时，传的就是format(value,'.2f')。然后，系统会把format方法所返回的结果卸载真个格式化字符串{}所在的位置。另外。每个类都可以通过__ format__这个内置方法制定相应的逻辑，这样的话format方法在把类实例转换成字符串时，就会按照这个逻辑转换。

​C风格格式化采用%来应道格式说明符，所以如果这个符号按照原样输出，就必须转义，也就是连写两个 `%%` 。同理，在调用str.format的时候，如果想把str中 `{` 、 `}` 输出，也需要转义：

~~~python
print('%.2f%%' % 12.5)
print('{} replaces {{}}'.format(1.23))
>>>
12.50%
1.23 replaces {}
~~~

​在花括号内，还可以指定传递给format方法用于替换占位符的参数的位置索引。这允许更新格式字符串来重新排序输出，而不需要你也改变格式表达式的右边，从而解决上面的第一个问题:

~~~python
key = 'my_var'
value = 1.234
formatted = '{1} = {0}'.format(key, value)
print(formatted)
>>>
1.234 = my_var
~~~

​同样的位置索引也可以在格式字符串中被多次引用，而不需要将值多次传递给格式方法，这从上到下解决了第三个问题：

~~~python
formatted = '{0} loves food. See {0} cook.'.format(name)
print(formatted)
>>>
Max loves food. See Max cook.
~~~

​不幸的是，新的格式方法并不能解决上面的第二问题，当需要在格式化值之前对其进行小的修改时，会使代码难以阅读。新旧选项之间的可读性几乎没有差别，它们也同样繁杂：

~~~python
pantry = [
    ('avocados', 1.25),
    ('bananas', 2.5),
    ('cherries', 15),
]
for i, (item, count) in enumerate(pantry):
    old_style = '#%d: %-10s = %d' % (
    i + 1,
    item.title(),
    round(count))
    new_style = '#{}: {:<10s} = {}'.format(
    i + 1,
    item.title(),
    round(count))
    print(old_style)
    print(new_style)

>>>
#1: Avocados   = 1
#1: Avocados   = 1
#2: Bananas    = 2
#2: Bananas    = 2
#3: Cherries   = 15
#3: Cherries   = 15
~~~

​str.format方法中使用的说明符还有更高级的选项，比如在占位符中使用字典键和列表索引的组合，以及将值强制转换为Unicode和repr字符串:

~~~python
menu = {
    'soup': 'lentil',
    'oyster': 'kumamoto',
    'special': 'schnitzel',
}
formatted = 'First letter is {menu[oyster][0]!r}'.format(
menu=menu)
print(formatted)
>>>
First letter is 'k'
~~~

​		但是这些特性并不能帮助减少第四个问题中的重复键的冗余。例如，这里我比较了在C风格的格式化表达式中使用字典的冗长，以及向format方法传递关键字参数的新风格

```python
    old_template = (
        'Today\'s soup is %(soup)s, '
        'buy one get two %(oyster)s oysters, '
        'and our special entrée is %(special)s.')
    old_formatted = old_template % {
        'soup': 'lentil',
        'oyster': 'kumamoto',
        'special': 'schnitzel',
    }
    new_template = (
        'Today\'s soup is {soup}, '
        'buy one get two {oyster} oysters, '
        'and our special entrée is {special}.')
    new_formatted = new_template.format(
        soup='lentil',
        oyster='kumamoto',
        special='schnitzel',
    )
    print(old_formatted)
    print(new_formatted)
>>>
Today's soup is lentil, buy one get two kumamoto oysters, and our special entrée is schnitzel.
Today's soup is lentil, buy one get two kumamoto oysters, and our special entrée is schnitzel.
```

​这种风格稍微不那么混乱，因为它消除了字典中的一些引号和格式说明符中的一些字符，但它几乎没有什么吸引力。此外，在占位符中使用字典键和索引的高级特性只提供了Python的一小部分表达功能。这种表达性的缺乏是如此有限，以至于从整体上削弱了str格式方法的价值。

​考虑到这些缺点和C风格格式表达式仍然存在第二和第四个问题，通常避免使用str.format。当然，我们还是必须掌握新的格式说明符所使用的这套迷你语言(mini language)，我们可以在str的{}里面按照这套迷你语言的规则来指定冒号右侧的格式。系统内置的format方法也会使用这套规则。除此之外，str.format方法就只有历史意义了，他让我们可以在这套机制的基础之上学习Python新引入的f-string。

**差值格式字符串**

​Python3.6添加了新的特性--插值格式字符串(interpolated format string，简写f-string)，这一种新的语法将会解决上面出现的所有问题。这种语法要求在格式字符串前添加前缀字母f，和bytes类型的字符串前面的b，或者表示原始字符串(未经转义)的前缀r是一样的。

​f-string让格式字符串的表达能力发挥到了极致，他彻底解决了上面的第四个问题：键名导致程序冗余。我们不用像C风格那样专门定义dict，也不用再像调用str.format方法那样专门把值传给某个参数，这次可以直接在f-string的{}里面引用当前Python里所以的变量名，从而达到简化目的：

~~~python
key = 'my_var'
value = 1.234
formatted = f'{key} = {value}'
print(formatted)
>>>
my_var = 1.234
~~~

​str.format方法所支持的那套秘密语言，也就是在{}内的冒号右侧所采用的那套规则，现在也可以用到f-string中，而且可以向之前使用str.format那样，通过！符号把值转化为Unicode和repr形式的字符串：

~~~python
formatted = f'{key!r:<10} = {value:.2f}'
print(formatted)
>>>
'my_var' = 1.23
~~~

>[!note] f-string 的转换标志
>- !r → repr(value)
>- !s → str(value)（默认行为，可省略）
>- !a → ascii(value)（Python 3 新增）

​采用f-string要比C风格的%操作以及str.format方法都更加简短。这里，从短到长的顺序把这种方法统一展示，并且将等号右侧对齐，以便更好的观察：

```python
key = 'my_var'
value = 1.234
f_string = f'{key:<10} = {value:.2f}'
c_tuple = '%-10s = %.2f' % (key, value)
str_args = '{:<10} = {:.2f}'.format(key, value)
str_kw = '{key:<10} = {value:.2f}'.format(key=key,
                                          value=value)
c_dict = '%(key)-10s = %(value).2f' % {'key': key,
                                       'value': value}

print(f_string)
print(c_tuple)
print(str_args)
print(str_kw)
print(c_dict)

>>>
my_var     = 1.23
my_var     = 1.23
my_var     = 1.23
my_var     = 1.23
my_var     = 1.23
```

​f-string还允许将完整的Python表达式放入占位符括号中，通过允许对使用简洁语法格式化的值进行小的修改，从上面解决第二个问题。用c风格的格式和str.format方法实现多行现在很容易就能在一行中实现：

```python
pantry = [
    ('avocados', 1.25),
    ('bananas', 2.5),
    ('cherries', 15),
]
for i, (item, count) in enumerate(pantry):
    old_style = '#%d: %-10s = %d' % (
        i + 1,
        item.title(),
        round(count))
    new_style = '#{}: {:<10s} = {}'.format(
        i + 1,
        item.title(),
        round(count))
    f_string = f'#{i + 1}: {item.title():<10s} = {round(count)}'
    print(new_style)
    print(new_style)
    print(f_string)

>>>
#1: Avocados   = 1
#1: Avocados   = 1
#1: Avocados   = 1
#2: Bananas    = 2
#2: Bananas    = 2
#2: Bananas    = 2
#3: Cherries   = 15
#3: Cherries   = 15
#3: Cherries   = 15
```

​你也可以向C语言相邻字符串(adiacent-string concatenation)拼接那样，把f-string写成多行，这样看起来会更加清晰。尽管，这样写要比单行更长，当仍然比其他多行的写法要好很多：

```python
pantry = [
    ('avocados', 1.25),
    ('bananas', 2.5),
    ('cherries', 15),
]
for i, (item, count) in enumerate(pantry):
    print(f'#{i + 1}: '
          f'{item.title():<10s} = '
          f'{round(count)}')
 >>>
#1: Avocados   = 1
#2: Bananas    = 2
#3: Cherries   = 15
```

​Python表达式也可以出现在格式说明符选项中。例如通过使用变量而不是在格式字符串中硬编码来参数化要打印的数字数：

```python
places = 3
number = 1.23456
print(f'My number is {number:.{places}f}')

>>>
My number is 1.235
```

​f-string所提供的表达性、简洁性和清晰性的结合，使其成为Python程序员的最佳内置选项。当需要将值格式化为字符串时，推荐使用f-strings。

**要点**

* 使用%操作符的c风格格式字符串会遇到各种陷阱和冗长的问题。
* str.format方法在其格式化说明符迷你语言中引入了一些有用的概念，但是它重复了c风格格式字符串的错误，应该加以避免。
* F-string是一种用于将值格式化为字符串的新语法，它解决了c风格格式字符串的最大问题。
* F-string简洁但功能强大，因为它们允许任意Python表达式直接嵌入到格式说明符中。

## 第5条 用辅助方法代替复杂的表达式

​Python简洁的语法使得编写实现大量逻辑的单行表达式变得很容易。例如，假设我想解码来自URL的查询字符串。这里，每个查询字符串参数表示一个整数值：

```python
from urllib.parse import parse_qs
my_values = parse_qs('red=5&blue=0&green=',keep_blank_values=True)
print(repr(my_values))

>>>
{'red': ['5'], 'blue': ['0'], 'green': ['']}
```

​在解析字符串参数时，有的可能有多个参数，有的可能只是单一参数，有的可能是空白值，可能还会遇到一些没有提供参数的情况。在结果字典上使用get方法将在每种情况下返回不同的值：

```python
from urllib.parse import parse_qs
my_values = parse_qs('red=5&blue=0&green=',keep_blank_values=True)
# print(my_values)
# print(repr(my_values))
print('Red: ', my_values.get('red'))
print('Green: ', my_values.get('green'))
print('Opacity: ', my_values.get('opacity'))
>>>
Red:  ['5']
Green:  ['']
Opacity:  None
```

​当参数不存在或者为空时，可以给定默认值0。对于这样的情况，采用Boolean表达式是更好的选择，不值得写完成的if语句或者辅助方法。

Python的Boolean表达式这种语法写起来更简单，Python会把空字符串、空列表以及0都当做False。因此，只需要把get方法找到的结果放在or操作符的左边，并在右边写上0就可以了。这样的话，只要左面的表达式为False，name整个表达式的值就自然被评估为右边那个表达式的值，也就是0.

```python
red = my_values.get('red', [''])[0] or 0
green = my_values.get('green', [''])[0] or 0
opacity = my_values.get('opacity', [''])[0] or 0
print(f'Red: {red!r}')
print(f'Green: {green!r}')
print(f'Opacity: {opacity!r}')

>>>
Red: '5'
Green: 0
Opacity: 0
```

​red这种情况正常返回，因为red值在my_values字典中，他的值就是在list列表中的一个字符串值。Python会把吧这种情况默认为True，所以red值就是or左侧的部分。

green能够读取是因为green的值是list列表中的空字符串。空字符串，Python默认为False，green的值就是or右侧的0.

opacity能够读取是因为：opacity不在my_values字典中，Python会默认返回第二个值[''](参见第16条)。默认值也是只有空字符串的列表，所以当opacity在字典中找不到时和green一样。

然而，这个表达式很难读懂，而且它仍然没有完成我们的所有需求。如果还希望确保所有的参数都转换为整数，以便可以立即在数学表达式中使用，还需要将内置方法int写进去，才能将字符串解析为int：

~~~python
red = int(my_values.get('red', [''])[0] or 0)

~~~

这样更加难读，并且看起还更加别扭。这种代码很可怕，如果你是第一次阅读，就需要把整个表达式逐层拆开，才能明白表达啥意思，这很浪费时间。代码可以下的短一些

并非都要写在一行：

~~~Python
red_str = my_values.get('red', [''])
red = int(red_str[0]) if red_str[0] else 0
~~~

这样写更好。当逻辑不是太复杂，if/else条件表达式会让代码更清晰。但是在这个例子中，不如写一个完整的if/else表达式结构清晰。对比实现逻辑的几种展开表达式，刚才的那种浓缩式的写法就显得复杂：

~~~python
green_str = my_values.get('green', [''])
if green_str[0]:
	green = int(green_str[0])
else:
	green = 0
~~~

如果你需要重复的使用这种逻辑，可以写一个辅助方法：

~~~python
def get_first_int(values, key, default=0):
	found = values.get(key, [''])
	if found[0]:
		return int(found[0])
return default

~~~

这样的代码要比采用or的表达式或者if/else结构都更加清晰易懂。

~~~python
green = get_first_int(my_values, 'green')
~~~

一旦表达式变得复杂，就应该考虑将它们分割成更小的部分，并将逻辑转移到帮助方法中。这样所获得的可读性总是超过所获得的简洁性。避免复杂表达式的语法让你陷入像这样的混乱。遵循DRY原则:不要重复自己。

>[!note] DRY原则
> Don’t Repeat Yourself  “不要重复你自己”
> 系统中**每一处知识或行为都必须有单一、明确、权威的表示**。  
> 凡是你写第二遍的代码、配置、文档或流程，都应该被抽象、共享或自动生成。
> ---
>为什么重要
>1. 维护成本：重复意味着改一处要改 N 处，容易遗漏。
>2. 一致性：同一逻辑的不同副本可能逐渐产生差异。
>3. 可靠性：副本越多，出 Bug 的概率越高。 
>4. 效率：复制粘贴的开发速度是假速度，后期还债更慢。
>---
>常见违反与对策
>- 多段相似代码：提取函数/类/模板方法
>- 多处硬编码常量：声明常量或配置文件
>- 多份 API 文档：用 Swagger/OpenAPI 自动生成
>- 前后端校验逻辑重复：共享校验库或 Schema
>- 多环境配置差异：统一配置模板 + 占位符替换
>- 重复造轮子：直接依赖成熟库或内部公共库

**要点**
* Python语法很容易把复杂的意思放在同一行表达，这样写很难懂
* 复杂的表达式，尤其是要重复使用的复杂表达式，应该放到辅助方法中
* 用if/else条件表达式，要比or、and写成的Boolean更好懂

## 第6条 把数据结构直接拆分到多个变量里,不要专门通过下标访问

​Python内置的元组类型可以创建不可变的序列，把许多元素依次保存起来。最简单的方法是只用元组保存两个值，例如字典里的键值对：
```python
snack_calories = {
	'chips': 140,
	'popcorn': 80,
	'nuts': 190,
}
items = tuple(snack_calories.items())
print(items)

>>>
(('chips', 140), ('popcorn', 80), ('nuts', 190))
```

​可以通过数字索引直接访问元组里的值：
```python
item = ('Peanut butter', 'Jelly')
first = item[0]
second = item[1]
print(first, 'and', second)

>>>
Peanut butter and Jelly
```

​一旦建立了元组，就不能够在通过索引去重新赋值：

```python
pair = ('Chocolate', 'Peanut butter')
pair[0] = 'Honey'

>>>
    pair[0] = 'Honey'
TypeError: 'tuple' object does not support item assignment
```

​Python同样拥有解包的语法，通过这种语法只需要一个语句就可以把元组里面的元素赋值给多个变量。解包元组时，并非是要修改元组本身，并且元组本身是不可更改的，但是解包后赋值元素的变量是不一样的。例如，如果元组是确定的，就可以直接通过解包操作把元组的元素赋值给两个变量名，而不通过索引：
~~~python
item = ('Peanut butter', 'Jelly')
first, second = item # Unpacking
print(first, 'and', second)
>>>
Peanut butter and Jelly
~~~

​通过解包操作来赋值要比通过下标去访问元组内的元素更加简洁，并通常仅需要几行代码。解包操作的左侧也可以是列表、序列、或任意深度的可迭代对象(iterable)。这里并不推荐按照下面这么写代码，但是知道它的原理是非常重要的：

~~~python
favorite_snacks = {
	'salty': ('pretzels', 100),
	'sweet': ('cookies', 180),
	'veggie': ('carrots', 20),
}
(
	(type1, (name1, cals1)),
	(type2, (name2, cals2)),
	(type3, (name3, cals3))
) = favorite_snacks.items()

print(f'Favorite {type1} is {name1} with {cals1} calories')
print(f'Favorite {type2} is {name2} with {cals2} calories')
print(f'Favorite {type3} is {name3} with {cals3} calories')

>>>
Favorite salty is pretzels with 100 calories
Favorite sweet is cookies with 180 calories
Favorite veggie is carrots with 20 calories
~~~

​对于Python小白来说，可能还不知道通过解包操作还可以交换两个变量的值，而不专门创建临时变量。这里使用典型的索引语法在列表中的两个位置之间交换值，这是升序排序算法的一部分：

```python
def bubble_sort(a):
    for _ in range(len(a)):
        for i in range(1, len(a)):
            if a[i] < a[i-1]:
                temp = a[i]
                a[i] = a[i-1]
                a[i-1] = temp
names = ['pretzels', 'carrots', 'arugula', 'bacon']
bubble_sort(names)
print(names)

>>>
['arugula', 'bacon', 'carrots', 'pretzels']
```

​然而，通过解包语法，就可以通过简单的一行实现交换：

~~~python
def bubble_sort(a):
    for _ in range(len(a)):
        for i in range(1, len(a)):
            if a[i] < a[i-1]:
                a[i-1],a[i] = a[i], a[i-1]

names = ['pretzels', 'carrots', 'arugula', 'bacon']
bubble_sort(names)
print(names)

>>>
['arugula', 'bacon', 'carrots', 'pretzels']
~~~

​这种交换变量的原理是：Python在处理赋值操作时，要先对等号右侧赋值，于是，它会创建一个临时的元组，把a[i] 与a[i-a]这两个元素放到临时的元组中。例如，第一次进入循环内部是，这两个元素分别是‘carrots’与‘pretzels’，于是，系统就创建临时元组(‘carrots’,‘pretzels’)。然后，Python会对这个临时元组进行解包操作，把临时元组里面的两个元素分别放到等号左边的两个地方，于是，‘carrots’就会把a[i-1]里面原有的‘pretzels’替换，‘pretzels‘也会把a[i]里面原有的’carrots‘替换条。现在，出现在a[0]的位置就是’carrots‘，出现在a[1]位置的就是’pretzels‘。做完解包操作后，系统会回收这个临时元组。

>[!note] 两种方法在时空间上的对比
> 解包交换 `a, b = b, a`
>源代码
>```python
>a, b = b, a
>```
>字节码（CPython 3.11，`-m dis` 输出，已去行号）
>```
  LOAD_FAST                1 (b)     # 把 b 压栈
  LOAD_FAST                0 (a)     # 把 a 压栈
  ROT_TWO                           # 交换栈顶两个引用
  STORE_FAST               0 (a)     # 栈顶 -> a
  STORE_FAST               1 (b)     # 次栈顶 -> b
>```
>- **仅使用 CPython 的求值栈**（stack），**不产生新的 PyObject（tuple 等）**。   
>- **时间复杂度 O(1)**，**额外内存 0 字节**（栈空间不计入 Python 堆内存）。
>---
>引入临时变量 `tmp = a; a = b; b = tmp`
>源代码
>```python
tmp = a
a   = b
b   = tmp
>```
字节码
>```
  LOAD_FAST                0 (a)     # 把 a 压栈
  STORE_FAST               2 (tmp)   # 栈顶 -> tmp
>
  LOAD_FAST                1 (b)     # 把 b 压栈
  STORE_FAST               0 (a)     # 栈顶 -> a
>  
  LOAD_FAST                2 (tmp)   # 把 tmp 压栈
  STORE_FAST               1 (b)     # 栈顶 -> b
>```
>- **多出一个局部变量 `tmp`**，需要在**局部变量数组**里多占 1 个槽位。   
>- **额外一次 STORE_FAST + LOAD_FAST**，**多 2 条指令**，**微基准测试**里通常慢 5%–10%（但属于纳秒级差异）。
>- **时间复杂度仍为 O(1)**，但**局部变量表**多 1 个引用，**内存占用略大**。
>---
>额外细节：为什么解包不会创建 tuple？
>- **早期 CPython（≤3.7）** 在 `a, b = b, a` 时确实会**先生成临时 tuple** 再拆包，内存占用略高。   
>- **3.8 之后** 引入了专门的字节码 `ROT_TWO`、`ROT_THREE`、`ROT_FOUR`，以及更通用的 `COPY`、`SWAP`（3.11），**直接在栈上旋转值**，**无临时 tuple**。
>- 因此**现代 Python 中解包交换已是零额外内存**。
​

解包操作还有一个重要的用法，可以用在for循环或者类似的结构中（例如推导与生成表达式，第27条），把复杂的数据拆分到相关的变量之中。下面这段代码没有采用解包操作，而是采用了传统的写法迭代snacks列表里面的元素。
```python
snacks = [('bacon', 350), ('donut', 240), ('muffin', 190)]
for i in range(len(snacks)):
    item = snacks[i]
    name = item[0]
    calories = item[1]
	print(f'#{i+1}: {name} has {calories} calories')

>>>
#1: bacon has 350 calories
#2: donut has 240 calories
#3: muffin has 190 calories
```

​这虽然能获取到正确结果，但是却很乱，因为snacks结构本身就是复杂列表，每一个元素都是一个元组，所以必须逐层访问才能查到具体的数据。下面换一种写法，首先调用内置的enumerate方法(参见第7条)获取当前要迭代的元组，然后针对这个元组进行解包，这样就可以直接获取到具体的name与calories值：

~~~python
for rank, (name, calories) in enumerate(snacks, 1):
	print(f'#{rank}: {name} has {calories} calories')
>>>
#1: bacon has 350 calories
#2: donut has 240 calories
#3: muffin has 190 calories
~~~

​这是Python风格的写法，不需要再通过下标逐层访问了。这种写法简短且容易理解。

Python的解包操作可以用在多个方面，例如构建列表(第13条)、给方法设计参数列表(第22条)、传递关键字参数(第23条)、接收多个返回值(第19条)等。

明智的使用解包操作，可以避免使用下标带来的麻烦，并且能让代码结果跟简单。

**要点**

* 解包操作是一种特殊的Python语法，只需要一行代码，就能把数据结构中的多个元素赋给多个值
* 解包操作在Python中运用广泛，凡是可迭代的对象都可以拆分，无论里面还有多少层迭代结构
* 尽量通过解包操作而不是下标访问数据，这能时代更简洁、明了

## 第7条 尽量使用enumerate取代range

​Python 内置的range方法适合迭代一系列整数。

```python
from random import randint
random_bits = 0
for i in range(32):
    if randint(0, 1):
        random_bits |= 1 << i

print(bin(random_bits))

>>>
0b10100010100010110001100001010111
```

​当有一个数据结构要迭代时，比如字符串列表，可以直接在序列上循环：

~~~python
flavor_list = ['vanilla', 'chocolate', 'pecan', 'strawberry']
for flavor in flavor_list:
	print(f'{flavor} is delicious')

>>>
vanilla is delicious
chocolate is delicious
pecan is delicious
strawberry is delicious
~~~

​当迭代一个列表数据时，经常会需要知道当前元素在列表中的位置。例如，遍历最喜欢的冰淇淋时，还要打印出他们的排行。可以通过传统的range方式：

~~~python
flavor_list = ['vanilla', 'chocolate', 'pecan', 'strawberry']
for i in range(len(flavor_list)):
	flavor = flavor_list[i]
	print(f'{i + 1}: {flavor}')
>>>
1: vanilla
2: chocolate
3: pecan
4: strawberry
~~~

​与遍历flavor_list或range的其他例子相比，这看起来有些笨拙。我必须知道列表的长度。必须对数组下标，且多重步骤使它更难阅读。

Python提供了内置方法enumerate来解决这个问题。enumerate方法能够把任何一种迭代器(iterator)封装成惰性生成器(lazy generator，见第30条)。当每次迭代的时候，enumerate产生对循环索引和给定迭代器的下一个值。这里，通过内置的next方法手动推进enumerate所返回的iterator，来演示enumerate的原理：

```python
flavor_list = ['vanilla', 'chocolate', 'pecan', 'strawberry']
it = enumerate(flavor_list)
print(next(it))
print(next(it))
>>>
(0, 'vanilla')
(1, 'chocolate')
```

​enumerate输出的每一对数据，还可以通过for循环解包(见第6条)给两个变量。这样会使代码更清晰：

~~~python
for i, flavor in enumerate(flavor_list):
	print(f'{i + 1}: {flavor}')
>>>
1: vanilla
2: chocolate
3: pecan
4: strawberry
~~~

​另外，还可通过enumerate的第二个参数指定起始序号，这样就不用在每次打印的时候去调整了。例如，本例可以从1开始计算：

```python
flavor_list = ['vanilla', 'chocolate', 'pecan', 'strawberry']
for i, flavor in enumerate(flavor_list,1):
    print(f'{i}: {flavor}')
    
>>>
1: vanilla
2: chocolate
3: pecan
4: strawberry
```

**要点**

* enumerate方法可以通过简洁的代码迭代iterator，而且可以指出循环的序号
* 直接用enumerate方法而非通过range方法指定下标的取值范围，再用下标去访问序列
* 可以通过enumerate的第二个参数指定起始序号(默认为0)

## 第8条 使用zip方法同时遍历两个迭代器

​在写Python代码时，经常会根据某份列表中的对象创建出许多相关的新列表。通过使用列表推导式，可以把表达式运用到源列表的每个元素，从而派生出一份派生列表(见第27条)：

~~~python
names = ['Cecilia', 'Lise', 'Marie']
counts = [len(n) for n in names]
print(counts)
>>>
[7, 4, 5]
~~~

​派生列表中的元素与源列表中对应位置上的元素有着一定的关系。如果相同时遍历这两份列表，那可以根据源列表的长度做迭代：

```python
longest_name = None
max_count = 0
names = ['Cecilia', 'Lise', 'Marie']
counts = [len(n) for n in names]
for i in range(len(names)):
    count = counts[i]
    if count > max_count:
        longest_name = names[i]
        max_count = count
print(longest_name)

>>>
Cecilia
```

​这样写的问题在于，整个循环语句看起来很乱。names和counts变量的索引让代码很难读。可以使用enumerate(见第7条)可以改善这个问题，但是治标不治本

```python
longest_name = None
max_count = 0
names = ['Cecilia', 'Lise', 'Marie']
counts = [len(n) for n in names]
for i, name in enumerate(names):
    count = counts[i]
    if count > max_count:
        longest_name = name
        max_count = count
print(longest_name)
>>>
Cecilia
```

​为了让代码更清晰，Python提供了zip内置方法。zip方法能够将两个或更多的iterator封装成惰性生成器(lazy generator)。每次迭代时，它会分别从这些迭代器里获取各自的下一个元素，并把这些值放在一个元组里。而这个元组可以通过for循环解包到不同变量中(见第6条)。这样写代码，比通过下标遍历列表更清晰：

```python
longest_name = None
max_count = 0
names = ['Cecilia', 'Lise', 'Marie']
counts = [len(n) for n in names]
for name, count in zip(names, counts):
    if count > max_count:
        longest_name = name
        max_count = count
print(longest_name)

>>>
Cecilia
```

​zip每次只从它封装的迭代器中取一个元素，所以即便源列表很长，程序也不会因为占内存多而崩溃。

​但是，当输入迭代器的长度不同时，要注意zip的操作了。例如，当我在names列表中新增了一个元素而忘记更行counts列表了。在通过zip去遍历两个列表时，输出结果就会异常：

```python
for name,count in zip(names,counts):
    print(name)
    
>>>
Cecilia
Lise
Marie
```

​新元素‘Rosalind’并没有打印出来。为什么呢？这就要了解zip方法的原理了。zip方法

会持续迭代生成元组，直到任何一个迭代器处理完毕，就不在继续往下运行了。它的输出长度和最短的输入长度相同。当已知的迭代器的长度相同时，它可以很好的运行。

​但是，很多情况下，列表的长度并不相同，zip方法提前终止会导致结果与预期不符。如果无法确定这些列表的长度是否相同，那就不要把他们传个zip方法，而是采用itertools模块中的zip_longest方法：

```python
import itertools
names = ['Cecilia', 'Lise', 'Marie']
counts = [len(n) for n in names]
names.append('Rosalind:')
for name, count in itertools.zip_longest(names, counts):
    print(f'{name}: {count}')

>>>
Cecilia: 7
Lise: 4
Marie: 5
Rosalind: None
```

​如果列表已经遍历完了，zip_longest会用当初传给fillvalue参数的那个值补空缺(本例中空缺的字符串‘Rosalind’的长度值)，默认是None。

**要点**

* 内置的zip函数可以同时遍历多个迭代器
* zip会创建惰性生成器，让它每次只生成一个元组，所以无论输入的数据有多长，他都是一个一个处理
* 如果提供的迭代器长度不一致，但任意一个迭代完毕，zip停止运行
* 如果想按照最长的迭代器遍历，那就使用内置itertools模块的zip_longest方法

## 第9条  避免在for和while循环后写else块

​Python的循环有一项大多数编程语言都不支持的特性：可以在整个循环后立即写一个else块：

```python
for i in range(3):
    print("Loop",i)
else:
    print("Else block!")
    
>>>
Loop 0
Loop 1
Loop 2
Else block!
```

​奇怪的是，在整个循环结束后，尽然会执行else块。为什么这种情况下还叫做"else”呢？这应该是叫做“and”才对。在if/else结构中，else意味着前面的没有被执行或出现才执行else。在try/except结构中，except也是同样的意思：知道try里面的执行失败才执行except里面的语句。

try/except/else结构的理念（参见第65条）与他们相似，他们都是指：如果没有异常需要处理，那就执行try里面的语句。try/finally结构中同样很直观，这种结构表示：不论前面的代码块执行情况如何，都要执行finally中的代码块。

了解了else，except，finally在Python的用法后，Python小白可能会同样觉着for/else结构中的else也是这个意思，即如果循环没有从头到尾执行完，就执行else代码块。但事实却相反，如果循环没有执行完毕或者说提前跳出了循环，那么else代码块就不会执行。在循环中使用break语句实际上会跳过else代码块：

```python
for i in range(3):
    print("Loop", i)
    if i == 1:
        break
else:
    print("Else block!")
 
>>>
Loop 0
Loop 1
```

​另外一种意想不到的是，如果循环体是空的，程序会立即执行else代码块：

```python
for x in []:
    print("Never runs")
else:
    print("Else block!")
>>>
Else block!
```

while循环也是这样，如果首次遇到False，程序会立即运行else代码块:

~~~python
while False:
    print("Never runs")
else:
    print("Else block!")
>>>
Else block!
~~~

​这样设计的原因是，在利用循环搜索东西时发挥它的作用。例如，要判断两个数是否互为质数（也就是只用1这一个公因数）。这里，使用循环遍历所有可能的公约数并测试这些数。在尝试了所有选项后，循环结束。else代码块在两个数互质时执行，应为程序不会遇到中断：

```python
a = 4
b = 9
for i in range(2,min(a ,b)+1):
    print("Testing",i)
    if a %i ==0 and b % i ==0:
        print("Not coprime")
        break
else:
    print('Coprime')
>>>

Testing 2
Testing 3
Testing 4
Coprime
```

​事实上很少这样写代码。一般会写一个辅助函数来进行这样的计算。这样的辅助函数一般会有两种普遍写法。

第一种情况是当找到了符合的情况就立即返回。如果循环执行完毕，就给一个默认值：

```python
def coprime(a, b):
    for i in range(2, min(a, b) + 1):
        if a % i == 0 and b % i == 0:
            return False
    return True


print(coprime(4, 9))
print(coprime(3, 6))

>>>
True
False
```

​第二种写法是，用变量来记录循环过程中有没有碰到这样的情况，如果有，就break提前跳出循环；如果没有，循环就执行完毕，无论如果，都返回那个变量的值：

```python
def coprime_alternate(a, b):
    is_coprime = True
    for i in range(2, min(a, b) + 1):
        if a % i == 0 and b % i == 0:
            is_coprime = False
            break
    return is_coprime


print(coprime_alternate(4, 9))
print(coprime_alternate(3, 6))

>>>
True
False
```

​这两种写法都可以让一个新的读者很容易就理解。根据不同情况，应该选用不同的写法。然而，for/else结构或者while/else结构虽然可以实现逻辑表达，但这种结构很会给读者或者自己带来困惑，弊大于利。因为for与while循环这种简单的结构，读起来应该相当明了才对，如果把else代码块紧跟在他们后面，就会让代码产生歧义。所以，请不要这么写。

**要点**
* Python拥有在for或者while循环后紧跟else代码块的这种语法
* 只有在整个循环没有因为break提前跳出的情况，else代码块才会执行
* 避免在循环后使用else代码，这样代码就太难看懂了

## 第10条 用赋值表达式减少重复代码

​赋值表达式(assignment expression)是Python3.8的新语法，它会用到海象操作符(walrus operator)。这用写法可以解决某些持续依旧的代码重复问题。a = b， 读作 a equals b；而a := b，读作a walrus b。这个符号为什么叫做walrus呢？因为把 := 顺时针旋转90度之后，冒号就是海象的一对眼睛，等号就它的牙齿。

这种表达式很有用，可以在普通的赋值语句无法应用的场合实现赋值，例如可以用在表达式的if语句里面。赋值表达式的值，就是赋给海象操作符左侧那个标识符的值。

例如，如果有一筐新鲜水果要给果汁店做食材，那就可以这样定义其内容：

~~~python
fresh_fruit = {
    'apple': 10,
    'banana': 8,
    'lemon': 5,
}
~~~

​顾客点柠檬汁之前，需要确认现在还有没有柠檬可以榨汁。所以，要首先查出柠檬的数量，然后用if判断其是不是非零值。

```python
fresh_fruit = {
    'apple': 10,
    'banana': 8,
    'lemon': 5,
}
def make_lemonade(count):
    ...


def out_of_stock():
    ...


count = fresh_fruit.get('lemon', 0)
if count:
    make_lemonade(count)
else:
    out_of_stock()
```

​代码看上去很简单，但是还是显得有点松散，因为count数量虽然定义在了整个if/else结构中，但只有if才用得到，else根本就用不到这个变量。所以，这种写法让人误以为count是个if/else都要用到的重要的变量，但实际并非如此。

我们在Python中经常要先获取某个值，然后判断其是否为零，如果是就执行某段代码。对于这种写法，我们以前要通过各种技巧来避免count这样的变量重复出现在代码中，这些技巧有时会让代码变得难懂(参见第5条)。Python引入了赋值表达式来解决这样的问题。下面用海象操作符：

```python
fresh_fruit = {
    'apple': 10,
    'banana': 8,
    'lemon': 5,
}
def make_lemonade(count):
    ...


def out_of_stock():
    ...



if count := fresh_fruit.get('lemon',0):
    make_lemonade(count)
else:
    out_of_stock()
```

​新代码虽然只短了一行，但读起来却清晰很多，因为这种写法明确体现了count变量只与if相关。这个表达式先把 := 右侧的值赋给左边的count变量，然后对自身求值，也就是把变量的值当做整个表达式的值。由于表达式紧跟着if，程序会根据他的值是否非零来决定是否执行if代码块。这种先赋值再判断的做法，正是海象操作符要表达的意思。

​柠檬汁效力强，所以只要一个就能完成订单，这就意味着程序只需要判断非零即可。如果客人点的是苹果汁，那就至少需要四个苹果才行。按照传统的写法，要想从fresh_fruit这个字典中查出苹果的数量，然后在if中构造条件表达式：

```python
fresh_fruit = {
    'apple': 10,
    'banana': 8,
    'lemon': 5,
}


def make_cider(count):
    ...


def out_of_stock():
    ...


count = fresh_fruit.get('apple', 0)
if count:
    if count >= 4:
        make_cider(count)
else:
    out_of_stock()
```

​		这段代码与刚才柠檬汁的例子相同，都过分突出了count的作用。这里，改用海象操作符，让代码更加清晰一些：

```python
fresh_fruit = {
    'apple': 10,
    'banana': 8,
    'lemon': 5,
}


def make_cider(count):
    ...


def out_of_stock():
    ...


if (count := fresh_fruit.get('apple', 4)) >= 4:
    make_cider(count)
else:
    out_of_stock()
```

​这与刚才的例子拥有同样的奇效，并且都让代码更短。但是这里，需要注意的是：赋值表达式本身就放在一对括号中。为什么要这样呢？因为我们要在if语句中把这个表达式的结果和4比较。刚才的例子没有加括号，因为那时只通过赋值表达式本身的值就能决定条件语句的走向：只要表达式的值不是0，程序就会进入if分支。但这次不行，这次要把这个赋值表达式的放在更大的表达式里面，所以需要放在括号里面。当然，在没有必要加括号的情况下，还是尽量不要加括号好。

​还有一种类似的逻辑也会出现刚才所说的代码重复，这里指的是：要根据情况给某个变量赋予不同的值，紧接着要用这个变量做参数调用某个函数。例如，顾客要点香蕉冰沙，那首先就要把香蕉分成好几份，然后用其中的两份来做冰沙。如果不够两份，那就抛出香蕉不足的异常(OutOfBananas)。传统情况会这么写代码：

```python
fresh_fruit = {
    'apple': 10,
    'banana': 8,
    'lemon': 5,
}


def make_cider(count):
    print(count)


def out_of_stock():
    ...


def slice_bananas(count):
    ...


class OutOfBananas(Exception):
    pass


def make_smoothies(count):
    ...


pieces = 0
count = fresh_fruit.get('banana', 0)
if count >= 2:
    pieces = slice_bananas(count)
try:
    smoothies = make_smoothies(pieces)
except OutOfBananas:
    out_of_stock()
```

​还有一种传统写法也很常见，就是把if/else结构上方的那条pieces = 0的赋值语句一到else中：

```python
fresh_fruit = {
    'apple': 10,
    'banana': 8,
    'lemon': 5,
}


def make_cider(count):
    print(count)


def out_of_stock():
    ...


def slice_bananas(count):
    ...


class OutOfBananas(Exception):
    pass


def make_smoothies(count):
    ...

count = fresh_fruit.get('banana', 0)
if count >= 2:
    pieces = slice_bananas(count)
else:
    pieces = 0
try:
    smoothies = make_smoothies(pieces)
except OutOfBananas:
    out_of_stock()
```

​这种写法有点奇怪，因为if与else两个分支都给pieces变量定义了初始值。根据Python的作用域规则，这种分别定义变量初始值的写法是成立的(参见第21条)。虽然说成立，但是看起来比较别扭，所以很多人喜欢第一种写法，也就是在进入条件语句之前，先把pieces的初始值设置好。

​改为海象操作符来实现，可以少写一行代码，也可以压低count变量的地位，让它只出现在if分支中，这样就能更清晰地意识到pieces变量才是整个代码的重点：

```python
fresh_fruit = {
    'apple': 10,
    'banana': 8,
    'lemon': 5,
}


def make_cider(count):
    print(count)


def out_of_stock():
    ...


def slice_bananas(count):
    ...


class OutOfBananas(Exception):
    pass


def make_smoothies(count):
    ...


pieces = 0
if (count := fresh_fruit.get('banana', 0)) >= 2:
    pieces = slice_bananas(count)
try:
    smoothies = make_smoothies(pieces)
except OutOfBananas:
    out_of_stock()
```

​对于if与else分支里面分别定义pieces变量的写法来说，海象操作符能让代码更加清晰，因为这次不用再把count变量放到整个条件语句的上方了：

```python
fresh_fruit = {
    'apple': 10,
    'banana': 8,
    'lemon': 5,
}


def make_cider(count):
    print(count)


def out_of_stock():
    ...


def slice_bananas(count):
    ...


class OutOfBananas(Exception):
    pass


def make_smoothies(count):
    ...


if (count := fresh_fruit.get('banana', 0)) >= 2:
    pieces = slice_bananas(count)
else:
    pieces = 0
try:
    smoothies = make_smoothies(pieces)
except OutOfBananas:
    out_of_stock()
```

​Python小白经常会遇到这样一种困难，就是找不到好的方法来实现switch/case结构。最接近这种结构的就是在if/esle里面嵌套if/else结构，或者使用if/elif/else结构。

```python
count = fresh_fruit.get('banana', 0)
if count >= 2:
    pieces = slice_bananas(count)
    to_enjoy = make_smoothies(pieces)
else:
    count = fresh_fruit.get('apple', 0)
    if count >= 4:
        to_enjoy = make_cider(count)
    else:
        count = fresh_fruit.get('lemon', 0)
        if count:
            to_enjoy = make_lemonade(count)
        else:
            to_enjoy = 'Nothing'
```

​这种难看的写法其实在Python中异常常见。幸好有了海象操作符，能够轻松的模拟出很接近switch/case的方案：

```python
if (count := fresh_fruit.get('banana', 0)) >= 2:
    pieces = slice_bananas(count)
    to_enjoy = make_smoothies(pieces)
elif (count := fresh_fruit.get('apple', 0)) >= 4:
    to_enjoy = make_cider(count)
elif count := fresh_fruit.get('lemon', 0):
    to_enjoy = make_lemonade(count)
else:
    to_enjoy = 'Nothing'
```

​这个版本只比原来断了五行，但是结构却清晰了很多，因为嵌套深度与缩进层数都变少了。只要碰到刚才那种难看的结构，就应该考虑能不能通过海象操作符来实现。

​Python小白还会遇到一个苦难，就是缺少do/while循环结构。例如要把新鲜水果做成果汁并装进瓶子里，直到水果用完为止。下面先用普通的while循环实现：

```python
def pick_fruit():
    ...


def make_juice(fruit, count):
    ...


bottles = []
fresh_fruit = pick_fruit()
while fresh_fruit:
    for fruit, count in fresh_fruit.items():
        batch = make_juice(fruit, count)
        bottles.extend(batch)
    fresh_fruit = pick_fruit()
```

​这种写法需要调用两次pick_fruit()方法，第一次在进入循环之前，因为要给fresh_fruit设定初始值，第二次在while循环体的末尾，因为要把下一轮需要处理的水果列表填充到fresh_fruit列表里面。

如果想复用这行代码，可以考虑loop-and-a-half模式。这个模式虽然能消除重复，但是会让while循环看起来很笨，因为它成了无限循环，程序只能通过break跳出循环体：

```python
bottles = []
while True: # Loop
    fresh_fruit = pick_fruit()
    if not fresh_fruit: # And a half
        break
    for fruit, count in fresh_fruit.items():
        batch = make_juice(fruit, count)
        bottles.extend(batch)
```

​有了海象操作符，就不需要使用loop-and-a-half模式了，可以每轮循环的开头给fresh_fruit变量赋值，并根据变量的值来决定要不要继续循环。这个写法简单易读，所以应该为首选方案：

```python
bottles = []
while fresh_fruit := pick_fruit():
    for fruit, count in fresh_fruit.items():
        batch = make_juice(fruit, count)
        bottles.extend(batch)
```

​在其他的一些场合，赋值表达式也能缩短重复代码(参见第29条)。总之，如果某个表达式或赋值操作需要多次出现在一组代码里面，那就可以考虑使用海象操作符来把这段代码变得简单一些。

**要点**
* 赋值表达式通过海象操作符(:=)，并且让这个值成为这个表达式的结果，可以通过这个特性缩短代码
* 如果赋值表达式是大表达式的一部分，就需要用括号括起来
* 虽然Python不支持switch/case与do/while结构，但可以利用赋值表达式来模拟这些结构