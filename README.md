<h1 align="ceter">为ParaView增添三种colormap及定制易用colormap</h1>
---
###abele_n@163.com
###2015-12-06
###这个是我给ParaView的ColorMap增加的三种颜色配置。They are my three extensional colormaps for Paraview.
###如果有什么想法或者错误欢迎大家交流，谢谢！


##【使用说明(How to use)】
----
拷贝colormax.xml、colormin.xml、colorminandmax.xml文件到任意地方，推荐拷贝到ParaView的lib/paraview-4.4/site-packages/paraview/目录下，
然后在左边Properties/Display/Coloring下点击Edit，如下图所示：
<div align="center">
<img src="https://github.com/weiminghu07/colormap/blob/master/pics/1.png" alt=""/><br />
（第一步 点击Edit）
</div>

接着我们看到右手边出现Color Map Editor的窗口，如下图所示：
<div align="center">
<img src="https://github.com/weiminghu07/colormap/blob/master/pics/2.png" alt=""/><br />
（第二步 点击带有爱心文件夹的图标Preset）
</div>

点击带有爱心文件夹的图标Preset,然后会弹出一个窗口，如图所示（Then pop on a window）:
<div align="center">
<img src="https://github.com/weiminghu07/colormap/blob/master/pics/3.png" alt=""/><br />
（第三步 点击import）
</div>

然后点击import，随后出现下图：
<div align="center">
<img src="https://github.com/weiminghu07/colormap/blob/master/pics/4.png" alt=""/><br />
（第四步 找到你前面拷贝的文件，点击ok）
</div>

找到前面你存放的文件，然后选中，点击ok即可输入（注意ParaView不识别中文）。
ok之后出现下图：
<div align="center">
<img src="https://github.com/weiminghu07/colormap/blob/master/pics/5.png" alt=""/><br />
（第五步 点击Apply）
</div>

点击Apply，最后就出现了下图：
<div align="center">
<img src="https://github.com/weiminghu07/colormap/blob/master/pics/colormapformax.png" alt=""/><br />
（第六步 最终效果图）
</div>

我们可以通过Color Map Edit窗口右上角的带e的彩色按钮（Edit Color Legend Parameters）调节Legend参数。
如下图所示：
<div align="center">
<img src="https://github.com/weiminghu07/colormap/blob/master/pics/6.png" alt=""/><br />
（Legend参数设置）
</div>

我们和tecplot的效果比较一下：
<div align="center">
<img src="https://github.com/weiminghu07/colormap/blob/master/pics/tecplot.png" alt=""/><br />
（tecplot效果图）
</div>

我们可以看到，ParaView的每一层的值不对应，软件自带的颜色也是一样的。我不知道怎么解决，
如果哪位仁兄可以解决的话，希望不惜赐教。 


##我的三种颜色配置效果图
-----
###colormax.xml focus on Maximum
效果图如下：
<div align="center">
<img src="https://github.com/weiminghu07/colormap/blob/master/pics/colormapformax.png" alt=""/><br />
（colormax.xml显示样式——关注最大值）
</div>


###colorminandmax.xml focus on both Minimum and Maximum
效果图如下所示：
<div align="center">
<img src="https://github.com/weiminghu07/colormap/blob/master/pics/colormapformaxandmin.png" alt=""/><br />
（colorminandmax.xml显示样式——关注最大值最小值）
</div>


###colormin.xml focus on Minimum
效果图如下所示：
<div align="center">
<img src="https://github.com/weiminghu07/colormap/blob/master/pics/colormapformin.png" alt=""/><br />
（colormin.xml显示样式——关注最小值）
</div>


##【定制易用好看colormap(How to customize beautiful colormap)】
-----
如果有兴趣自己定义颜色组合的可以看看下面的内容：

###ParaView的ColorMap
ParaView支持的ColorMap文件格式有.xml（主要有matplotlib）和另一种Matlab格式的，因为ParaView默认的是.xml，
所以我只以.xml格式说明。ParaView的ColorMaps.xml文件放在lib/paraview-4.4/site-packages/paraview/目录下。

###ColorMap的xml格式
```
<ColorMaps>
    <ColorMap name="Blue to Red Rainbow" space="HSV">
     <Point x="0.0" r="0.0" g="0.0" b="1.0" o="0.0"/>
     <Point x="1.0" r="1.0" g="0.0" b="0.0" o="0.0"/>
     <NaN r="0.498039215686" g="0.498039215686" b="0.498039215686"/>
    </ColorMap>
</ColorMaps>
```
我们结合下面的图来讲解：
<div align="center">
<img src="https://github.com/weiminghu07/colormap/blob/master/pics/7.png" alt=""/><br />
（颜色显示控制）
</div>
通过点击Color Map Editor下的控制点（小圆点）可以得到上图。

1.
```
<ColorMaps>
...
</ColorMaps>
```
上面代码是固定格式。

2.
```
<ColorMap name="Blue to Red Rainbow" space="HSV">
...
</ColorMap>
```
上面代码表示一种颜色的界定。name表示这种颜色映射的名字，space表示其所属空间——在图
右下方Color Space可以看到。

3.
```
<Point x="0.0" r="0.0" g="0.0" b="1.0" o="0.0"/>
<Point x="1.0" r="1.0" g="0.0" b="0.0" o="0.0"/>
```
上面代码中x代表控制点位置（control point），就是图中的小圆点。r：red，g：green，
b：blue。o：opacity，透明度。x1<x2,...,xi<...xn,xi可为正也可为负，常用的是x1=0,xn=1
和x1=-1,xn=1。xi，x(i-1)用来控制某种颜色的宽度，某一种颜色的最终显示的宽度取决于
（xi-x(i-1)）/（xn-x1）和数据的分布。xi-x(i-1)可以用来调整数据分区的大小。

r,g,b控制整个颜色的最终显示，在xml中一般取值范围为0～1,在GUI面板中，对应着0～255。
那么，GUI面板中的r,g,b的实际值a1,a2,a3和xml中r,g,b的实际值b1,b2,b3可以用下式表示：
（（a1,a2,a3）/255） = （（b1,b2,b3）/1）。

o：opacity，透明度。为1是不透明，0为完全透明。

4.
```
<NaN r="0.498039215686" g="0.498039215686" b="0.498039215686"/>
```
NAN表示无穷值的表示颜色，在前述图中的右下角可以找到。

5.在做非离散图时，如我所提供的三种颜色配置，要注意前一种颜色和后一种颜色的控制点距离要小，
不然ParaView会在这两个控制点内随机插入颜色。做连续图时没有这个问题，如我上面的这个例子，你会发现
ParaView是在控制点间随机插入颜色，颜色顺序是按照GUI中select color中的颜色顺序排的。很明显，
上面这个例子只设置了两个控制点，两种颜色，我们看到的是下图的这种效果：
<div align="center">
<img src="https://github.com/weiminghu07/colormap/blob/master/pics/8.png" alt=""/><br />
（上述例子的显示效果）
</div>
ParaView的连续显示还可以，所以我没我有再弄连续的颜色配置文件。
下面给出我的colormax.xml:
```
<ColorMaps>
    <ColorMap name="FoucsMax" space="HSV">     
     <Point x="-1.00000000"  o="0.00000" r="0.00000" g="0.00000" b="1.00000"/>
     <Point x="-0.75000001"  o="0.00000" r="0.00000" g="0.00000" b="1.00000"/>
     <Point x="-0.75000000"  o="0.00000" r="0.00000" g="0.15000" b="1.00000"/>
     <Point x="-0.55000001"  o="0.00000" r="0.00000" g="0.15000" b="1.00000"/>
     <Point x="-0.55000000"  o="0.00000" r="0.00000" g="0.40000" b="1.00000"/>
     <Point x="-0.42500001"  o="0.00000" r="0.00000" g="0.40000" b="1.00000"/>
     <Point x="-0.42500000"  o="0.00000" r="0.00000" g="0.70000" b="1.00000"/>
     <Point x="-0.30000001"  o="0.00000" r="0.00000" g="0.70000" b="1.00000"/>
     <Point x="-0.30000000"  o="0.00000" r="0.00000" g="1.00000" b="1.00000"/>
     <Point x="-0.17500001"  o="0.00000" r="0.00000" g="1.00000" b="1.00000"/>
     <Point x="-0.17500000"  o="0.00000" r="0.17300" g="1.00000" b="0.50000"/>
     <Point x="-0.05000001"  o="0.00000" r="0.17300" g="1.00000" b="0.50000"/>
     <Point x="-0.05000000"  o="0.00000" r="0.06000" g="1.00000" b="0.20000"/>
     <Point x="0.07500000"  o="0.00000" r="0.06000" g="1.00000" b="0.20000"/>
     <Point x="0.07500001"  o="0.00000" r="0.00000" g="1.00000" b="0.00000"/>
     <Point x="0.22500000"  o="0.00000" r="0.00000" g="1.00000" b="0.00000"/>
     <Point x="0.22500001"  o="0.00000" r="0.40000" g="1.00000" b="0.08000"/>
     <Point x="0.35000000"  o="0.00000" r="0.40000" g="1.00000" b="0.08000"/>
     <Point x="0.35000001"  o="0.00000" r="0.70000" g="1.00000" b="0.08000"/>
     <Point x="0.47500000"  o="0.00000" r="0.70000" g="1.00000" b="0.08000"/>
     <Point x="0.47500001"  o="0.00000" r="0.99000" g="1.00000" b="0.08000"/>
     <Point x="0.60000000"  o="0.00000" r="0.99000" g="1.00000" b="0.08000"/>
     <Point x="0.60000001"  o="0.00000" r="1.00000" g="0.55000" b="0.08000"/>
     <Point x="0.72500000"  o="0.00000" r="1.00000" g="0.55000" b="0.08000"/>
     <Point x="0.7250001"  o="0.00000" r="1.00000" g="0.25000" b="0.03000"/>
     <Point x="0.8500000"  o="0.00000" r="1.00000" g="0.25000" b="0.03000"/>
     <Point x="0.85000001"  o="0.00000" r="1.00000" g="0.00000" b="0.00000"/>
     <Point x="0.95000000"  o="0.00000" r="1.00000" g="0.00000" b="0.00000"/>
     <Point x="0.95000001"  o="0.00000" r="0.70000" g="0.00000" b="0.00000"/>
     <Point x="1.00000000"  o="0.00000" r="0.70000" g="0.00000" b="0.00000"/>
     <NaN r="0.00000" g="0.00000" b="0.00000"/>
    </ColorMap>
</ColorMaps>
```


##小结
-----
本想看看ParaView的ColorMap函数和相关的类来研究一下，但是找了半天也没找到，如果谁知道的话麻烦不惜赐教。
后来只好参考其自带的ColorMap.xml文件研究，搞了一天才搞明白。所以写出来给大家做个参考，避免大家走弯路，
如果想自己定义颜色配置，可稍稍参考一下这篇文章。
如果对于这篇文章给各位带来了帮助，希望大家多多点赞。
谢谢！！！
