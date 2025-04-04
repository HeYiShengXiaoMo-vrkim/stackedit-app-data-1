# 对于`_`类

```python
class Queue:
  def __init__(self, contents):
    self._hiddenlist = list(contents)
 
  def push(self, value):
    self._hiddenlist.insert(0, value)
    
  def pop(self):
    return self._hiddenlist.pop(-1)
 
  def __repr__(self):
    return "Queue({})".format(self._hiddenlist)
 
queue = Queue([1, 2, 3])
print(queue)
queue.push(0)
print(queue)
queue.pop()
print(queue)
print(queue._hiddenlist)
```
<br>
<hr>
这个 `Queue` 类是一个简单的队列（FIFO，先进先出）实现，但有几个特别之处：

### 1. **隐藏的内部列表**
```python
self._hiddenlist = list(contents)
```
- `_hiddenlist` 代表队列的内部存储结构。Python 中下划线开头的变量（如 `_hiddenlist`）通常被视为“受保护的”或者“内部使用”的，表示这是类的私有数据，虽然在技术上用户仍然可以访问它（不像 Java 或 C++ 的 `private` 修饰符会严格限制访问）。
- 它特别之处在于，这个设计是告诉用户：虽然你可以访问 `_hiddenlist`，但这不是你应该直接操作的对象。你应当通过 `push()` 和 `pop()` 方法来修改队列，而不是直接操作 `_hiddenlist`。

### 2. **`push` 和 `pop` 方法的实现**
```python
def push(self, value):
    self._hiddenlist.insert(0, value)
```
- `push()` 方法把新元素插入到列表的开头。这是队列的一个特征：新来的元素会插入队列的最前面。

```python
def pop(self):
    return self._hiddenlist.pop(-1)
```
- `pop()` 方法移除并返回列表的最后一个元素。这符合队列的 "先进先出" 原则：最早进入队列的元素最先被移除。

### 3. **队列的可视化 (`__repr__`)**
```python
def __repr__(self):
    return "Queue({})".format(self._hiddenlist)
```
- 这个方法用于定义当你打印对象时如何显示。这个方法使得 `print(queue)` 显示一个友好的字符串格式，如 `Queue([1, 2, 3])`，而不是 Python 默认的内存地址形式。它让你更清晰地看到队列中目前的状态。

### 4. **队列 vs 列表**
- 虽然它内部是用 Python 列表实现的，但设计上表现为一个“队列”。区别在于，这个类提供了专门的 `push()` 和 `pop()` 方法，来确保队列的行为是 FIFO（先进先出）。
- 然而，代码中直接访问了 `_hiddenlist`，显示了它的本质还是个列表。这也说明类的封装并不完全严格。

### 总结
- **特别之处**在于，它通过封装列表来模拟队列，并为用户提供了专门的方法去操作队列。
- **封装**：虽然提供了队列的行为和外观，但实际上没有完全限制访问内部列表，用户可以直接访问 `_hiddenlist`。
- **操作方法**：推送和弹出元素都遵循了队列的先进先出规则。

这段代码展示了如何使用类的封装来提供一个简单的抽象（队列），同时也展示了 Python 的灵活性和封装的不完全强制性。

# 对于`__`类
```python
class Spam:
  __egg = 7
  def print_egg(self):
    print(self.__egg)
 
s = Spam()
s.print_egg()
print(s._Spam__egg)
print(s.__egg)class Spam:
  __egg = 7
  def print_egg(self):
    print(self.__egg)
 
s = Spam()
s.print_egg()
print(s._Spam__egg)
print(s.__egg)
```
<br>
<hr>

让我们一步步分析这个代码，特别是其中的“封装”和“私有属性”机制：

### 1. **私有属性 `__egg`**
```python
class Spam:
  __egg = 7
  def print_egg(self):
    print(self.__egg)
```
- `__egg` 前面用了双下划线（`__`），这是 Python 中的一种私有属性的约定。Python 会自动对这种双下划线开头的属性进行“**名称改写（name mangling）**”，将属性名修改为 `_类名__属性名`。这样可以避免外部直接访问私有属性，从而实现一种更强的封装机制。

### 2. **调用 `print_egg()` 方法**
```python
s = Spam()
s.print_egg()  # 输出 7
```
- `print_egg()` 方法可以访问类中的私有属性 `__egg`，因为它在类的内部。输出结果会是 `7`。

### 3. **通过名称改写访问私有属性**
```python
print(s._Spam__egg)  # 输出 7
```
- 虽然 `__egg` 是私有的，但你可以通过 Python 的名称改写机制直接访问它。名称改写的规则是将 `__egg` 改成 `_Spam__egg`。所以，`s._Spam__egg` 能正确访问这个私有属性，输出结果为 `7`。
  
### 4. **尝试直接访问 `__egg`**
```python
print(s.__egg)  # 报错：AttributeError
```
- 这行代码试图直接访问 `s.__egg`，但因为 Python 对其进行了名称改写，类外部无法直接访问原始的 `__egg` 名称。所以会引发一个 `AttributeError`，提示找不到这个属性。

### 总结
- **双下划线（`__`）前缀**：这种写法会触发 Python 的名称改写机制，实际上是将属性改成 `_类名__属性名`，从而隐藏属性，防止直接访问。
- **访问方式**：类内可以直接访问私有属性，但类外需要通过改写后的名称访问（如 `_Spam__egg`）。
- **限制**：虽然名称改写增加了访问的难度，但它并不是一种绝对的保护机制（不像 C++ 或 Java 的 `private` 修饰符那样严格）。如果你知道改写规则，仍然可以通过 `_Spam__egg` 这种方式访问到私有属性。

所以，这种封装机制主要是为了避免意外访问和修改，而不是为了绝对禁止。
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzU0NDEyNzI3XX0=
-->