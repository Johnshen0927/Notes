# Compatibility

## browser(浏览器版本之间的兼容性问题)

-  IE6、7不支持把块转成内嵌块
    -  解决方法:
                display:inline
                zoom:1
        触发 haslayout

- i9+ 才开始支持h5语义化标签

- 盒模型
    - w3c标准盒模型
        - content + padding + border + margin

    - IE 怪异盒模型
        - content(包含padding+border) + margin

- 占位宽
    - 低版本IE下，如果子级的宽高超过父级，那么会撑开父级的宽高

- height
    - IE6下，如果高度设置小于19px，会按照19px显示
        - 解决方法：overflow:hidden;

- 字体最小值
    - chrome的最小字体大小只能为12px
        - 解决方法：换成图片

- 边框
    - 在IE6，1px的点虚线会变成方虚线
        - 解决方法： 换成图片

- 浮动
    - 在ie6、7下li本身没有加浮动，但是li的内容都浮动了，或者有两个以上的浮动，li下边就会有几个px的间隙
        - 解决方法：
            1. 给li加浮动
            2. vertical-align:top;
    -  在ie6、7下浮动元素的父级设置了固定宽度的话，不需要清除浮动.**在正常浏览器下做不到**
    - 因为不接受after伪类，所以无法用clearboth去清除浮动
        - 解决方法： 添加zoom：1
            - 原理haslayout
    -  ie6下双边距bug，在ie6下，块元素有浮动有横向margin，横向的margin值会被放大成两倍
        - 解决方法： display:inline 
    - 在ie6下，一行元素的宽度之和 和 父级的宽度相差超过3px，则最后一行元素的下margin失效
    - 在ie6下，元素的宽度和父级宽度相差小于3px，并且两个浮动之后之间有注释或者内嵌元素，元素内容会被复制
        - 解决方法：用一个块标签包一下

- 定位
    - 在ie6下，当浮动元素和绝对定位元素，是同级关系的话（并且浮动元素的占位宽度和父级小于3px），绝对定位元素会消失掉
        - 解决方法： 用块把绝对元素包起来
    - 在ie6、7下，子元素有相对定位的话，父级的overflow包不住它
        - 解决方法：给父级也加position:relative
    - IE6下 不接受固定定位
        - 解决方法：使用js

- 透明
    - iE8 及以下不支持 opacity
        - 解决方法： filter: alpha(opacity=50);

- 表格
    - 在ie6、7下，不支持border-spacing这条样式
        - 解决方法:行间属性：cellspacing- 单元格间距

- 表单
    - IE6、7下， input上下各有1px的间隙
        - 解决方法：input加float
    - IE6下要去掉边框:
        - 解决方法：border：0;
    - 在ie6、7下，输入类型的表单控件，输入文字的时候背景图会跟随文字一块移动
        - 解决方法：给父级加背景

- 伪类
    - ie6下只支持link、visited、hover、active这四个伪类，并且只支持添加给a标签
    - ie7下只支持link、visited、hover、active
    - after/before 只接受8以上，如果要在低版本实现：通过js

- margin传递
    - 在ie6下，父级有边框的话，可能会造成子元素的margin失效
    - 解决方法：触发Haslayout

## 移动端兼容问题

- ios
    - 点击a,button,input标签会有阴影
        -  ```css
            a,input,button{
                -webkit-tap-highlight-color: rgba(0,0,0,0);
            }
          ```

    -  横竖屏切换的时候，大小会有变化
        - ```css
            body *{
                -webkit-text-size-adjust: 100%;
            }
          ```

    - ios按钮自带圆角
        - ```css
            input,button{
                -webkit-appearance: none;
                border-radius: 0;
            }
          ```

- 移动端tranform必须要加-webkit-