# Matlab03

matlab分支循环





```matlab
% 函数功能：计算给定矩阵主、副对角线元素的和
% 输入：任意方阵A
% 输出：方阵A的主、副对角线元素的和


function y = sum_all(A)
% 函数功能：计算给定矩阵主、副对角线元素的和
% 输入：任意方阵A
% 输出：方阵A的主、副对角线元素的和
% A = [ 1 2 3 ; 4 5 6 ; 7 8 9];


%%
n = size(A,1);
sum1 = sum(diag(A));
sum2 = sum(diag(rot90(A)));
sum3 = sum1 + sum2;
%%
if mod(n, 2) == 0
    y = sum3;
else
    index = ceil(n / 2);
    y = sum3 - A(index, index);
end
end
```









```Matlab
% 利用Matlab编写代码, 从键盘获取一个正整数n的值, 计算“n+nn+nnn+nnnn+nnnnn+nnnnnn“值。

% （举例说明：n=2时，计算2+22+222+2222+2222+22222的值）

clc;
clear;  
n = input('n=');
sum = 0;
temp = 0;
for i = 1:6
    temp = 10*temp + n;
    sum = sum + temp;
end
disp(sum);
```

