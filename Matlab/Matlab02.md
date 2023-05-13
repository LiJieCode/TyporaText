# Matlab02

matlab软件页面

matlab内置函数

matlab帮助文档

脚本

实时脚本



常用函数：

- 取整函数：

  - round  四舍五入 
  - fix  保留整数部分 
  - floor  向下取整 
  - ceil  向上取整 
  - sign  提取符号 
  - rem  取余数 
  - mod  取模数

- 随机函数：控制随机数生成器 rng();

  - rand() : rand(m,n) 生成0-1间**均匀分布**的随机矩阵(m行，n列)，如果m=n，则可简写为rand(m)

    ```
    生成a-b间均匀分布的随机矩阵(m行，n列)，如果m=n，则可简写。
    
    a+(b-a)*rand(m,n)
    4 7
    
    4 + 
    ```

    

  - randn() : randn(m,n)生成标准**正态分布**矩阵(m行，n列)，如果m=n，则可简写为randn(m)

  - randi (): 生成min到max之间的整数随机矩阵(m行，n列)，如果m=n，则可简写为`randi ([min,max],m)`矩阵规模计算：length(A) 和 size(A) 

- diag()；
- rot90()： 逆时针90
- linspace；
- repmat()：赋值矩阵
- sum ,abs, sqrt, min, max, mean, 
- sort(向量)
- 







``` 矩阵提取
先创建一个10*10的全零矩阵(zeros)，然后把后四行修改为1
先创建一个10*10的全一矩阵(ones)，然后把前六行修改为0
拼接：先创建一个6*10的全零矩阵，再创建一个4*10的全一矩阵，最后上下拼接
```







