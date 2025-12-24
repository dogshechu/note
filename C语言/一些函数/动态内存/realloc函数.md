```
int *p;
p=(int*)(malloc(5*sizeof(int )));
int  *new_p=(int*)realloc(p,10*sizeof(int ));
```
当返回成功时，返回指向重新分配内存块的指针，当返回失败时，返回NULL,原内存块保持不变。
在[[malloc函数]]  [[calloc函数]]所定义的内存不够时，来扩大或缩小内存块。
     