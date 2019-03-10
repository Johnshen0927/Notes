# 常见布局

## 双飞翼圣杯布局

- 两侧宽度固定，中间宽度随页面宽度变化而变化

```html
<div class="left"></div>
<div class="right"></div>
<div class="center"></div>
```

```css
body{
    margin:0;
}
.center{
    height: 400px;
    margin: 0 210px 0 300px;
    background: red;
}
.left{
    width: 290px;
    height: 400px;
    background: green;
    position: absolute;
    left: 0;
    top: 0;
}
.right{
    width: 200px;
    height: 400px;
    background: orange;
    position: absolute;
    right: 0;
    top: 0;
}
```

## 等高布局

```html
    <div class="box">
        <div class="left"></div>
        <div class="right"></div>
    </div>
```

```css
    .box{
    border: 5px solid #000;
    color: #fff;
    font-size: 24px;
    width: 600px;
    overflow: hidden;
    /* background: red; */
}
.left{
    background: red;
    float: left;
    width: 200px;
    padding-bottom: 999px;
    margin-bottom: -999px;
}
.right{
    background: green;
    float: right;
    width: 400px;
    padding-bottom: 999px;
    margin-bottom: -999px;
}
```