# Vector

在C++中，`std::vector` 是标准模板库（STL）中非常常用的一种序列容器，它类似于动态数组，提供了动态大小的数组功能。以下是一些常用的 `std::vector` 相关函数：

### 构造函数

- **默认构造**：`std::vector<int> v;` 创建一个空的 `vector`。
- **指定大小**：`std::vector<int> v(10);` 创建一个大小为10的 `vector`，所有元素初始化为0。
- **指定大小和初始值**：`std::vector<int> v(10, 1);` 创建一个大小为10的 `vector`，所有元素初始化为1。
- **从另一个容器构造**：`std::vector<int> v1 = {1, 2, 3};` 或 `std::vector<int> v2(v1);` 从另一个容器或数组构造。

### 容量相关函数

- **`size()`**：返回当前 `vector` 中元素的数量。

  ```cpp
  std::vector<int> v = {1, 2, 3};
  std::cout << v.size(); // 输出3
  ```

- **`capacity()`**：返回当前分配的存储容量（以元素个数为单位）。

  ```cpp
  std::vector<int> v;
  v.reserve(10);
  std::cout << v.capacity(); // 输出10
  ```

- **`empty()`**：检查 `vector` 是否为空。

  ```cpp
  std::vector<int> v;
  if (v.empty()) {
      std::cout << "Vector is empty";
  }
  ```

- **`reserve(size_type n)`**：预留至少 `n` 个元素的存储空间，减少动态分配的次数。

  ```cpp
  std::vector<int> v;
  v.reserve(100); // 预留100个元素的空间
  ```

- **`shrink_to_fit()`**：尝试减少分配的存储空间，使其更接近实际大小。

  ```cpp
  std::vector<int> v(100);
  v.resize(10);
  v.shrink_to_fit(); // 尝试减少存储空间
  ```

### 元素访问

- **`operator[]`**：通过下标访问元素（不检查边界）。

  ```cpp
  std::vector<int> v = {1, 2, 3};
  std::cout << v[1]; // 输出2
  ```

- **`at(size_type pos)`**：通过下标访问元素（检查边界，越界抛异常）。

  ```cpp
  std::vector<int> v = {1, 2, 3};
  std::cout << v.at(1); // 输出2
  ```

- **`front()`**：返回第一个元素的引用。

  ```cpp
  std::vector<int> v = {1, 2, 3};
  std::cout << v.front(); // 输出1
  ```

- **`back()`**：返回最后一个元素的引用。

  ```cpp
  std::vector<int> v = {1, 2, 3};
  std::cout << v.back(); // 输出3
  ```

- **`data()`**：返回指向底层数组的指针。

  ```cpp
  std::vector<int> v = {1, 2, 3};
  int* ptr = v.data();
  std::cout << *ptr; // 输出1
  ```

### 修改器

- **`push_back(const T& value)`**：在末尾添加一个元素。

  ```cpp
  std::vector<int> v;
  v.push_back(1);
  v.push_back(2);
  ```

- **`pop_back()`**：移除最后一个元素。

  ```cpp
  std::vector<int> v = {1, 2, 3};
  v.pop_back();
  std::cout << v.size(); // 输出2
  ```

- **`insert(iterator pos, const T& value)`**：在指定位置插入一个元素。

  ```cpp
  std::vector<int> v = {1, 3};
  v.insert(v.begin() + 1, 2); // 在索引1处插入2
  ```

- **`erase(iterator pos)`**：删除指定位置的元素。

  ```cpp
  std::vector<int> v = {1, 2, 3};
  v.erase(v.begin() + 1); // 删除索引1处的元素
  ```

- **`clear()`**：清空所有元素，但不释放内存。

  ```cpp
  std::vector<int> v = {1, 2, 3};
  v.clear();
  std::cout << v.size(); // 输出0
  ```

- **`resize(size_type n, const T& value)`**：改变 `vector` 的大小。

  ```cpp
  std::vector<int> v = {1, 2, 3};
  v.resize(5, 0); // 扩大到5个元素，新元素初始化为0
  v.resize(2); // 缩小到2个元素
  ```

### 迭代器相关

- **`begin()`** 和 **`end()`**：返回指向第一个元素和最后一个元素之后位置的迭代器。

  ```cpp
  std::vector<int> v = {1, 2, 3};
  for (auto it = v.begin(); it != v.end(); ++it) {
      std::cout << *it << " ";
  }
  ```

- **`rbegin()`** 和 **`rend()`**：返回指向最后一个元素和第一个元素之前位置的逆向迭代器。

  ```cpp
  std::vector<int> v = {1, 2, 3};
  for (auto it = v.rbegin(); it != v.rend(); ++it) {
      std::cout << *it << " ";
  }
  ```

这些函数提供了丰富的功能，使得 `std::vector` 成为C++中非常灵活和强大的容器之一。

# Stack

在C++中，`std::stack`、`std::queue` 和 `std::map` 是标准模板库（STL）中常用的容器适配器或关联容器，它们提供了丰富的成员函数来操作容器中的元素。以下是它们的相关函数介绍：

### `std::stack`
`std::stack` 是一个后进先出（LIFO）的容器适配器，它基于底层容器（默认是 `std::deque`）实现。

#### 常用成员函数
- **构造函数**
  - `std::stack<T> s;`：默认构造一个空栈。
  - `std::stack<T> s(cont);`：基于给定的底层容器 `cont` 构造栈。
- **元素访问**
  - `T& top();`：返回栈顶元素的引用。
  - `const T& top() const;`：返回栈顶元素的常量引用。
- **容量**
  - `bool empty() const;`：检查栈是否为空，为空返回 `true`。
  - `size_type size() const;`：返回栈中元素的数量。
- **修改器**
  - `void push(const T& value);`：将一个元素压入栈顶。
  - `void push(T&& value);`：将一个右值元素压入栈顶。
  - `void pop();`：移除栈顶元素。
  - `void swap(stack& other);`：交换两个栈的内容。

#### 示例代码
```cpp
#include <iostream>
#include <stack>

int main() {
    std::stack<int> s;
    s.push(1);
    s.push(2);
    s.push(3);

    std::cout << "Top element: " << s.top() << std::endl; // 输出 3
    s.pop();
    std::cout << "Top element after pop: " << s.top() << std::endl; // 输出 2

    std::cout << "Stack size: " << s.size() << std::endl; // 输出 2
    std::cout << "Is stack empty? " << (s.empty() ? "Yes" : "No") << std::endl; // 输出 No

    return 0;
}
```

# Queue

### `std::queue`

`std::queue` 是一个先进先出（FIFO）的容器适配器，它基于底层容器（默认是 `std::deque`）实现。

#### 常用成员函数
- **构造函数**
  - `std::queue<T> q;`：默认构造一个空队列。
  - `std::queue<T> q(cont);`：基于给定的底层容器 `cont` 构造队列。
- **元素访问**
  - `T& front();`：返回队列头部元素的引用。
  - `const T& front() const;`：返回队列头部元素的常量引用。
  - `T& back();`：返回队列尾部元素的引用。
  - `const T& back() const;`：返回队列尾部元素的常量引用。
- **容量**
  - `bool empty() const;`：检查队列是否为空，为空返回 `true`。
  - `size_type size() const;`：返回队列中元素的数量。
- **修改器**
  - `void push(const T& value);`：将一个元素添加到队列尾部。
  - `void push(T&& value);`：将一个右值元素添加到队列尾部。
  - `void pop();`：移除队列头部元素。
  - `void swap(queue& other);`：交换两个队列的内容。

#### 示例代码
```cpp
#include <iostream>
#include <queue>

int main() {
    std::queue<int> q;
    q.push(1);
    q.push(2);
    q.push(3);

    std::cout << "Front element: " << q.front() << std::endl; // 输出 1
    q.pop();
    std::cout << "Front element after pop: " << q.front() << std::endl; // 输出 2

    std::cout << "Queue size: " << q.size() << std::endl; // 输出 2
    std::cout << "Is queue empty? " << (q.empty() ? "Yes" : "No") << std::endl; // 输出 No

    return 0;
}
```

# Map

### `std::map`

`std::map` 是一个基于红黑树的关联容器，它存储键值对，并且按键的顺序自动排序。

#### 常用成员函数
- **构造函数**
  - `std::map<Key, T> m;`：默认构造一个空映射。
  - `std::map<Key, T>(const std::map<Key, T>& other);`：拷贝构造。
  - `std::map<Key, T>(std::map<Key, T>&& other);`：移动构造。
- **迭代器**
  - `iterator begin();`：返回指向第一个键值对的迭代器。
  - `const_iterator begin() const;`：返回指向第一个键值对的常量迭代器。
  - `iterator end();`：返回指向最后一个键值对之后的迭代器。
  - `const_iterator end() const;`：返回指向最后一个键值对之后的常量迭代器。
- **容量**
  - `bool empty() const;`：检查映射是否为空，为空返回 `true`。
  - `size_type size() const;`：返回映射中键值对的数量。
  - `size_type max_size() const;`：返回映射能容纳的最大键值对数量。
- **元素访问**
  - `T& operator[](const Key& key);`：通过键访问对应的值，如果键不存在则会插入一个默认构造的值。
  - `const T& at(const Key& key) const;`：通过键访问对应的值，如果键不存在则抛出 `std::out_of_range` 异常。
- **修改器**
  - `std::pair<iterator, bool> insert(const std::pair<Key, T>& value);`：插入一个键值对，返回一个迭代器和一个布尔值，布尔值表示是否插入成功。
  - `void erase(iterator pos);`：通过迭代器删除一个键值对。
  - `void erase(const Key& key);`：通过键删除一个键值对。
  - `void clear();`：清空映射。
- **查找**
  - `iterator find(const Key& key);`：查找键，返回指向该键的迭代器，如果未找到则返回 `end()`。
  - `const_iterator find(const Key& key) const;`：查找键，返回指向该键的常量迭代器。
  - `size_type count(const Key& key) const;`：返回键的数量，对于 `std::map` 总是返回 0 或 1。

#### 示例代码
```cpp
#include <iostream>
#include <map>

int main() {
    std::map<int, std::string> m;
    m[1] = "one";
    m[2] = "two";
    m[3] = "three";

    std::cout << "Element with key 2: " << m[2] << std::endl; // 输出 two

    auto it = m.find(3);
    if (it != m.end()) {
        std::cout << "Found element with key 3: " << it->second << std::endl; // 输出 three
    }

    m.erase(2);
    std::cout << "Size after erase: " << m.size() << std::endl; // 输出 2

    for (const auto& pair : m) {
        std::cout << pair.first << ": " << pair.second << std::endl;
    }

    return 0;
}
```
