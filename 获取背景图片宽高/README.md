# js获取背景图片宽高

有时候我们经常需要为一些页面更换背景图片，而设计师每次给的背景图片宽高可能不一样，这就为我们更换背景时带来了不便，最笨的办法就是每次根据背景图片的大小手动更改css样式中背景容器的宽高；稍微smart一点的办法就是，在html文件中增加一个`<img>`标签，将`<img>`标签的`src`属性指向背景图片的地址，将该<img>标签隐藏不可见，然后利用js获取该`<img>`的宽高；再稍微smart一点的就是利用js先获取背景图片的路径，然后利用`new Image()`新建一个图片对象，并将背景图片的路径赋值给新建图片对象的`src`，最后获取背景图片的宽高。笨办法就不说了，下面将简单介绍一下后两种方法：

### 利用js新建一个<img>标签来实现：

关键代码：

html：
```
<div class="wrapper">
    <img class="bgImg hide" src="../img/bg.jpg">
</div>
```

css：
```
.wrapper{
    position:relative;
    width:100%;
    overflow:hidden;
    background:url(../img/bg.jpg) top left no-repeat;
    background-size:100% auto;
}
.hide{
    position:absolute;
    top:0;
    left:0;
    z-index:-1;
    opacity:0;
}
```

js：
```
// 获取背景图片的宽高
var bgWidth = $('.bgImg').width(),
    bgHeight = $('.bgImg').height();
console.log(bgWidth);
console.log(bgHeight);
```

`Demo`:point_right:[演示地址](https://mxxumin.github.io/fragment/%E8%8E%B7%E5%8F%96%E8%83%8C%E6%99%AF%E5%9B%BE%E7%89%87%E5%AE%BD%E9%AB%98/demo1/index.html):point_left:`别忘了这是移动端的页面哦！！！`

### 利用`background-iamge、new Image()`来实现：

关键代码：

```
// 获取背景图片的url
var bgImg = $('.wrapper').css('background-image');

// 对url进行提取，提取出背景图片的路径地址
var bgImgSrc = bgImg.split('("')[1].split('")')[0];

// 新建一个图片对象
newImg = new Image();

// 将背景图片的路径赋值给新建的图片对象
newImg.src = bgImgSrc;

// 获取背景图片的宽高
console.log(newImg.width);
console.log(newImg.height);
```

其中`wrapper`为背景图片的容器。

`Demo`:point_right:[演示地址](https://mxxumin.github.io/fragment/%E8%8E%B7%E5%8F%96%E8%83%8C%E6%99%AF%E5%9B%BE%E7%89%87%E5%AE%BD%E9%AB%98/demo2/index.html):point_left:`别忘了这是移动端的页面哦！！！`

> 值得注意的是，如果图片和代码保存在本地，且在本地运行上面代码时，可能得到的背景图片宽高为0，不过不要紧，当把图片和代码放在线上时就不会出现上述问题。

### 参考文献：
[js获取背景图片的宽高大小](http://www.wanhui027.com/html/201512/a179.htm)