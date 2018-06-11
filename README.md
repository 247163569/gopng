GoPng
=====

GoPng

## live demo
http://alloyteam.github.com/gopng/

## rem雪碧图使用

将需要的小图标拖进去，全部拖进去后再调位置（每拖一个进去都会帮你排列好，但是没有间隔，所以全部拖进去后自己调）

然后点击右边绿色的make按钮即可

点击后，上面的选项会高亮，提示你制作好了，

点击PNG选项即可下载制作好的雪碧图， 点击css选项即可查看每个小图标在雪碧图中对应的x和Y位置

对于PC端来说，基本就完成了。

对于移动端采用rem布局的，则需要多一些步骤：

首先将对应的x和y位置转化为rem:以640设计稿为例，html的fontsize为64px（本例假设采用了淘宝的flex.js）

假设某个小图标对应雪碧图的x y位置为-200px , -100px

则对应的x位置为-200/64(rem)  Y坐标为-100/64(rem);

此外，还需要background-size配合，假设制作好的雪碧图为400*300，

则设置:background-size: 400/64(rem)  300/64(rem) 或者:background-size: 400/64(rem)  auto   或者直接  background-size: 400/64(rem)；

如此一来，即使使用了rem布局在移动端也可以大胆的使用雪碧图了，但是在rem转化的时候计算非常麻烦，因此可以再sass文件里添加2个方法：

//将px转化为rem（根据html的fz进行转化）

@function torem($px) {
       @return $px / 64px * 1rem;
}

//定制mixin代码块：需要4个参数：图片地址，x轴位置，Y轴位置，雪碧图宽度

@mixin spImg($url, $left, $top, $imgWidth ) {
        background: url($url) no-repeat $left $top;
        background-size:$imgWidth;
}

使用的时候如下：

.share｛
  @include spImg("../../img/sprite.png",torem(-115px),0,torem(424px))
｝
