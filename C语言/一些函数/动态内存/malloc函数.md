形式： `#include<stdlib.h>//头文件`  
        `int *p;`
        `p=(int*)(malloc(5*sizeof(int )));`
          `free(p);//释放内存`
          `p=NULL;//p变成空指针`
也可用[[calloc函数]].
不初始化（垃圾值）；
较快（不用初始化）。
