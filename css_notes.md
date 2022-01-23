# 组合器
适用于所有浏览器

## 后代组合器
单个空格连接，组合了两个选择器，第二个选择器是第一个的任一后代。  
A B {color: red} 表示：匹配所有位于任意 A 元素之内的 B 元素都呈现红色。

## 直接子代组合器
大于符号连接，选择前一个元素的儿子节点  
A > B {color: red} 表示： 匹配所有位于 A 元素之内的所有为B的儿子元素呈现红色，孙子等后代无效

## 一般兄弟组合起
波浪号连接，前后两个元素只需共享同一个父元素，不用相邻   
A ~ B 选择A元素之后所有同层级B元素。

## 紧邻兄弟组合起
加号连接，当第二个元素紧跟在第一个元素之后，并且两个元素都是属于同一个父元素的子元素，则第二个元素将被选中。
A + B，A后面紧跟着的B将被选中  
```html
<ul>
  <li>One</li>
  <li>Two!</li>
  <li>Three</li>
</ul>
```
```css
li:first-of-type + li {
  color: red;
}
/* Two!为红色 */
```

# 伪类
表示处于某种状态的一种选择器，鼠标、键盘等互动是状态，第几也是一种状态

## 形式：
开头为冒号的关键字

## 作用
和一般的DOM中的元素样式不一样，它并不改变任何DOM内容。只是插入了一些修饰类的元素，这些元素对于用户来说是可见的，但是对于DOM来说不可见，为处于这种特殊状态的元素添加效果。所以一个元素达到一个特定状态时，它可能得到一个伪类的样式；当状态改变时，它又会失去这个样式。

## 分类
1. 树结构
    - :root 文档根元素，比如HTML中的<html>，一般独立使用，用于生命全局变量
    - :empty 没有内容（text或者node，空格也属于text）的元素，如comment
    - :nth-child  冒号前的元素的所有兄弟元素（不论类型）中的第An+B个元素，n> = 0, An+B >= 1, AB可以为负数
    - :nth-last-child  倒数第An+B个
    - :first-child
    - :last-child
    - :only-child 等效 :first-child:last-child / :nth-child(1):nth-last-child(1)
    - :nth-of-type  冒号前的元素的所有同类兄弟元素（不论类型）中的第An+B个元素
    - :nth-last-of-type
    - :first-of-type    父元素容器内任意类型子元素的第一个元素
    - :last-of-type
    - :only-of-type

2. 用户操作
    - :hover 鼠标悬浮（div，button，a等元素都适用），可能有兼容性问题，会被:link, :visited, :active 重写，顺序为:link — :visited — :hover — :active
    - :active   被点击后的元素（button，a），会被:link, :visited, :active 重写
    - :focus    button、input、textarea由点击、触摸、tab键触发聚焦
    - :focus-visible     聚焦且user agent判断应当聚焦
    - :focus-within     子元素聚焦时选中父元素

3. 定位
    - :visited  被访问的链接
    - :link   未被访问的链接
    - :any-link  任何链接
    - :local-link  本地连接
    - :target   打开/跳转到对应id的元素，链接的href与id一致
        ```html
        <h3>Table of Contents</h3>
        <ol>
        <li><a href="#p1">Jump to the first paragraph!</a></li>
        <li><a href="#p2">Jump to the second paragraph!</a></li>
        </ol>

        <article>

        <h3>My Fun Article</h3>
        <p id="p1">You can target <i>this paragraph</i> using a
        URL fragment. Click on the link above to try out!</p>
        <p id="p2">This is <i>another paragraph</i>, also accessible
        from the links above. Isn't that delightful?</p>
        </article>
        ``` 

        ```css
        article:target-within {
        background-color: gold;
        }

        /* Add a pseudo-element inside the target element */
        p:target::before {
        font: 70% sans-serif;
        content: "►";
        color: limegreen;
        margin-right: .25em;
        }

        /* Style italic elements within the target element */
        p:target i {
        color: red;
        }
        ```
    - :target-within  匹配id的元素及其后代
    - :scope    在一个元素上调用，指代的是其本身，就像this

4. 输入（主要是与表单元素相关的）
    - :autofill 触发输入框自动填充状态时
    - :enabled  选中、点击、输入、聚焦等用户交互行为启用时
    - :diabled  选中、点击、输入、聚焦等用户交互行为禁用时
    - :read-only    只读模式开启时
    - :read-write   读写模式开启时
    - :placeholder-shown    input/textarea的占位符显示时
    - :default  表单元素的初始/默认状态 button未被点击状态，checkbox、radio input的勾选状态，select的选中状态
    - :checked radio、checkbox、option的选中状体啊
    - :indeterminate    既没有勾选又没有不勾选的模糊状态
    - :blank    input、textarea的空白状态，但很多浏览器不支持，慎用
    - :valid    required的input框有格式一致的内容时
    - :invalid  与上面相反
    - :in-range     标签设置了min和max的属性，当元素位于min和max之间时
    - :out-of-range     与上面相反
    - :required     input, select, textarea属性为required，则这些元素必填时
    - :optional     input, select, textarea没有required属性，则为选填
    - :user-invalid     表单提交时进行判断，只适用于firebox

5. 时间维度

    有时间轴的媒体资源（主要是文档，如视频字幕)，只适用于Safari
    - :current  
    - :past
    - :future
    ```html
    <video controls preload="metadata">
        <source src="video.mp4" type="video/mp4" />
        <source src="video.webm" type="video/webm" />
        <track label="English" kind="subtitles" srclang="en" src="subtitles.vtt" default>
    </video>
    ```

    ```css
    :current(p, span) {
        background-color: yellow;
    }

    :past(p, span) {
        display: none;
    }

    :future(p, span) {
        display: none;
    }
    ```

6. 资源状态

    视频等媒体资源
    - :playing  播放时
    - :paused   暂停播放时

7. 语义
    - :dir(ltr) / :dir(rtl) 文字内容左对齐/右对齐的元素 独立使用，需要在标签中定义dir=ltr
    - :lang(params) 所有包含params语言的元素 独立使用，需要在标签中定义lang=params，可以通过quotes给选中的元素改变引用样式，如加括号

# 伪元素
伪元素是一个附加至选择器末的关键词，允许对被选择元素的特定部分修改样式，用两个冒号表示

## 常用伪元素
- ::after
- ::backdrop    实验中的功能，任何处于全屏模式的元素下的即刻渲染的盒子（并且在所有其他在堆中的层级更低的元素之上），部分浏览器不兼容
- ::before
- ::cue     匹配所选元素中的WebVTT提示。这可以用于在VTT轨道的媒体中使用字幕和其他线索。部分浏览器不兼容
- ::first-letter
- ::first-line
- ::grammar-error   实验中的功能
- ::marker  通常用于li和summary，表示选中该元素的marker box，可以使用所有字体属性，color，content，颜色IE不兼容，部分手机浏览器不兼容
- ::placeholder 实验中的功能，可以选择一个表单元素的占位文本
- ::selection   被选中高亮时
- ::slotted()   参数为*或者标签，仅仅适用于影子节点树(Shadow Dom). 并且只会选择实际的元素节点，而不包括文本节点，IE不兼容
- ::spelling-error  实验中的功能，还不能使用

# 优先级
当一个元素有多个声明的时候，会给每个元素分配权重，优先执行分数最高的选择器  
1. 类型选择器和伪元素+1，类、伪类和属性选择器+10，ID选择器+100，他们构成的组合器对全部部分进行分数加总
2. 通配符、关系选择符、:is()、:not()对优先级没有影响, +0
3. !import最先执行，其次行内样式， !import可以提升样式优先级，但不建议使用；都使用!import时权重决定优先级
4. 直接添加的样式优先级高于继承
5. 后写的会覆盖先写的（内联样式和外联样式在html中也是一样）






