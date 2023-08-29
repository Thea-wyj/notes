# Markdown

<span id="jump">目录</span>

[TOC]

## 符号及公式

![image-20210120152122362](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210120152122362.png)

​                                                                                eg:   $\delta$   

### 数学符号

![image-20210120152257440](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210120152257440.png)

#### 希腊字母

![image-20210120152308868](C:\Users\11934\AppData\Roaming\Typora\typora-user-images\image-20210120152308868.png)

![image-20210120152328242](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210120152328242.png)

[点击跳转到目录](#jump)

#### 二元关系符

可以通过在下述命令前加上\not 来得到其否定形式，如\not >即为$\not >$。

![image-20210120152450548](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210120152450548.png)

#### 二元运算符

![image-20210120152552637](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210120152552637.png)

#### 大尺寸运算符

![image-20210120152611124](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210120152611124.png)

#### 箭头

![image-20210120152630565](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210120152630565.png)

#### 其他符号

![image-20210120152649220](C:\Users\11934\AppData\Roaming\Typora\typora-user-images\image-20210120152649220.png)

### 公式

#### 函数

![image-20210120152735068](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210120152735068.png)

#### 积分、求和

![image-20210120152752430](C:\Users\11934\AppData\Roaming\Typora\typora-user-images\image-20210120152752430.png)

![image-20210120152803750](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210120152803750.png)

![image-20210120152830011](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210120152830011.png)

eg： $\begin{matrix} \prod_{i=1}^N x_i \end{matrix}$

#### 矩阵、方程

![image-20210120153003774](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210120153003774.png)

![image-20210120153020179](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210120153020179.png)

若想在公式或方程后添加编号，只需添加`\tag{序号}`即可，如：

$$ax+by+c=0\tag{1.1}$$

## 排版

#### 表格

**Markdown推荐的标准表格**
| 左对齐 | 右对齐   | 居中    | 效果      | 语法    | 效果      | 语法     | 效果        |

| :---- | ------: | :-------: | --------- | ------- | --------- | -------- | ----------- |

| \sum | $\sum$ | \bigcup | $\bigcup$ | \bigvee | $\bigvee$ | \bigolus | $\bigoplus$ |

| 左对齐 | 右对齐   | 居中    | 效果      | 语法    | 效果      | 语法     | 效果        |
| :---- | ------: | :-------: | --------- | ------- | --------- | -------- | ----------- |
| \sum | $\sum$ | \bigcup | $\bigcup$ | \bigvee | $\bigvee$ | \bigolus | $\bigoplus$ |

由于Markdown兼容html语法，因此可以用html语法生成一些复杂形式的表格。如下面可合并行列的表格：

<table><tbody>
    <tr>
        <th rowspan=3>合并行</th>
        <th>第一列</th>
        <th>第二列</th>
        <th>第三列</th>
    </tr>
    <tr>
        <td colspan=2>合并列</td>
        <td rowspan=2>第三列</td>
    </tr>
    <tr>
        <td><img src="http://latex.codecogs.com/gif.latex? \omega" /></td>
        <td><img src="http://latex.codecogs.com/gif.latex? 35*d_2" /></td>
    </tr>
</table>  

插入公示，只需添加

![image-20210120161839248](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20210120161839248.png)

<img src="http://latex.codecogs.com/gif.latex? \sum" />

### 图片

插入图片时，可以直接复制粘贴一张图，图片可以是任意位置的图片，粘贴进来会自动生成地址，不用担心图片挪动位置导致图片不显示。但直接复制粘贴的图片默认是居左显示的，如下图：

![在这里插入图片描述](https://img-blog.csdn.net/20181011190106378?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM5MTQ0NzE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

如果想调整图像大小，只需在代码后面添加尺寸约束“ =200x”（宽x高），尺寸可以自定义，在不确定图像比例的情况下可以省略高度信息：

![在这里插入图片描述](https://img-blog.csdn.net/20181011190106378?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM5MTQ0NzE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70 =200)

或者用html

<img src="https://img-blog.csdn.net/20181011191327845?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM5MTQ0NzE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="500" hegiht="313" />

若想让图片居中或者居右显示，则替换align=center或right

<div align=center><img src="https://img-blog.csdn.net/20181011191327845?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM5MTQ0NzE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70"/></div>

## 页内跳转

页内跳转除了通过Markdown默认的目录功能外，还可以通过HTML中的设置锚点的方式进行。具体操作如下：
在需要跳转至的地方设置锚点：

在需要点击进行跳转的地方链接锚点id：


[baidu](https://www.baidu.com/)