###  `strcspn()` 函数

- 函数原型：`size_t strcspn(const char *str1, const char *str2);`
    
- 功能：在 `str1` 中查找第一个出现在 `str2` 中的字符，返回该字符的位置
    
- 示例：`strcspn("张三 李四\n", "\n")` 返回 `8`（`\n` 在第8个位置）