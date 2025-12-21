`const void*` 是C语言中一个非常重要的指针类型，它表示 **"指向常量数据的通用指针"**。
## **1. 基本概念**

c

const void* ptr;  // 声明一个指向常量数据的通用指针

**拆解理解：**

- `void*`：通用指针，可以指向任何数据类型
    
- `const`：常量限定符，表示不能通过这个指针修改所指向的数据
    
- 组合起来：**一个可以指向任何类型数据的指针，但保证不会修改这些数据**
**总结：**

- `const void*`：数据是const，指针不是
    
- `void* const`：指针是const，数据不是
    
- `const void* const`：指针和数据都是cons
## **总结**

|概念|含义|示例|
|---|---|---|
|`const void*`|指向常量数据的通用指针|`const void* ptr = &data;`|
|`void* const`|常量指针，指向可修改数据|`void* const ptr = &data;`|
|`const void* const`|常量指针指向常量数据|`const void* const ptr = &data;`|

**关键要点：**

1. **`const void*` 的主要用途**：作为函数参数，表示函数不会修改传入的数据
    
2. **类型安全**：使用 `const void*` 可以防止意外修改数据
    
3. **通用性**：可以指向任何类型的数据，同时保持只读保证
    
4. **标准库使用**：许多C标准库函数使用 `const void*` 作为参数
    
5. **转换注意**：从 `const void*` 转换回具体类型时，要保持const的一致性
    

**简单记忆：**

- 读作 **"const修饰的是void*指向的数据"**
    
- 意味着 **"通过这个指针，数据是只读的"**
    
- 常用于 **比较函数、查找函数、回调函数** 等场景
**最常用的场景就是 [[qsort 函数]]的比较函数**：

c

int compare(const void* a, const void* b) {
    // 这里保证不会修改a和b指向的数据
    return *(const int*)a - *(const int*)b;
}