形式：整体同[[malloc函数]]
     `p=(int *)(calloc(5,sizeof(int)));`
同样需要free，p=NULL;
初始化全为零‘；
较慢（因为要初始化）。