`qsort` 是C语言标准库中一个功能强大的**通用排序函数**，使用快速排序算法实现（但不保证一定是快速排序）。它可以在 O(n log n) 的平均时间复杂度内对任何类型的数组进行排序。
## **函数原型**

`#include <stdlib.h>`

`void qsort(void *base, size_t nmemb, size_t size,int (*compar)(const void *, const void *));`
[[const void 指针]]
## **参数说明**
| 参数       | 类型       | 说明            |
| -------- | -------- | ------------- |
| `base`   | `void*`  | 指向数组第一个元素的指针  |
| `nmemb`  | `size_t` | 数组中元素的数量      |
| `size`   | `size_t` | 每个元素的大小（字节）   |
| `compar` | 函数指针     | 比较函数，用于定义排序规则 |

## **总结**

### **qsort 的优点：**

1. **通用性强**：可以对任何数据类型排序
    
2. **高效**：通常使用快速排序算法
    
3. **标准库函数**：跨平台可用
    
4. **易于使用**：只需提供比较函数
    

### **使用要点：**

1. **比较函数必须正确实现**：返回负/零/正表示a在b前/相等/后
    
2. **注意类型转换**：在比较函数内部进行正确的类型转换
    
3. **处理相等情况**：确保相等时返回0
    
4. **避免溢出**：特别是整数比较时
```c
// 整数升序
int compare_int_asc(const void *a, const void *b) {
    int x = *(int*)a;
    int y = *(int*)b;
    if (x < y) return -1;
    if (x > y) return 1;
    return 0;
}

// 整数降序
int compare_int_desc(const void *a, const void *b) {
    int x = *(int*)a;
    int y = *(int*)b;
    if (x > y) return -1;  // 注意：这里反过来了
    if (x < y) return 1;
    return 0;
}

// 字符串升序
int compare_str_asc(const void *a, const void *b) {
    return strcmp(*(const char**)a, *(const char**)b);
}

// 结构体排序
int compare_struct(const void *a, const void *b) {
    MyStruct *s1 = (MyStruct*)a;
    MyStruct *s2 = (MyStruct*)b;
    // 多级排序示例
    `if (s1->field1 != s2->field1) {`
        `return s1->field1 - s2->field1;`
    `}`
    `return s1->field2 - s2->field2;`
}
```