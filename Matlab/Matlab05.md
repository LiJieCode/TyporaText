# Matlab05

画图：



函数 plot  



h = plot()





一个句柄：

**gcf**  % 获取当前图形窗口句柄  -  figure

窗口背景颜色：

```matlab
color：
```



**gca** % 获取当前坐标轴句柄  -  axe

```matlab
set(gca,'color','green')


# 坐标轴描述
XLabel
YLabel
title
Legend

# 坐标轴区间  限制 （给两个断点值）[-5 5]
XLim 
YLim


# 坐标轴  打刻度 （给一个向量） -5:5
XTick
YTick


# 小刻度
XMinorTick
YMinorTick


# 坐标轴网格 是否打网格  'on'   'off'
XGrid
YGrid
Grid on


# 刻度标记的显示
TickDir   in   out  both 


# 坐标轴的位置
XAxisLocation   bottom[ˈbɒtəm]   top 
YAxisLocation   left             right
```



**gco** % 获取被鼠标最近点击对象的句柄





GUI操作
