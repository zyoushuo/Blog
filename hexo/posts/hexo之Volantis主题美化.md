---
title: hexo之Volantis主题美化
tags:
  - 博客
pin: true
categories:
  - 博客
abbrlink: 1788
date: 2020-05-22 16:26:03
description: 所有的主题美化都是相通的，各自有各自的风格。不同之处在于语法格式有些差异。本文主要结合Volantis主题，对其进行了一些优化。<img src="https://cdn.jsdelivr.net/gh/zyoushuo/Blog/images/meihua_1.jpg">
icons: [fas fa-fire red]
thumbnail: https://cdn.jsdelivr.net/gh/zyoushuo/Blog/emoji/ya/ya-5.jpg
sidebar: []
---

<!-- more -->

<p style="font-size:25px;font-family:SimSun;font-weight:bolder">更新</p>

<p style="font-size:14px">2020.7.20</p>

{% radio cyan ,  valine评论区卡片式背景%}

{% radio cyan ,  添加鼠标样式%}

{% radio cyan ,  文章首字下沉%}

{% radio cyan ,  文章末尾版权%}

{% radio red checked,  修改页面卡片阴影%}

<p style="font-size:14px">2020.6.15</p>

{% radio cyan ,  valine表情区域样式%}

{% radio cyan ,  主页、正文区域文章标题居中%}

{% radio cyan ,  博客文章链接优化%}

🌸<span style="font-size:20px"> 写在前面</span>

{% note warning, 本教程适用于Volantis2.6.4及以上的版本，如果版本不同，文件位置可能会有些不同。不过总体不影响。可以查看作者更新文档。当然也不仅局限于Volantis主题，其他主题按照自身的语法格式同样可修改。

Volantis主题已升级到3.0版本，有些文件位置与2.X版本有所不同，文中会提出。
%}

{% noteblock bug red %}
本文中涉及到修改.styl后缀的文件时一定要注意格式，不能多一个或少一个空格
{% endnoteblock %}

{% checkbox blue checked, 主界面优化 %}
{% checkbox blue checked, 页面优化 %}
{% checkbox blue checked, 评论区优化 %}

### 主界面显示

#### 设置主页logo

默认显示文字显得有些单调，故选择使用图片logo代替文字显示标题。修改主题配置文件`_config.yml`中的cover，添加logo属性值。

#### 添加小标题动态彩色字体

修改主题配置文件`_config.yml`中的cover。去除subtitile属性值；在 themes/volantis/layout/_cover中index.ejs文件中添加如下代码(文字部分可修改)：

{% folding green, 查看代码 %}

```javascript
<!-- 封面滚动字体 -->
<div id="binft"></div> 
<script>
    var binft = function (r) {
      function t() {
        return b[Math.floor(Math.random() * b.length)]
      }  
      function e() {
        return String.fromCharCode(94 * Math.random() + 33)
      }
      function n(r) {
        for (var n = document.createDocumentFragment(), i = 0; r > i; i++) {
          var l = document.createElement("span");
          l.textContent = e(), l.style.color = t(), n.appendChild(l)
        }
        return n
      }
      function i() {
        var t = o[c.skillI];
        c.step ? c.step-- : (c.step = g, c.prefixP < l.length ? (c.prefixP >= 0 && (c.text += l[c.prefixP]), c.prefixP++) : "forward" === c.direction ? c.skillP < t.length ? (c.text += t[c.skillP], c.skillP++) : c.delay ? c.delay-- : (c.direction = "backward", c.delay = a) : c.skillP > 0 ? (c.text = c.text.slice(0, -1), c.skillP--) : (c.skillI = (c.skillI + 1) % o.length, c.direction = "forward")), r.textContent = c.text, r.appendChild(n(c.prefixP < l.length ? Math.min(s, s + c.prefixP) : Math.min(s, t.length - c.skillP))), setTimeout(i, d)
      }
      var l = "",
      o = ["山有木兮木有枝，心悦君兮君不知。", "人生若只如初见，何事秋风悲画扇。","十年生死两茫茫，不思量，自难忘。", "曾经沧海难为水，除却巫山不是云。","洛中何郁郁，冠带自相索。","只愿君心似我心，定不负相思意。","愿得一心人，白头不相离。","入我相思门，知我相思苦。"].map(function (r) {
      return r + ""
      }),
      a = 2,
      g = 1,
      s = 5,
      d = 75,
      b = ["rgb(110,64,170)", "rgb(150,61,179)", "rgb(191,60,175)", "rgb(228,65,157)", "rgb(254,75,131)", "rgb(255,94,99)", "rgb(255,120,71)", "rgb(251,150,51)", "rgb(226,183,47)", "rgb(198,214,60)", "rgb(175,240,91)", "rgb(127,246,88)", "rgb(82,246,103)", "rgb(48,239,130)", "rgb(29,223,163)", "rgb(26,199,194)", "rgb(35,171,216)", "rgb(54,140,225)", "rgb(76,110,219)", "rgb(96,84,200)"],
      c = {
        text: "",
        prefixP: -s,
        skillI: 0,
        skillP: 0,
        direction: "forward",
        delay: a,
        step: g
      };
      i()
      };
      binft(document.getElementById('binft'));
  </script>
```

{% endfolding %}

```diff 文章地址 themes/volantis/layout/_cover/index.ejs 
  <div class='a'>
    <% if (theme.cover.logo) { %>
      <img class='logo' src='<%- url_for(theme.cover.logo) %>'/>
    <% } %>
    <% if (theme.cover.title) { %>
      <p class="title"><%- theme.cover.title ? theme.cover.title : config.title %></p>
    <% } %>
    <% if (theme.cover.subtitle) { %>
      <p class="subtitle"><%- theme.cover.subtitle%></p>
    <% } %>
+     此处添加代码
  </div>
```

<span style="color:red">这个滚动字体可以加在任何位置。</span>

#### 界面间距

原界面处title,subtitle,searc,menu之间间距感觉有点大，所以调整了一下。在 themes/volantis/source/css/_layout中的`cover.styl`文件修改margin-top，margin-bottom的值。

{% folding green, 查看代码 %}

```yaml
.cover-wrapper .cover
  top: 0
  left: 0
  max-width: 100%
  height: 100vh
  display: flex
  flex-wrap: nowrap
  flex-direction: column
  align-items: center
  align-self: center
  align-content: center
  color: $color-site-inner
  padding: $gap
  .cover-body
    div.b
      margin-top: 3vh
      margin-bottom: 8vh
```

{% endfolding %}

另：在界面中导航栏部分默认第一个会有下划线，如下

![](https://cdn.jsdelivr.net/gh/zyoushuo/Blog/images/meihua_2.png)

去除方法：在themes/volantis/source/css/_layout中`cover.styl`文件，大概在148行处，删除border-bottom属性

``` diff 文章地址 themes/volantis/source/css/_layout/cover.styl
    ul>li>a
      font-size: $fontsize-meta
      padding: 2px
      margin: 4px
      trans()
      color: alpha($color-site-inner, .65)
      text-shadow: 0 1px 2px rgba(0, 0, 0, 0.05)
      border-bottom: 2px solid transparent
      i
        margin-right: 4px
      &:hover, &.active, &:active
        color: $color-site-inner
-       border-bottom: 2px solid $color-site-inner(删除此行)
```

总体效果：

![](https://cdn.jsdelivr.net/gh/zyoushuo/Blog/images/meihua_1.png)

### 页面优化

#### 导航栏样式

主要是在原基础上添加了一个渐变背景。
首先在主题配置文件`_config.yml`中navbar的effext毛玻璃特效（blur）去掉。

``` diff 文章地址 volantis/_config.yml
style:
  font_smoothing: false # font-smoothing for webkit
  max_width: 1280px # Sum of body width and sidebar width (This limit will be exceeded           when the device width is greater than 2000px, reaching 75% of the total width)
  scrollbar:
    size: 4px
    border: 2px
    color: '#2196f3'
    hover: '#ff5722'
  navbar:
    height: 64px
    width: auto # auto, max
-   effect: [shadow, blur] # [shadow, floatable, blur]
+   effect: [shadow] # [shadow, floatable, blur]
```

然后在themes\volantis\source\css\\_layout\navbar.styl中，大概25行处添加代码

{% folding green, 查看代码 %}

```yaml
background-image: linear-gradient(to top, #fff1eb 0%, #ace0f9 100%);
```

{% endfolding %}

```diff 文章地址 themes\volantis\source\css\_layout\navbar.styl
.l_header
  $iconW = 32px
  $iconMargin = 4px
  position: fixed
  z-index: 1000
  top: 0
  width: 100%
  height: $navbar-height
  background: $color-card
+ background-image: linear-gradient(to top, #fff1eb 0%, #ace0f9 100%)
  box-shadow: $boxshadow-card
```

效果：

![](https://cdn.jsdelivr.net/gh/zyoushuo/Blog/images/meihua_3.png)

附上一个免费的CSS渐变背景样式网站👉[CSS背景渐变](http://color.oulu.me/)

#### 页面卡片阴影

在主页面中的文章、侧边栏添加一点阴影，并在鼠标悬停时出现阴影。
~~在themes\volantis\source\css\\_layout中`main.styl`文件，找到`.white-box`属性,在background下方添加代码：~~

主页文章：在\themes\volantis\source\css\\_layout中`main.styl`文件，找到`.post-wrapper`属性

```diff 文章地址 \themes\volantis\source\css\_layout\main.styl
  .post-wrapper
    column-break-inside: avoid
    break-inside: avoid-column
+   box-shadow: 0 1px 20px -6px rgba(0,0,0,0.5)
+   border-radius: 8px
+   transition: box-shadow .5s ease
+   &:hover
+     box-shadow:0px 1px 20px 1px rgba(0,0,0,0.5)
```

~~在themes\volantis\source\css\\_layout中`sidebar.styl`文件，找到`.widget`属性，在display下方添加上方同样的代码。~~

侧边栏：在themes\volantis\source\css\\_layout中`sidebar.styl`文件，找到`.widget`属性

```diff 文章地址 \themes\volantis\source\css\_layout\sidebar.styl
.widget
  z-index: 0
  background: $color-card
  margin-top: $gap
  border-radius: $border-card
  width: 100%
  display: none
+ box-shadow: 0 1px 20px -6px rgba(0,0,0,0.5)
+ transition: box-shadow .5s ease
+ &:hover
+   box-shadow:0px 1px 20px 1px rgba(0,0,0,0.5)
```

<span style="color:red;font-size:20px">注意格式！</span>

#### 页面特效

以下特效整理于网上分享的js代码，均在themes\volantis\layout中`layout.ejs`文件body里面直接引用即可。(不限制于Volantis主题)

{% noteblock warning yellow%}

特效选择添加一两个就好，如果多了会影响页面访问速度，很卡。

{% endnoteblock %}

1. 樱花
   {% folding yellow, 查看图片 %}

   ![](https://cdn.jsdelivr.net/gh/zyoushuo/Blog/images/meihua_4.gif)

   {% endfolding %}

   ```javascript
   <script src="https://cdn.jsdelivr.net/gh/zyoushuo/Blog/hexo/js/sakura.js"></script>
   ```

2. 鼠标滑动特效

   {% folding yellow, 查看图片 %}

   ![](https://cdn.jsdelivr.net/gh/zyoushuo/Blog/images/meihua_5.gif)

   {% endfolding %}

   ```javascript
   <script src="https://cdn.jsdelivr.net/gh/zyoushuo/Blog/hexo/js/mouse_slide.js"></script>
   ```

3. 鼠标点击特效

   {% folding yellow, 查看图片 %}

   ![](https://cdn.jsdelivr.net/gh/zyoushuo/Blog/images/meihua_6.gif)

   {% endfolding %}

   ```javascript
   <script src="https://cdn.jsdelivr.net/gh/zyoushuo/Blog/hexo/js/mouse_click.js"></script>
   ```

4. 鼠标点击爱心特效

   {% folding yellow, 查看图片 %}

   ![](https://cdn.jsdelivr.net/gh/zyoushuo/Blog/images/meihua_7.gif)

   {% endfolding %}

   ```javascript
   <script src="https://cdn.jsdelivr.net/gh/zyoushuo/Blog/hexo/js/clicklove.js"></script>
   ```

5. 鼠标点击社会主义价值观特效

    {% folding yellow, 查看图片 %}

   ![](https://cdn.jsdelivr.net/gh/zyoushuo/Blog/images/meihua_8.gif)

   ​      {% endfolding %}

   ```javascript
   <script src="https://cdn.jsdelivr.net/gh/zyoushuo/Blog/hexo/js/clicksocialist.js"></script>
   ```

#### 主页、正文文章标题居中

主页面的文章、文章正文、关于/友链/留言板等自定义页面的标题居中。

```diff 文章地址 themes\volantis\source\css\_layout\main.styl
  .post-wrapper
    margin-bottom: $gap
    .post
      div.meta
        margin-bottom: $gap
        .title
          font-size: $fontsize-h2
+         text-align: center
```


```diff 文章地址 themes\volantis\source\css\_layout\main.styl
      .title
        trans(.1s)
        margin: 0
+       text-align: center
        color: $color-text
```
#### 博客文章链接优化

原本hexo中文章的链接是`:year/:month/:day/:title/`格式，有时候可能还会有乱码，不好看，所以通过插件修改。

**安装插件**

```yaml
npm install hexo-abbrlink --save
```

{% noteblock warning red%}

此插件跟`hexo-asset-image`插件可能有冲突（可以使用本地图片的插件），若使用这个插件，`hexo-asset-image`插件会失效。

{% endnoteblock %}

**修改配置文件**

```diff 文章地址 blog\_config.yml
# permalink: :year/:month/:day/:title/
+ permalink: post/:abbrlink.html  //post可以修改
+ abbrlink:
+   alg: crc16
+   rep: hex
```
最后一键三连。然后链接就会变成`post/***.html`的格式。

#### 添加鼠标样式

下载两个文件（{% btn  regular, 点击下载, https://cdn.jsdelivr.net/gh/zyoushuo/Blog@master/File/default.cur, fas fa-download %}、{% btn  regular, 点击下载, https://cdn.jsdelivr.net/gh/zyoushuo/Blog@master/File/pointer.cur, fas fa-download %} ），文件放在`\blog\themes\volantis\source\img`中，然后在`index.styl`文件中引用。

```diff 文章地址 \themes\volantis\source\css\_base\index.styl
*
  box-sizing: border-box
  outline: none
  margin: 0
  padding: 0
+ cursor: url(/img/default.cur),auto
+:link
+ cursor: url(/img/pointer.cur),auto
```

#### 文章首字下沉

设置文章中第一个p标签首字样式，达到下沉的效果。

```diff 文章地址 \themes\volantis\source\css\_layout\article.styl
.article
  underline()
    &:hover
      text-decoration: underline
  .article-entry
+   >p
+     &:first-child::first-letter
+       float: left
+       margin-top: 14px
+       margin-right: 6px
+       color: #555
+       font-size: 42px
+       line-height: 28px
+       font-style: normal
+       font-weight: 400
+       +mobile(){
+         margin-top: 10px
+         margin-right: 4px
+         font-size: 26px
+         line-height: 20px
+       }
```

#### 文章末尾版权

修改默认的文章末尾版权区域样式。

修改样式：

```diff 文章地址 \themes\volantis\source\css\_layout\article.styl
  blockquote
+    background: #efefef     //修改背景颜色
+    border-left: $border-codeblock solid #575757   //修改左边框颜色
    border-radius: $border-codeblock
```

修改内容：

```diff 文章地址 \themes\config.yml
  copyright:
    class: copyright
    display: [desktop, mobile] # [desktop, mobile]
    blockquote: true
+    permalink: '🔗 本文链接：'
    content:
+     - '📚 本文由<a href="https://www.zyoushuo.cn/">阳光派Plus</a>创作，转载请注明出处'
+     - '🧾 博客内容遵循 署名-非商业性使用-相同方式共享 4.0 国际 (CC BY-NC-SA 4.0) 协议'
+     - permalink
```

图标来自于[📙 Emojipedia — 😃 ](https://emojipedia.org/)

### valine评论优化

#### Valine添加博主标签

此部分参考博主[HCLonely Blog](https://blog.hclonely.com/)的文章[Valine添加博主标签及评论微信、QQ通知](https://blog.hclonely.com/posts/409d3090/)。

Volantis主题添加需要修改一点语法格式。

{% radio checked green, 添加评论`QQ头像` %}
{% radio checked green, 添加`博主`，`小伙伴`，`访客`标签 %}
{% radio checked red, 添加`浏览器`和`操作系统`图标，需 `fontawesomeV5` 支持 %}
{% radio checked green, 增加 QQ 邮箱识别%}
{% radio checked red, `metaplaceholder` 可自定义 %}

##### 首先引入valine的js代码

```
https://cdn.jsdelivr.net/gh/HCLonely/Valine@latest/dist/Valine.min.js
```

本人使用的版本引入valine的js是在主题配置文件`_conflg.yml`的valine配置中，其他版本要是没有的话就在themes\volantis\layout\\_partial的`scripts.ejs`文件中找一下。

#####  添加valine配置参数

|      参数       |     类型     |          说明          |       默认       |                     实例                     |
| :-------------: | :----------: | :--------------------: | :--------------: | :------------------------------------------: |
|     tagMeta     |    Array     |    标签要显示的文字    | 博主,小伙伴,访客 |               博主,小伙伴,访客               |
|     master      | Array/String |  md5 加密后的博主邮箱  |        .         |       315be36db8ad7b3e3a7bb0839d6fa839       |
|     friends     |    Array     | md5 加密后的小伙伴邮箱 |        .         |       315be36db8ad7b3e3a7bb0839d6fa839       |
| metaPlaceholder |    Object    | meta placeholder 内容  |        .         | {“nick”:“昵称 / QQ 号”,“mail”:“邮箱 (必填)”} |

{% noteblock warning red %}

md5加密需要完整的邮箱地址，例如QQ邮箱就是123456789@qq.com；加密必须是32位小写。

{% endnoteblock %}

例如我的配置为

{% folding green, 查看代码 %}

```diff 文章地址 themes\volantis\_config.yml
comments:
  title: <i class='fas fa-comments'></i> 评论
  subtitle:
  service: valine # valine, minivaline, disqus, gitalk, livere
  valine:
    appId:  ***# your appId
    appKey: ***# your appKey
    js: https://cdn.jsdelivr.net/gh/HCLonely/Valine@latest/dist/Valine.min.js
    path: # All pages use the same path (share the same comments data)
    meta: nick,mail,link # valine comment header info
    requiredFields: ['nick','mail']
    enableQQ: true # Unstable avatar link
    placeholder: 快来评论吧~ # valine comment input placeholder(like: Please leave your footprints )
    avatar: robohash # gravatar style https://valine.js.org/avatar
    pageSize: 10 # comment list page size
    lang: zh-cn
    highlight: true
    visitor: true
    mathJax: false
+   metaPlaceholder:
+     - nick: 阳光派Plus
+     - mail: ***@qq.com
+   tagMeta: 博主,小伙伴,访客
+   master: 
+     - 487f87505f619bf9ea08f26bb34f8118
+   friends: 
+     - 011c2b8a03f490e9aeab5d41a8a0469a
+     - 8fe874d093278833df8b7172113eca32
+     ......
```

{% endfolding %}

附上一个MD5加密网站👉[MD5在线加密](https://md5jiami.51240.com/)

##### 添加valine渲染文件参数

在themes\volantis\layout\\_partial中`scripts.ejs`文件，找到enableValine，<span style="color:red">（3.0版本文件位置在\themes\volantis\layout\_third-party\comments\valine的scripts.ejs文件）</span>在valine.init中添加	

{% folding green, 查看代码 %}

```yaml
master: master,
friends: friends,
```

{% endfolding %}

```diff 文章地址 themes\volantis\layout\_partial\scripts.ejs
 valine.init({
    el: '#valine_container',
    meta: meta,
    <% if (page.valine && page.valine.path) { %>
      path: "<%= page.valine.path %>",
    <% } else if (theme.comments.valine.path) { %>
      path: "<%= theme.comments.valine.path %>",
    <% } %>
    appId: "<%= theme.comments.valine.appId %>",
    appKey: "<%= theme.comments.valine.appKey %>",
    placeholder: "<%= (page.valine && page.valine.placeholder) ? page.valine.placeholder : theme.comments.valine.placeholder %>",
    pageSize:'<%= theme.comments.valine.pageSize %>',
    avatar:'<%= theme.comments.valine.avatar %>',
    lang:'<%= theme.comments.valine.lang %>',
    visitor: '<%= theme.comments.valine.visitor %>',
    highlight: '<%= theme.comments.valine.highlight %>',
    mathJax: '<%= theme.comments.valine.mathJax %>',
    enableQQ: '<%= theme.comments.valine.enableQQ %>',
    requiredFields: requiredFields,
+   emojiCDN: 'https://cdn.jsdelivr.net/gh/zyoushuo/Blog/emoji/',
    emojiMaps: emojiMaps,
+	master: master,
+	friends: friends,
  })
```

然后在 `var valine = new Valine();`下方添加

{% folding green, 查看代码 %}

```javascript
  var friends = '<%= theme.comments.valine.friends %>'.split(',');
  var master = '<%= theme.comments.valine.master %>'.split(',');
```

{% endfolding %}

```diff 文章地址 themes\volantis\layout\_partial\scripts.ejs
  var valine = new Valine();
+ var friends = '<%= theme.comments.valine.friends %>'.split(',');
+ var master = '<%= theme.comments.valine.master %>'.split(',');
  function emoji(path, idx, ext) {
      return path + "/" + path + "-" + idx + "." + ext;
  }
```

#### 评论添加一言

![](https://cdn.jsdelivr.net/gh/zyoushuo/Blog/images/meihua_9.png)

在themes\volantis\layout\\_third-party中的`comments.ejs`文件，找到enableValine，<span style="color:red">（3.0版本文件位置在\themes\volantis\layout\_third-party\comments\valine的layout.ejs中）</span>在</ section>上方添加代码

{% folding green, 查看代码 %}

```javascript
 <!-- valine 添加一言 -->
<script src="https://sdk.jinrishici.com/v2/browser/jinrishici.js" charset="utf-8"></script>
<script type="text/javascript">
     jinrishici.load(function(result) {
     var jrsc_plac =  result.data.content + "\n「" + result.data.origin.title + "」" + result.data.origin.dynasty + " · " + result.data.origin.author
     document.getElementById("veditor").setAttribute("placeholder",jrsc_plac);
      });
 </script>
```

{% endfolding %}

```diff 文章地址 themes\volantis\layout\_third-party\comments.ejs
<% if (enableValine){ %>
  <section id="comments">
     <div id="valine_container" class="valine_thread">
       <i class="fas fa-cog fa-spin fa-fw fa-2x"></i>
     </div>
	 <!-- valine 添加一言 -->
+	<script src="https://sdk.jinrishici.com/v2/browser/jinrishici.js" charset="utf-8"></script>
+       <script type="text/javascript">
+              jinrishici.load(function(result) {
+            var jrsc_plac =  result.data.content + "\n「" + result.data.origin.title + "」" + result.data.origin.dynasty + " · " + result.data.origin.author
+             document.getElementById("veditor").setAttribute("placeholder",jrsc_plac);
+            });
+     </script>
   </section>
<% } %>
```

#### 添加评论背景

在themes\volantis\source\css\_third-party中的`valine.styl`文件，找到vedit，在span标签下方再添加.veditor标签属性。

{% folding green, 查看代码 %}

```yaml
 .veditor
   background: url(https://cdn.jsdelivr.net/gh/zyoushuo/Blog/images/valinebg.webp) 100% 100% no-repeat
```

{% endfolding %}

背景可替换。

```diff 文章地址 themes\volantis\source\css\_third-party\valine.styl
        .vedit
          .vctrl span
            padding: 0
            margin: 10px
          span
            fill: $color-p
            &.actived
              fill: $color-theme
+		  .veditor
+		    background: url(https://cdn.jsdelivr.net/gh/zyoushuo/Blog/images/valinebg.webp) 100% 100% no-repeat
```

#### 添加自定义表情

目前我使用的版本，在主题配置文件_config.yml的valine配置中，即使引用不同的js，valine的表情还是没有变化，需要修改渲染文件。

在themes\volantis\layout\\_partial中的`scripts.ejs`文件，找到enableValine，<span style="color:red">(3.0版本文件位置在\themes\volantis\layout\_third-party\comments\valine的scripts.ejs文件）</span>在var emojiMaps = {}中即可添加。例如我的配置：

{% folding green, 查看代码 %}

```javascript
  var emojiMaps = {
	"doge": "https://cdn.jsdelivr.net/gh/zyoushuo/Blog@master/emoji/bilibili/doge.png",
    "亲亲": "https://cdn.jsdelivr.net/gh/zyoushuo/Blog@master/emoji/bilibili/亲亲.png",
    "偷笑": "https://cdn.jsdelivr.net/gh/zyoushuo/Blog@master/emoji/bilibili/偷笑.png",  
	"再见": "https://cdn.jsdelivr.net/gh/zyoushuo/Blog@master/emoji/bilibili/再见.png",
    "冷漠": "https://cdn.jsdelivr.net/gh/zyoushuo/Blog@master/emoji/bilibili/冷漠.png",
    "发怒": "https://cdn.jsdelivr.net/gh/zyoushuo/Blog@master/emoji/bilibili/发怒.png",
    "发财": "https://cdn.jsdelivr.net/gh/zyoushuo/Blog@master/emoji/bilibili/发财.png",
    "可爱": "https://cdn.jsdelivr.net/gh/zyoushuo/Blog@master/emoji/bilibili/可爱.png",
    .....
    }
```

{% endfolding %}

这种方法适合中文命名表情包，如果不在乎表情包名字的话可以按照作者的语法格式：

```javascript
  for (var i = 1; i <= 54; i++) {
    emojiMaps['tieba-' + i] = emoji('tieba', i, 'png');
  }
  for (var i = 1; i <= 101; i++) {
    emojiMaps['qq-' + i] = emoji('qq', i, 'gif');
  }
  for (var i = 1; i <= 116; i++) {
    emojiMaps['aru-' + i] = emoji('aru', i, 'gif');
  }
  for (var i = 1; i <= 125; i++) {
    emojiMaps['twemoji-' + i] = emoji('twemoji', i, 'png');
  }
  for (var i = 1; i <= 4; i++) {
    emojiMaps['weibo-' + i] = emoji('weibo', i, 'png');
  }
```

按照语法格式对表情包进行命名，比较方便。例如 tieba-1，tieba-2.....

我的配置为：

{% folding green, 查看代码 %}

```javascript
<% if (enableValine){ %>
  <% if (theme.comments.valine.js) { %>
    <%- js(theme.comments.valine.js) %>
  <% } else { %>
    <%- js(['js/valine.js']) %>
  <% } %>
  <script>
  var GUEST_INFO = ['nick','mail','link'];
  var meta = '<%= theme.comments.valine.meta %>'.split(',').filter(function(item){
    return GUEST_INFO.indexOf(item) > -1
  });
  var REQUIRED_FIELDS = ['nick','mail','link'];
  var requiredFields = '<%= theme.comments.valine.requiredFields %>'.split(',').filter(function(item){
    return REQUIRED_FIELDS.indexOf(item) > -1
  });
  var valine = new Valine();
  function emoji(path, idx, ext) {
      return path + "/" + path + "-" + idx + "." + ext;
  }
  var friends = '<%= theme.comments.valine.friends %>'.split(',');
  var master = '<%= theme.comments.valine.master %>'.split(',');
  var emojiMaps = {
	"doge": "https://cdn.jsdelivr.net/gh/zyoushuo/Blog@master/emoji/bilibili/doge.png",
    "亲亲": "https://cdn.jsdelivr.net/gh/zyoushuo/Blog@master/emoji/bilibili/亲亲.png",
    "偷笑": "https://cdn.jsdelivr.net/gh/zyoushuo/Blog@master/emoji/bilibili/偷笑.png",  
    "冷漠": "https://cdn.jsdelivr.net/gh/zyoushuo/Blog@master/emoji/bilibili/冷漠.png",
    "发怒": "https://cdn.jsdelivr.net/gh/zyoushuo/Blog@master/emoji/bilibili/发怒.png",
             ....
  };
  for (var i = 1; i <= 23; i++) {
    emojiMaps['weibo-' + i] = emoji('weibo', i, 'png');
  }
  for (var i = 1; i <= 23; i++) {
    emojiMaps['tieba-' + i] = emoji('tieba', i, 'png');
  }
  for (var i = 1; i <= 23; i++) {
    emojiMaps['bqb-' + i] = emoji('bqb', i, 'jpg');
  }
  for (var i = 1; i <= 23; i++) {
    emojiMaps['ya-' + i] = emoji('ya', i, 'jpg');
  }
  valine.init({
    el: '#valine_container',
    meta: meta,
    <% if (page.valine && page.valine.path) { %>
      path: "<%= page.valine.path %>",
    <% } else if (theme.comments.valine.path) { %>
      path: "<%= theme.comments.valine.path %>",
    <% } %>
    appId: "<%= theme.comments.valine.appId %>",
    appKey: "<%= theme.comments.valine.appKey %>",
    placeholder: "<%= (page.valine && page.valine.placeholder) ? page.valine.placeholder : theme.comments.valine.placeholder %>",
    pageSize:'<%= theme.comments.valine.pageSize %>',
    avatar:'<%= theme.comments.valine.avatar %>',
    lang:'<%= theme.comments.valine.lang %>',
    visitor: '<%= theme.comments.valine.visitor %>',
    highlight: '<%= theme.comments.valine.highlight %>',
    mathJax: '<%= theme.comments.valine.mathJax %>',
    enableQQ: '<%= theme.comments.valine.enableQQ %>',
    requiredFields: requiredFields,
    emojiCDN: 'https://cdn.jsdelivr.net/gh/zyoushuo/Blog/emoji/',
    emojiMaps: emojiMaps,
	master: master,
	friends: friends,
  })
  </script>
<% } %>
```

{% endfolding %}

{% noteblock warning yellow%}

此方法要在emojiCDN处添加地址。

{% endnoteblock %}

#### 表情区域样式

修改表情大小、背景颜色。

```diff 文章地址 themes\volantis\source\css\_third-party\valine.styl
        .vemojis,.vpreview
+         background: #fff  //背景区域颜色
          border-radius: $border-codeblock
          padding: $gap * 0.5
+         border: 1px solid #f6f6f6 //边框
          scrollbar()
          .vemoji
+           max-height: 40px   //表情大小
+           max-width: 100px
```

#### 评论区卡片式背景

具体样式就是给每一条评论加个背景边框。

```diff 文章地址 themes\volantis\source\css\_third-party\valine.styl
      .vcards
+       .vcard
+         box-shadow: 0 0 4px 1px rgba(0, 0, 0, .12)
+         padding: 15px 20px 0 20px
+         margin-bottom: 10px
+         border-radius: 8px
        .vquote
          border-left: none
        .vh
          border-bottom: 1px dashed alpha($color-text, .1)
+         .vcard
+           box-shadow: none
```

🍭<span style="font-size:18px;font-weight:bold">最后</span>

虽然是对Volantis主题的美化，但是其他主题同样适用。学会使用F12，找准位置，然后找到对应的文件，按照语法格式修改即可。多去参考参考其他博主的网站。

{% radio checked cyan, 目前对Volantis主题就修改了怎么多，若再有修改，日后添加。 %}

<p style="color:red;font-size:25px;font-family:SimSun">注意事项</p>

{% radio red, 如果修改了样式发现没有变化，请使用`hexo cl`清理文件缓存、`Ctrl+F5`强制刷新、`Ctrl+shift+delete`清理浏览器缓存。（尤其是最后一个） %}

{% radio red, 有时候在修改`styl文件`会出现错误，比如这样： %}

{% folding yellow, 查看图片 %}

<img src="https://cdn.jsdelivr.net/gh/zyoushuo/Blog/images/meihua_10.png" style="zoom:70%;" />

{% endfolding %}

可以发现是格式不正确，请删除多余的空格。

参考文章：

[Valine-1.4.4新版本尝鲜+个性制定（表情包、qq头像、UI样式）](https://blog.csdn.net/cungudafa/article/details/105548858)

[Valine添加博主标签及评论微信、QQ通知](https://blog.hclonely.com/posts/409d3090/)

[halo 博客深度定制与美化教程](https://bestzuo.cn/posts/halo-beauty.html)