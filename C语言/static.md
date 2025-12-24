在C语言中，`static`关键字有多种用法，主要用于控制变量的**存储期**和**作用域**。下面是`static`变量的详细说明：

## 1. **局部静态变量**（在函数内部）

```c
void function() {
    static int count = 0;  // 静态局部变量
    count++;
    printf("函数被调用了 %d 次\n", count);
}

int main() {
    function();  // 输出：函数被调用了 1 次
    function();  // 输出：函数被调用了 2 次
    function();  // 输出：函数被调用了 3 次
    return 0;
}
```

### 特点：

- **生命周期**：整个程序运行期间都存在
    
- **作用域**：仅限于定义它的函数内部
    
- **初始化**：只在第一次进入函数时初始化一次
    
- **存储位置**：数据段（而非栈）
    

## 2. **静态全局变量**（在函数外部）

```c
// file1.c
static int private_var = 10;  // 静态全局变量，只在当前文件可见

void function1() {
    private_var = 20;  // 可以访问
}

// file2.c
extern int private_var;  // 错误！无法访问file1.c中的private_var
```

### 特点：

- **链接性**：内部链接（只在定义它的源文件中可见）
    
- **作用**：隐藏实现细节，避免命名冲突
    

## 3. **静态函数**

```c
// file1.c
static void private_function() {  // 静态函数，只在当前文件可见
    printf("这是一个私有函数\n");
}

// file2.c
extern void private_function();  // 错误！无法访问
```

## 4. **静态成员变量**（在结构体中）

```c
struct Counter {
    int id;
    static int total_count;  // 静态成员（C语言不支持，这是C++语法）
};
```

**注意**：C语言的结构体不支持静态成员，这是C++的特性。

## 主要特性总结

|特性|静态局部变量|静态全局变量|
|---|---|---|
|**生命周期**|整个程序运行期|整个程序运行期|
|**作用域**|函数内部|文件内部|
|**初始化**|只初始化一次|程序启动时初始化|
|**默认值**|自动初始化为0|自动初始化为0|
|**存储位置**|数据段|数据段|

## 实际应用场景

### 1. **计数器功能**

```c
int get_next_id() {
    static int id = 0;
    return ++id;
}
```

### 2. **缓存/记忆化**

```c
int fibonacci(int n) {
    static int cache[100] = {0};
    
    if (n <= 1) return n;
    if (cache[n] != 0) return cache[n];
    
    cache[n] = fibonacci(n-1) + fibonacci(n-2);
    return cache[n];
}
```

### 3. **单次初始化**

```c
void initialize_once() {
    static bool initialized = false;
    if (!initialized) {
        printf("初始化资源...\n");
        initialized = true;
    }
    // 其他操作...
}
```

## 重要注意事项

1. **线程安全性**：静态变量在多线程环境中需要加锁保护
    
2. **递归函数中的静态变量**：所有递归调用共享同一个静态变量
    
3. **可重入性**：使用静态变量的函数是不可重入的
    
4. **初始化时机**：在main函数执行之前初始化
    

```c
// 线程不安全的例子
int get_id() {
    static int id = 0;
    return ++id;  // 多线程下可能得到重复ID
}
```

## 对比表格

|变量类型|作用域|生命周期|存储位置|
|---|---|---|---|
|自动变量（局部）|函数内部|函数执行期间|栈|
|静态局部变量|函数内部|整个程序|数据段|
|全局变量|整个程序（多文件）|整个程序|数据段|
|静态全局变量|单个文件|整个程序|数据段|

静态变量是C语言中实现**状态保持**和**信息隐藏**的重要机制，合理使用可以提高程序的模块性和效率。