`strtol` 是C语言标准库中的一个函数，用于将字符串转换为长整型（long int）。它的功能比`atoi`更强大、更安全。
## **函数原型**

c

`long int strtol(const char *str, char **endptr, int base);`

## **参数说明**

- `str`：要转换的字符串
    
- `endptr`：指向字符指针的指针，用于存储转换结束的位置
    
- `base`：进制基数（2-36之间，0表示自动检测）
