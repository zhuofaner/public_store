# [三栏排版](1)

> 三栏排版是果酱V视 app 内部采用的一种排版方法，使用自行扩展的 html 标签语法，具有可扩展、快速和自组合的特点，是编写精美的菜单项最重要的利器。

## 基本标签

三栏排版顾名思义采用 `左(left)` `中(center)` `右(right)` 三组标签进行排版，默认每一组标签单独占据一行。

> 所谓标签，就是一组尖括号开头后接标签名 中间用空格分隔属性名和值并以反斜线和尖回括的一种文本格式（去掉了包裹特性）。

```jamv
<left 我在左边/><center 我在中间/><right 我在右边/>
```


![ignore]()

如果需要将任意两行合并，使用 `merged` 关键字，注意该关键字只对下一栏标签有效。

> 注意⚠️：不是下一条标签，下面会讲一栏标签的作用范围。

### merged 效果1

```jamv
<left 我在左边 merged/><center 我在中间/><right 我在右边/>
```

![ignore]()

### merged 效果2

```jamv
<left 我在左边/><center 我在中间 merged/><right 我在右边/>
```

![ignore]()

### merged 效果3

```jamv
<left 我在左边 merged/><center 我在中间 merged/><right 我在右边/>
```

![ignore]()

## 分隔标签

我们当然不能只使用这么简单的场景，如果我们给每一栏增加一个图标，一个后缀，并且设置不同的文字大小、颜色甚至导入不同的图片、动画，该如何操作呢？

将一栏标签分割成若干个子标签的标签叫分隔标签，它们是  `start`  和  `end` ，为了说明你分隔的是哪一栏，你必须在使用 start 和 end 作为开头标签和结束标签时至少带上一次分栏信息。

```
<start/><right-end/>
<center-start/><end/>
<left-start/><p/><left-end/>
```

以上都是合法的使用方式，唯独不能同时使用 start 和 end 作为开头和结尾，因为无法判断是哪一栏。(left? center? 还是right?)

> start 和 end 中间可以添加任意数量的标签，他们共同组成了这一栏的内容，通常会拆分出独立的属性到单独的标签中。

分隔后你就可以开始针对分隔的字符进行单独设置，你注意到我使用到了属性这个概念，`标签` 和 `属性` 都是xml 和 html 的概念，不必拘泥于某个未知领域的学习，果酱V做了简化，标签名字也可以是属性名，反之亦然。

#### 一个居右的彩色点击提示符

```jamv
<right-start big 点击进入/><green small text=">"><small red text=">"><blue end small text=">">
```

![ignore]()

> 看到了么，在这一个示例中我们几乎是用了所有类型的属性作为标签名字，理论上一个单独的一栏或者被merged 过的标签都是`<p>` 元素也就是行内元素，这与`<div>` 块状元素相对应，他们的区别就是是否需要换行。

## 定宽

三栏排版让我们对菜单项有了基本的美化，然而面对长短不一的标题文字我们有时候又很无助。

使用 `width`、`height` 标签族进行栏目的宽度固定，从而得到统一的视觉效果。

```jamv
<center 标签名 merged/><right width_75 说明 merged/><right width_75 标签族/>
<center text="minWidth" merged/><right width_75 设置最小宽度 merged/><right width_75 text="width"/>
<center text="maxWidth" merged/><right width_75 设置最大宽度 merged/><right width_75 text="width"/>
<center text="minHeight" merged/><right width_75 设置最小高度 merged/><right width_75 text="height"/>
<center text="maxHeight" merged/><right width_75 设置最大高度 merged/><right width_75 text="height"/>
```

> 所有标签属性都有标准的赋值写法 例如: text="我是内容", width="75" 然后直接使用标签的简写方式 `<p width_75 我是内容/>` 更加酷炫！
>
> 注意⚠️：有特殊字符或者不想作为属性解析时必须使用标准写法。

以上我们使用定宽创造了一种表格的写法，虽然 markdown 有自己的表格书写方式，但是还不够灵活。

# [让菜单更生动](2)

> 让菜单更加生动的手段有很多种，设置文字背景图、图标、emoji表情甚至动画。

## 设置可伸缩的背景图

我们来一起实现一下alpha3版本 `最新活动` 里设置的炫酷效果吧：

```jamv
<left width_55 src="http://gitee.com/da-jia-vinci-studio/public_store/raw/master/pic/jack-small.png" bottom merged/>
<bg center-start padding_7_14_7_25 9patch_15_5_27_20 src="http://gitee.com/da-jia-vinci-studio/public_store/raw/master/pic/dialog-style-pink.png"/><center-end #ff0000 大家好，我是果酱V视APP的设计师Jack，这是一份背景图测试/>
```

![ignore]()

- `src` 属性，定义网络图片、动画，没有简写形式。
- `bg` 属性，配合 `src` 成为本栏的背景图。
- `padding` 属性，内边距。目前仅支持简写形式，padding\_[left]\_[top]\_[right]\_[bottom]
  - [] 中括号内为数字
  - left、top、right、bottom 代表距离左边、上边、右边和下边的距离。
- `9patch` 属性，伸缩属性，google 发明的用于 android 开发的一种内置 padding 和 伸缩数据在图片中的。目前仅支持简写形式，9patch_[left]\_[top]\_[right]\_[bottom]，用法同上。

[点击这里详细了解9patch技术](https://developer.android.com/studio/write/draw9patch?hl=zh-cn)

## 纵向排列

之前我们一直在讲分栏，左中右实际是一种横向排列，在一个长列表中纵向往往是自然延伸的。然而当我们设置了分栏对应了不同大小的图标、背景图、不同长度的文字时，我们使用 `top` `middle` `bottom` 这组标签让它们获得理想的纵向排列效果。

