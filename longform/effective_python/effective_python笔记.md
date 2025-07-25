## 解释“将副作用从确定性行为中分离出来”
### 什么叫“确定性行为”  
1. 数学意义  
   给定同样的输入，永远得到同样的输出，且**不对外界产生任何可观测的影响**。  
2. 在示例里的对应物  
   - 输入：当前字典 `{'green':12,'blue':3}` 与增量列表 `[('red',5),('blue',17),('orange',9)]`  
   - 期望的“纯粹计算结果”：  
     ```
     {'green':12,'blue':20,'red':5,'orange':9}
     ```  
   只要输入不变，这个映射就永远不变，这就是确定性。

### 什么叫“副作用”  
1. 定义  
   函数或表达式**除了返回值以外，对外界产生的任何可观测变化**都算副作用：  
   - 打印到终端  
   - 写磁盘 / 写数据库  
   - 修改全局变量  
   - 发送网络请求  
2. 在示例里的对应物  
   `log_missing` 里的 `print('Key added')` 就是副作用。  
   它不会影响到字典的最终内容，但会**把信息写到标准输出**，改变了程序之外的“世界状态”。

### 什么叫“分离”  
1. 代码结构上的分离  
   - 纯逻辑：`defaultdict` 只负责一件事——  
     “如果键不存在，就调用工厂函数拿默认值并塞进字典”。  
   - 副作用：`log_missing` 这个函数负责“打印提示”。  
   两者**通过函数指针解耦**：  
   ```python
   result = defaultdict(log_missing, current)   # 把副作用注入进来
   # 换成别的工厂函数，副作用立刻消失
   result2 = defaultdict(lambda: 0, current)    # 不再打印
   ```
2. 测试上的分离  
   - 测试“字典累加逻辑”时，用哑工厂函数，断言最终字典即可；  
   - 测试“打印逻辑”时，单独调用 `log_missing`，用 `capsys` 等工具捕获 stdout。  
3. 阅读与维护上的分离  
   读代码的人一眼就能判断：  
   - 哪部分代码是纯粹的数据变换（安全、可预测）；  
   - 哪部分代码会跟外部系统交互（需要额外注意日志、并发、重试等问题）。

### 总结  
`defaultdict` 只关心“缺键时应该返回什么”这一**确定性规则**；  
而“在缺键时顺便打印日志”这一**副作用**被外置到 `log_missing` 函数里，  
二者通过函数指针松耦合——这就是“将副作用从确定性行为中分离出来”。


## “同一个简单函数接口”在 Python 里可以用到的不同实现方式
假设接口要求：传一个字符串，返回其长度。

1. 普通函数  
```python
def strlen(s: str) -> int:
    return len(s)
```

2. lambda 表达式  
```python
strlen = lambda s: len(s)
```

3. operator 模块里的现成函数  
```python
from operator import length_hint as strlen   # 语义类似
```

4. 内置函数直接当接口  
```python
strlen = len        # 直接把内置函数拿来用
```

5. 偏函数（functools.partial）  
```python
from functools import partial
strlen = partial(len)   # 把 len 的第一个参数位置留空
```

6. 类 + `__call__` 实现可调用对象  
```python
class StrLen:
    def __call__(self, s: str) -> int:
        return len(s)

strlen = StrLen()
```

7. 闭包工厂  
```python
def make_strlen():
    def _strlen(s):          # 内层函数捕获外层作用域
        return len(s)
    return _strlen

strlen = make_strlen()
```

8. 生成器函数（一次性接口）  
虽然不返回长度，但可演示“同一签名”的另一种行为：  
```python
def strlen_gen(s: str):
    yield len(s)            # 返回生成器对象，可迭代一次

# 使用：next(strlen_gen("abc")) → 3
```

9. 异步函数（async def）  
```python
import asyncio

async def strlen(s: str) -> int:
    await asyncio.sleep(0)  # 假装异步
    return len(s)

# 使用：asyncio.run(strlen("abc"))
```

这些实现都满足“接受一个字符串，返回一个整数”的**简单接口**，但可根据是否需要状态、异步、惰性求值、可组合性等场景自由选择。


## 为什么说generate_inputs就是要展示的类多态
因为 `generate_inputs` 是一个 **类方法**，它通过 `cls` 来创建对象；  
而 `cls` 在运行时会**指向不同的具体子类**，于是同一段代码：
```python
for input_data in input_class.generate_inputs(config):
    ...
```

在 `input_class` 分别是 `PathInputData`、`HttpInputData`、`S3InputData`……时，会自动调用各自**子类覆写后的** `generate_inputs`，产生对应类型的 `input_data` 实例。  
**同一接口、不同实现**，这就是多态。

## 什么时候应该显式传入super的参数
在 **Python 3** 中，`super()` 的零参数形式（即 `super()`）只能在 **类定义内部** 的方法里使用，编译器会自动补全为 `super(当前类, self)`。  
其余所有情况都必须 **显式传入两个参数**，即：

> `super(类A, 实例或子类B)`

什么时候必须显式写这两个参数？下面分场景展开。

### 1. 在 **类外部** 使用 `super`
```python
class Parent:
    def greet(self): print('Hi from Parent')

class Child(Parent):
    def greet(self): print('Hi from Child')

c = Child()
super(Child, c).greet()   # 必须写 Child 和 c
```
类外没有“当前类”的上下文，解释器无法自动推断，必须自己给。

### 2. 在 **类内部** 但想 **跳过当前类**，从 MRO 的某个中间点开始
```python
class A: pass
class B(A): pass
class C(A): pass
class D(B, C):
    def show(self):
        # 跳过 D 本身，直接从 B 之后（即 C）开始
        super(B, self).some_method()
```
此时用 `super(B, self)` 明确告诉 Python：从 `B` 的下一个 MRO 节点开始找方法。

### 3. 使用 **类方法** 或 **静态方法** 时
```python
class Base:
    @classmethod
    def factory(cls):
        return cls()

class Sub(Base):
    @classmethod
    def factory(cls):
        # 在类方法里没有 self，只能显式写 cls
        return super(Sub, cls).factory()
```
因为类方法没有绑定实例，必须显式提供第二个参数（类本身或实例）。

### 4. **动态继承 / 元编程** 场景
当你用 `type()` 动态创建类，或在元类里操作 MRO 时，编译期无法推断“当前类”，只能手写：

```python
def patch_method(target_cls):
    def patched(self):
        super(target_cls, self).original()
    target_cls.original = target_cls.method
    target_cls.method = patched
```


### 5. 在 **Python 2** 里
Python 2 没有零参数 `super()`，**任何时候都要显式写**：

```python
super(Child, self).__init__()
```


### 参数合法性要求
- `super(cls, obj)`：要求 `isinstance(obj, cls)` 为真。  
- `super(cls1, cls2)`：要求 `issubclass(cls2, cls1)` 为真。

### 速查表

| 场景 | 是否显式传参 | 示例 |
|---|---|---|
| 普通实例方法（Python 3） | ❌ | `super().method()` |
| 类方法 / 静态方法 | ✅ | `super(Sub, cls).method()` |
| 类外部 | ✅ | `super(Child, instance).method()` |
| 多重继承想跳过某一级 | ✅ | `super(SomeParent, self).method()` |
| Python 2 | ✅ | `super(Child, self).method()` |

一句话总结：  
**只要编译器无法在编译期自动推断“当前类”和“当前实例/子类”，就必须显式把这两个参数塞进 `super()` 中。**

## Mixin类与普通类的区别
Mixin 类与普通类在 **语法层面和代码执行层面没有本质差别**；它们都遵循 Python 的类定义、继承、MRO 等同一套规则。真正的差异主要体现在 **设计意图和使用约定** 上，具体可以总结为以下 5 点：

| 维度 | Mixin 类 | 普通类 |
|---|---|---|
| **设计目的** | 提供“可插拔”的单一功能片段，供其他类组合 | 描述一个完整、独立的实体 |
| **实例化意愿** | **不被单独实例化**（通常没有或只有极小的 `__init__`） | 可直接实例化 |
| **继承位置** | 一般放在多重继承列表的 **右侧**，主类在左侧 | 通常作为 **主父类** 或单继承 |
| **命名习惯** | 类名后缀 **Mixin** 或 **Able** 等（提示用途） | 无强制后缀 |
| **依赖关系** | 不关心宿主类是谁，只负责提供方法实现 | 子类与父类存在“is-a”语义 |

### 语法层面如何“识别”
- 语法解析器 **不会** 因为类名带 `Mixin` 就特殊对待；它们仍是普通类。  
- 是否属于 Mixin **全凭约定**：  
  - 类很小，只包含少量方法；  
  - 不单独 `__main__` 里 `()` 出来用；  
  - 文档或注释写明“仅作混入”。  

### 代码执行层面如何“区分”
- Mixin 类的方法在 **运行时** 和普通父类方法一样，通过 MRO 查找，没有任何额外开销。  
- 若 Mixin 没写 `__init__`，子类会沿着 MRO 自动跳过它；写了 `__init__` 就必须在子类里用 `super()` 保证链式调用，否则可能出现重复初始化或漏初始化——但这和普通多继承的风险一致，并非 Mixin 独有。  

一句话总结：  
**在 Python 里，Mixin 不是语法关键字，而是一种“约定大于配置”的设计模式**。只要遵循“小而专、不单独实例化、供组合使用”的原则，任何普通类都可以被当作 Mixin 来使用 。

## 最少惊奇原则(the rule of least surprise)
最少惊奇原则（**Rule of Least Surprise / Principle of Least Astonishment**）是软件设计中的一条黄金准则，核心思想是：

> **接口、行为或设计应当符合用户（开发者或终端用户）的预期，避免“意料之外”的体验。**

---

### **为什么重要？**
- **降低认知成本**：用户不需要额外学习或猜测系统行为。
- **减少错误**：不符合直觉的设计容易导致误用或bug。
- **提升可维护性**：代码行为可预测，团队协作更高效。

---

### **经典案例**
1. **Python列表的切片**  
   `lst[1:3]` 返回 `[1, 2)`（左闭右开），**看似违背直觉**，但Python通过**统一的区间约定**（所有切片、range等一致）减少了其他场景下的惊奇。

2. **Unix命令行设计**  
   `ls -l` 默认不递归子目录，而 `find` 递归——**分工明确**，避免用户混淆。

3. **React的`setState`异步更新**  
   早期开发者常误以为`setState`后立即可读到新状态，后来React通过**文档和工具明确提示异步行为**，减少误解。

---

### **如何实践？**
- **遵循惯例**：如HTTP状态码（404=未找到）、编程语言命名风格（Python用`snake_case`）。
- **明确文档**：对可能反直觉的行为（如副作用、性能陷阱）需在文档中**显式警告**。
- **渐进式揭示**：复杂功能通过可选参数或分层API暴露（如`requests`库的`Session`对象）。
- **错误信息友好**：例如TypeScript的类型报错会提示具体字段，而非笼统报错。

---

### **反例警示**
- **JavaScript的 `==`  vs  `===`**  
  `'5' == 5` 返回 `true` 曾导致无数bug，违背直觉（类型强制转换），ESLint强制 `===` 即是对该原则的修复。
- **C++的隐式类型转换**  
  允许`int`到`bool`的隐式转换，易引发逻辑错误，现代C++推荐使用`explicit`关键字抑制。

---
### **一句话总结**  
**好的设计让用户感叹“就应该这样”，而非“还能这样？”**

## 调用站点（call site）
“调用站点”(call site) 是编程里的**特有名词**，专指“源代码中发起函数/方法/属性访问的那一行（或那一处位置）”。

## 漏桶算法
漏桶算法（Leaky Bucket），描述了一个桶口流入水流，底部开口的桶。是不是很像小时候经常做的一边注水一边放水的数学应用题？ 桶的上部接水，桶的下部以固定的速率漏水，当桶中的水的量超过桶的容量时，后续的水将无法进入桶中，漏桶随即进入溢出状态。在溢出状态时，后续的水将被抛弃，或者在队列中等待，直到桶中的水量低于一个阈值时，才可以继续承接水量。

**漏桶配额**（Leaky Bucket Quota）