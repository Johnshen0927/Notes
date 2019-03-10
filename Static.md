# css随笔

## 内嵌块，内嵌，块的特征

- 块
    - 独占一行
    - 不设置高度，则有内容撑开
    - 不设置宽度，宽度会撑满整个父级w
    - 可以接受所有的样式

- 内嵌
    - 一行显示多个，一行宽度不够则会换行
    - 换行产生间隙
    - 不接受宽高的设置
    - 上下元素margin/padding有问题

- 内嵌块
    - 一行可显示多个
    - 换行会产生间隙
    - 接受宽高的设置
    - 下方存在默认间隙 (使用vettical-align:top实现对齐)

## BFC

- Block Formatting Context
- 作用
    - 不会被浮动元素覆盖
    - 防止margin的传递
    - 包含浮动的子元素，使子元素参与父级高度的计算
- 触发条件
    - float不为none
    - display为:inline-block/table-cell/table-caption
    - position:absolute/fixed
    - overflow不为visible

## haslayout

- ie渲染引擎中的一个属性，用来调节元素的渲染模式，当我们把这个属性设置为true的话，这个元素就根据自身的内容大小或者父级的大小重新计算自己的宽高
- 触发haslayout的样式
    - display：inline-block
    - height不为auto
    - float不为none
    - position：absolute
    - width不为auto
    - writing-mode:tb-rl（改变文字排版为竖向）
    - zoom不为normal

## 浮动的特征

- 使元素排列在一行
- 换行没有间隙
- 内嵌元素支持宽高
- 不设置宽高则由内容撑开
- 触发BFC
- 可以控制浮动方向，只有当遇到**父级元素边界**或者**上一个具有浮动的元素**，才会停止浮动
- 脱离文档流
- 解决margin重叠的问题

## 清除浮动的方法

- 加固定宽高
- 父级添加:
            <!-- .clearFix:after{
                content:'';
                display:block;
                clear:both;
            } -->
- 触发BFC

## 实践

- 如何使一个宽200px高300px的div在屏幕水平垂直居中？
    ```css
    .div1{
    width: 200px;
    height: 300px;
    background: red;
    position: absolute;
    left:50%;
    top:50%;
    margin-left: -100px;
    margin-top: -150px;
    }
    ```
- 如何使一个宽高未知的图片，在一个盒子里水平垂直居中？
    - 方法1：通过给父级加display:table-cell，并且加上vertical-align:middle
    - 方法2：给同级的子元素，写一个和父级一样的高度，使其成为同级元素中最高的元素。然后使用vertical-align:middle会让图片和最高的元素垂直居中

## 常用的默认样式清除

- a:text-decoration:none;
- img:border:none;vertical-align:top;
- ul/ol:margin:0;padding:0;list-style:none;
- h1-h6:margin:0;
- p:margin:0;
- body:margin:0;
- dl/dd:margin:0;
- em:font-style:normal
- strong:font-weight:normal;
- mark:background:none;