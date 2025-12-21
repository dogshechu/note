- `fgets()` 会读取一行输入，包括换行符 `\n`
    
- 例如：如果输入 "张三 李四" 并按回车，`s.name` 的内容是 `"张三 李四\n"`
- `fgets()` 是C语言中用于从输入流读取字符串的标准库函数，特别适合读取包含空格的字符串。

## 函数原型

c

char *fgets(char *str, int n, FILE *stream);

## 参数说明

- `str`：指向字符数组的指针，用于存储读取的字符串
    
- `n`：要读取的最大字符数（包括结尾的空字符）
    
- `stream`：输入流，通常是 `stdin`（标准输入）
    

## 返回值

- 成功：返回 `str` 指针
    
- 失败或到达文件末尾：返回 `NULL`
    

## 特点

1. **读取包含空格的字符串**：与 `scanf("%s")` 不同，`fgets()` 会读取空格
    
2. **自动添加空字符**：在字符串末尾添加 `\0`
    
3. **包含换行符**：如果读取到换行符，会将其包含在字符串中
    
4. **防止缓冲区溢出**：最多读取 `n-1` 个字符，确保安全
    

## 基本用法

c

#include <stdio.h>

int main() {
    char buffer[100];
    
    printf("请输入字符串: ");
    fgets(buffer, sizeof(buffer), stdin);
    
    printf("你输入的是: %s", buffer);
    
    return 0;
}

## 处理换行符

由于 `fgets()` 会保留换行符，通常需要移除它：

c

#include <stdio.h>
#include <string.h>

int main() {
    char name[50];
    
    printf("请输入姓名: ");
    fgets(name, sizeof(name), stdin);
    
    // 移除换行符
    size_t len = strlen(name);
    if (len > 0 && name[len-1] == '\n') {
        name[len-1] = '\0';
    }
    
    printf("你好, %s!\n", name);
    
    return 0;
}

## 与 `scanf()` 的比较

|特性|`fgets()`|`scanf("%s")`|
|---|---|---|
|读取空格|是|否|
|缓冲区安全|是|否（除非指定宽度）|
|包含换行符|是|否|
|读取整行|是|否|

## 实际应用示例

c

#include <stdio.h>
#include <string.h>

struct Person {
    char name[50];
    int age;
};

int main() {
    struct Person p;
    
    // 使用 fgets 读取可能包含空格的姓名
    printf("请输入姓名: ");
    fgets(p.name, sizeof(p.name), stdin);
    
    // 移除换行符
    p.name[strcspn(p.name, "\n")] = 0;
    
    printf("请输入年龄: ");
    scanf("%d", &p.age);
    
    printf("\n个人信息:\n");
    printf("姓名: %s\n", p.name);
    printf("年龄: %d\n", p.age);
    
    return 0;
}

## 注意事项

1. **混合使用 `fgets()` 和 `scanf()`**：
    
    - 在 `scanf()` 后使用 `fgets()` 时，需要清除输入缓冲区
        
    - 可以使用 `while(getchar() != '\n');` 清除缓冲区
        
2. **错误处理**：
    
    - 始终检查 `fgets()` 的返回值
        
    - 处理可能的读取错误或文件结束
        

c

#include <stdio.h>
#include <string.h>

int main() {
    char input[100];
    
    if (fgets(input, sizeof(input), stdin) != NULL) {
        // 成功读取
        input[strcspn(input, "\n")] = 0; // 移除换行符
        printf("输入: %s\n", input);
    } else {
        // 读取失败或到达文件末尾
        printf("读取失败或到达文件末尾\n");
    }
    
    return 0;
}

## 总结

`fgets()` 是C语言中读取字符串的安全方法，特别适合：

- 读取包含空格的字符串
    
- 需要防止缓冲区溢出的情况
    
- 读取整行输入
    

虽然需要额外处理换行符，但其安全性使其成为处理用户输入的首选方法。