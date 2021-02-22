# 响应式开发

响应式开发：通俗点说就是元素样式自适应

#### 响应式开发原理

 就是使用媒体查询，针对不同的宽度的设备进行布局和响应的设置，从而适配不同设备的目的。

|         设备划分         |   尺寸区间   |
| :----------------------: | :----------: |
|     超小屏幕（手机）     |    <768px    |
|     小屏设备（平板）     | 768px~992px  |
|   中等屏幕（电脑桌面）   | 992px~1200px |
| 宽屏设备（大桌面显示器） |   >1200px    |

####  响应式布局

响应式布局需要一个父级作为布局容器，来配合子集元素来实现变化效果。

原理就是在不同屏幕下通过媒体查询来改变这个容器的大小。

再改变里面子元素的排列方式和大小，从而实现不同屏幕下看到不同页面布局和样式变化。

也就是说我们只根据布局容器的大小来改变子元素的布局和样式和变化

 平时我们的响应尺寸划分

*  超小屏幕设置宽度为 100%
* 小屏幕设置宽度为	750px
* 中等屏幕宽度设置为 970px
* 大屏幕宽度设置为	1170px。

``以上的屏幕划分只是常用的屏幕划分，你可以自己按需求进行划分``

```html
  /* 1、引入css样式 */
<link rel="stylesheet" href="./modules/bootstrap/css/bootstrap.css">
<style>
    .container{
       height: 200px;
       background-color: pink;
       margin: auto; 
    }
/* 设置布局容器的宽度 */
    /* 设置超小屏幕时，布局容器的宽度 */
    @media screen and (max-width: 767px){
        .container{width: 100%;}
    }
     /* 后面的会覆盖前面的样式，所以只需要写最小宽度就行 */
     /* 设置小屏幕时，布局容器的宽度 */
    @media screen and (min-width: 768px) {
        .container{width: 750px;}
    }
     /* 设置中等屏幕时，布局容器的宽度 */
    @media screen and (min-width: 992px) {
        .container{width: 970px;}
    }
     /* 设置大屏幕时，布局容器的宽度 */
    @media screen and (min-width: 1200px) {
        .container{width: 1170px;}
    }
</style>
```

#### bootstrap的响应式布局

##### 布局容器

``.container``:	bootstrap为我们预定义的一个响应式布局容器类，容器的宽度和上面响应式宽度设置的一样。我们需要自定义一个响应式组件时，就可以直接用这个类作为父级容器

*  超小屏幕设置宽度为 100%
* 小屏幕设置宽度为	750px
* 中等屏幕宽度设置为 970px
* 大屏幕宽度设置为	1170px。

``.container-fluid``:也是bootstrap预定义的一个布局容器，不是响应式的布局容器，是流式布局容器，适合于单纯的移动端设计。

* 百分百宽度
* 占据全部视图

# 栅格系统

 Bootstrap 提供了一套响应式、移动设备优先的流式栅格系统，随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多12列。它包含了易于使用的[预定义类](https://v3.bootcss.com/css/#grid-example-basic)，还有强大的[mixin 用于生成更具语义的布局](https://v3.bootcss.com/css/#grid-less) 

+ “行（row）”必须包含在 `.container` （固定宽度）或 `.container-fluid` （100% 宽度）中，以便为其赋予合适的排列（aligment）和内补（padding）。

+ 通过“行（row）”在水平方向创建一组“列（column）”。

+ 你的内容应当放置于“列（column）”内，并且，只有“列（column）”可以作为行（row）”的直接子元素。类似 `.row` 和 `.col-xs-4` 这种预定义的类，可以用来快速创建栅格布局。Bootstrap 源码中定义的 mixin 也可以用来创建语义化的布局。

+ 通过为“列（column）”设置 `padding` 属性，从而创建列与列之间的间隔（gutter）。通过为 `.row` 元素设置负值 `margin` 从而抵消掉为 `.container` 元素设置的 `padding`，也就间接为“行（row）”所包含的“列（column）”抵消掉了`padding`。

+ 负值的 margin就是下面的示例为什么是向外突出的原因。在栅格列中的内容排成一行。栅格系统中的列是通过指定1到12的值来表示其跨越的范围。例如，三个等宽的列可以使用三个  `.col-xs-4` 来创建。

+ 如果一“行（row）”中包含了的“列（column）”大于 12，多余的“列（column）”所在的元素将被作为一个整体另起一行排列。

+ 栅格类适用于与屏幕宽度大于或等于分界点大小的设备 ， 并且针对小屏幕设备覆盖栅格类。 因此，在元素上应用任何 `.col-md-*` 栅格类适用于与屏幕宽度大于或等于分界点大小的设备 ， 并且针对小屏幕设备覆盖栅格类。 因此，在元素上应用任何 `.col-lg-*` 不存在， 也影响大屏幕设备

#### 栅格参数

通过下表可以详细查看 Bootstrap 的栅格系统是如何在多种屏幕设备上工作的。

|                       | 超小屏幕            手机 (<768px) | 小屏幕            平板 (≥768px)                     | 中等屏幕            桌面显示器 (≥992px) | 大屏幕            大桌面显示器 (≥1200px) |
| --------------------- | --------------------------------- | --------------------------------------------------- | --------------------------------------- | ---------------------------------------- |
| 栅格系统行为          | 总是水平排列                      | 开始是堆叠在一起的，当大于这些阈值时将变为水平排列C |                                         |                                          |
| `.container` 最大宽度 | None （自动）                     | 750px                                               | 970px                                   | 1170px                                   |
| 类前缀                | `.col-xs-`                        | `.col-sm-`                                          | `.col-md-`                              | `.col-lg-`                               |
| 列（column）数        | 12                                |                                                     |                                         |                                          |
| 最大列（column）宽    | 自动                              | ~62px                                               | ~81px                                   | ~97px                                    |
| 槽（gutter）宽        | 30px （每列左右均有 15px）        |                                                     |                                         |                                          |
| 可嵌套                | 是                                |                                                     |                                         |                                          |
| 偏移（Offsets）       | 是                                |                                                     |                                         |                                          |
| 列排序                | 是                                |                                                     |                                         |                                          |

示例：

```html
 <!-- 一个 container 就是一个栅格系统，行数不限，列数最多 12  -->
   <div class="container">
       <!-- 一个 row 就是行 并不只是一行只是代表一个区域，row 只能放在 container中，但是container可以没有 row,row的直接子元素只能 列  
        -->
        <div class="row">
            <!-- 凑齐 12 就是一行 ，就是说，如果你想一列占一行，就写12 -->
            <!-- 当然也可以每列不平均，反正凑齐12就是一行，写x就是 占 x/12 x不能大于12-->
                <div class="col-xs-3  col-sm-3 col-md-6 col-lg-12">方格1</div>
                <div class="col-xs-3  col-sm-3 col-md-6 col-lg-12">方格2</div>
                <div class="col-xs-3  col-sm-3 col-md-6 col-lg-12">方格3</div>
                <div class="col-xs-3  col-sm-3 col-md-6 col-lg-12">方格4</div>
            
        </div>
   </div>
```

#### 列嵌套

```html
<div class="col-xs-3  col-sm-3 col-md-6 col-lg-12">
    <!-- 嵌套的时候可以直接写 列 ，但推荐再写一个 row ,这样父级列的 padding会被处理 -->
    <div class="row">
        <div class="col-lg-6 col-xs-6 col-sm-6 col-md-6 child">我是嵌套的1</div>
        <div class="col-lg-6 col-xs-6 col-sm-6 col-md-6 child">我是嵌套的2</div>
        <div class="col-lg-6 col-xs-6 col-sm-6 col-md-6 child">我是嵌套的3</div>
        <div class="col-lg-6 col-xs-6 col-sm-6 col-md-6 child">我是嵌套的4</div>
    </div>
</div>
```

![1591887145043](C:\Users\xiamin\AppData\Roaming\Typora\typora-user-images\1591887145043.png)

#### 列右偏移

空出几列来不要 .col-情形-offset-几列 表示在哪个情形下向右偏移几个列

````html
<div class="row">
    <div class="col-lg-4 col-xs-6 col-sm-4 col-md-4">我是左</div>
    <div class="col-lg-4 col-xs-6 col-sm-4 col-md-4 col-lg-offset-4">我是右</div>
</div>
````

![1591887293131](C:\Users\xiamin\AppData\Roaming\Typora\typora-user-images\1591887293131.png)

#### 列重置

重新排列 ``列``的位置

类似于列偏移,这个不会相互挤压，只会相互覆盖，向右推 col-lg-push-6，向左拉 col-lg-pull-4

```html
<div class="container">
    <div class="row" >
        <div class="col-xs-6  col-sm-6 col-md-6 col-lg-6 col-lg-push-6" style="background-color: silver;">方格1</div>
        <div class="col-xs-6  col-sm-6 col-md-6 col-lg-6 col-lg-pull-6" style="background-color: steelblue;">方格2</div>
    </div>
</div>
```



![1591887372137](C:\Users\xiamin\AppData\Roaming\Typora\typora-user-images\1591887372137.png)



#### 响应式工具

特定屏幕隐藏：hidden-lg      特定屏幕显示：visible-lg

```html
<div class="container">
    <div class="row" >
        <div class="col-xs-6  col-sm-6 col-md-6 col-lg-6 hidden-lg "style="background-color: silver;">大屏隐藏，其他显示</div>
        <div class="col-xs-6  col-sm-6 col-md-6 col-lg-6 visible-lg " style="background-color: steelblue;">大屏显示，其他隐藏</div>
    </div>
</div>
```

![1591887599982](C:\Users\xiamin\AppData\Roaming\Typora\typora-user-images\1591887599982.png)

