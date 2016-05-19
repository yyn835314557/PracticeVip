#Coding Style of the HTML,JS and CSS/SASS (编码规范)
*this document aims at improving collaboration,code quality and enabling supporting infrastructure.*
*此文档旨在增强团队开发写作，提高代码质量以及打造开发基石的编码风格规范*
***
## 1. General style rules(一般规范)
**1.1. file and resource names: follow the same naming conventions(文件及资源的命名: 遵循相同的命名规则)**

* minus(-) sign as the separating parts in a file name(使用`- `号来分隔文件名称)
* lower case letter sign as the file name where possible (尽可能的使用小写字符命名)
* special sign as the file name in special cases(特殊字符的使用场景)
    *  versions in the post-fix as outlined in the post-fix note(作为版本号时候)
    *  flag file for a special purpose(underscore for compass to ignore a certain file for direct css compilation)(`compass[1]`中的下划线就是用来标记跳过直接编译的文件用的)
* post- or pre-fixes or extensions (i.e. .min.js, .min.css) or reeving which includes some pre-fixes (i.e. file hashes like 3fa89b.main.min.css). In those cases we recommend to use dot's to separate the clear purpose of this additional meta-data in a filename.(需要对文件增加前后缀或特定的扩展名（比如 `.min.js`, `.min.css`），抑或一串前缀（比如 `3fa89b.main.min.css`）,建议使用点分隔符来区分这些在文件名中带有清晰意义的元数据)

 **Recommended**
 ```
 my-script.js
 my-camel-case-name.css
 i-love-underscores.html
 thousand-and-one-scripts.js
 my-file.min.css
 ```
 **Not recommended**
 ```
 MyScript.js
 myCamelCaseName.css
 i_love_underscores.html
 1001-scripts.js
 my-file-min.css
 ```

**1.2. Protocol(协议)**

* Omit the protocol portion(`http:`,`https:`) from embedded resources unless the respective files are not available over both protocols.(不要指定具体的协议部分(`http,https`除非这两个协议都不用))
* makes URL relative,prevents mixed content issues and results in minor file size savings(是的URL为相对路径)
 
 **Recommended**
 ```
 <script src="//cdn.com/foundation.min.js"></script>
 .example {
   background: url(http://static.example.com/images/bg.jpg);
 }
 ```
 **Not recommended**
 ```
 <script src="http://cdn.com/foundation.min.js"></script>
 .example {
   background: url(http://static.example.com/images/bg.jpg);
 }
 ```

**1.3. Text Coding(文本编辑)**

* Indent by 2 spaces at a time(tab缩进设置为两个空格).
* semicolon(;) sign added to the end of the line.(每一行一分号结尾)
* Comments(注释):
    -  don't comment what's coded(不要写你的代码都干了些什么)
    -  comment why it was coded this way and comment the thinking behind.(写你的代码为什么要这么写)
    -  include links in your comments to open issues, specifications etc.(所思考问题或是解决方案的链接地址)
* use [JSDoc](http://usejsdoc.org/) or [YUIDoc](http://yui.github.io/yuidoc/) for JS annotation(JS注释插件)
* code checking: [JSLint](http://www.jslint.com/) or [JSHint](http://jshint.com/)（JS代码检查插件）
 ```
    <ul>
      <li>Fantastic</li>
      <li>Great</li>
      <li>
        <a href="#">Test</a>
      </li>
    </ul>

    @media screen and (min-width: 1100px) {
      body {
        font-size: 100%;
      }
    }

    (function(){
      var x = 10;

      function y(a, b) {
        return {
          result: (a + b) * x
        }

      }
    }());
 ```

## 2. HTML style ruleste(HTML规范)
**2.1. Document type(文档类型)**

* HTML5 (HTML syntax) is preferred for all HTML documents: `<!DOCTYPE html>`.(使用H5文档类型声明)
* Use HTML as text/html (not to use XHTML as application/xhtml + xml)(避免使用XHTML以及它的属性)
* Do not close void elements, write `<br>`,not `<br />`(最好不要将无内容的元素标签闭合)

**2.2. HTML validity(HTML校验)**

* Use valid HTML codess unless that is not possible due to otherwise unattainable performance goals regarding file size.(建议使用能通过标准规范验证的 HTML 代码，)
* Use tools such as the W3C HTML validator to test.(使用诸如 W3C HTML validator 这样的工具来进行检测。)

 **Recommended**
 ```
 <!DOCTYPE html>
 <meta charset="utf-8">
 <title>Test</title>
 <article>This is only a test.</article>
 ```
 **Not recommended**
 ```
 <title>Test</title>
 <article>This is only a test.
 ```

**2.2. Optional tags(省略可选标签)**

* The HTML5 specification defines what tags can be omitted in the HTML markup. For readability purpose the raw source file should NOT omit optional tags. Omitting optional tags can lead to readability and scannability issues, and therefore should not be used in the raw source files.
* 虽然HTML标签可以省略，但是从可读性来说，开发源文件最好不要这样做，省略标签会导致一些问题
* Omitting tags can lead to significant page size reductions specially on large scale sites. For this purpose you should consider an HTML minification post processing of your raw files for distribution purpose.
* 我们可以在开发后期对页面进行压缩处理，此环节可省略一些可选标签，使得页面大小减少

**2.3. Script loading(脚本加载)**

For performance reasons it's important to load scripts asynchronously. A script loaded in the `<head>` like this
`<script src="main.js"></script>` will block the whole DOM parsing until the script has fully loaded and executed. This
will delay the page to be displayed until the script has fully loaded. With larger scripts this can have a big impact
on user experience.

Asynchronous script loading helps to minimize this performance impact. If browser support is only concerned about IE10+
the HTML5 async attribute on scripts should be used. This will prevent DOM parser blocking and you can even place your
script element into the `<head>` element.

If you need to support older browsers it's common practice to use script loaders that will make use of dynamic script
injection. You should consider [yepnope](http://yepnopejs.com/) or [labjs](http://labjs.com/). The problem with injected
scripts though is that [they will not start loading until CSS Object Model is ready](https://www.igvita.com/2014/05/20/script-injected-async-scripts-considered-harmful/)
(shortly after the CSS from the head is loaded). This can also load to delay of your behavior added by these javascript
which can again affect the user experience.

As a result of the above described behaviors you should always consider the following best practice if you need to
support old browsers (IE9-).

Add your script element just before the body close tag and add them with a async attribute. This will not load the
scripts asynchronously on old browsers but they will only block the DOM parser just before the body close which is not
affecting the user experience too much. On modern browsers this will delay the script load until the DOM parser
discovers the script element at the end of the body, but they will then asynchronously load the script and don't wait
for CSSOM to complete before loading (execution will still happen after CSSOM).

出于性能考虑，脚本异步加载很关键。一段脚本放置在 `<head>`内，比如 `<script src="main.js"></script>`，其加载会一直阻塞 DOM 解析，直至它完全地加载和执行完毕。这会造成页面显示的延迟。特别是一些重量级的脚本，对用户体验来说那真是一个巨大的影响。

异步加载脚本可缓解这种性能影响。如果只需兼容 IE10+，可将 HTML5 的 async 属性加至脚本中，它可防止阻塞 DOM 的解析，甚至你可以将脚本引用写在 `<head>` 里也没有影响。

如需兼容老旧的浏览器，实践表明可使用用来动态注入脚本的脚本加载器。你可以考虑 yepnope 或 labjs。注入脚本的一个问题是：一直要等到 CSS 对象文档已就绪，它们才开始加载（短暂地在 CSS 加载完毕之后），这就对需要及时触发的 JS 造成了一定的延迟，这多多少少也影响了用户体验吧。

终上所述，兼容老旧浏览器(IE9-)时，应该遵循以下最佳实践。

脚本引用写在 body 结束标签之前，并带上 `async` 属性。这虽然在老旧浏览器中不会异步加载脚本，但它只阻塞了 body 结束标签之前的 DOM 解析，这就大大降低了其阻塞影响。而在现代浏览器中，脚本将在 DOM 解析器发现 body 尾部的 script 标签才进行加载，此时加载属于异步加载，不会阻塞 CSSOM（但其执行仍发生在 CSSOM 之后）。

**Recommended for modern and old browsers(所有浏览器中，推荐)**
```
<html>
  <head>
    <link rel="stylesheet" href="main.css">
  </head>
  <body>
    <!-- body goes here -->

    <script src="main.js" async></script>
  </body>
</html>
```

**Recommended for only modern browsers(只在现代浏览器中，推荐)**
```
<html>
  <head>
    <link rel="stylesheet" href="main.css">
    <script src="main.js" async></script>
  </head>
  <body>
    <!-- body goes here -->
  </body>
</html>
```

***

**2.4. Semantics(语义化)**

Use elements (sometimes incorrectly called “tags”) for what they have been created for. For example, use heading
elements for headings, p elements for paragraphs, a elements for anchors, etc.

Using HTML according to its purpose is important for accessibility, reuse, and code efficiency reasons.

The following bad / good example should outline some of the major important semantic HTML cases:

根据元素（有时被错误地称作“标签”）其被创造出来时的初始意义来使用它。打个比方，用 heading 元素来定义头部标题，p 元素来定义文字段落，用 a 元素来定义链接锚点，等等。

有根据有目的地使用 HTML 元素，对于可访问性、代码重用、代码效率来说意义重大。

以下示例列出了一些的语义化 HTML 主要情况：

**Not recommended**
```
<b>My page title</b>
<div class="top-navigation">
  <div class="nav-item"><a href="#home">Home</a></div>
  <div class="nav-item"><a href="#news">News</a></div>
  <div class="nav-item"><a href="#about">About</a></div>
</div>

<div class="news-page">
  <div class="page-section news">
    <div class="title">All news articles</div>
    <div class="news-article">
      <h2>Bad article</h2>
      <div class="intro">Introduction sub-title</div>
      <div class="content">This is a very bad example for HTML semantics</div>
      <div class="article-side-notes">I think I'm more on the side and should not receive the main credits</div>
      <div class="article-foot-notes">
        This article was created by David <div class="time">2014-01-01 00:00</div>
      </div>
    </div>

    <div class="section-footer">
      Related sections: Events, Public holidays
    </div>
  </div>
</div>

<div class="page-footer">
  Copyright 2014
</div>
```

**Recommended**
```
<!-- The page header should go into a header element -->
<header>
  <!-- As this title belongs to the page structure it's a heading and h1 should be used -->
  <h1>My page title</h1>
</header>

<!-- All navigation should go into a nav element -->
<nav class="top-navigation">
  <!-- A listing of elements should always go to UL (OL for ordered listings) -->
  <ul>
    <li class="nav-item"><a href="#home">Home</a></li>
    <li class="nav-item"><a href="#news">News</a></li>
    <li class="nav-item"><a href="#about">About</a></li>
  </ul>
</nav>

<!-- The main part of the page should go into a main element (also use role="main" for accessibility) -->
<main class="news-page" role="main">
  <!-- A section of a page should go into a section element. Divide a page into sections with semantic elements. -->
  <section class="page-section news">
    <!-- A section header should go into a section element -->
    <header>
      <!-- As a page section belongs to the page structure heading elements should be used (in this case h2) -->
      <h2 class="title">All news articles</h2>
    </header>

    <!-- If a section / module can be seen as an article (news article, blog entry, products teaser, any other
     re-usable module / section that can occur multiple times on a page) a article element should be used -->
    <article class="news-article">
      <!-- An article can contain a header that contains the summary / introduction information of the article -->
      <header>
        <!-- As a article title does not belong to the overall page structure there should not be any heading tag! -->
        <div class="article-title">Good article</div>
        <!-- Small can optionally be used to reduce importance -->
        <small class="intro">Introduction sub-title</small>
      </header>

      <!-- For the main content in a section or article there is no semantic element -->
      <div class="content">
        <p>This is a good example for HTML semantics</p>
      </div>
      <!-- For content that is represented as side note or less important information in a given context use aside -->
      <aside class="article-side-notes">
        <p>I think I'm more on the side and should not receive the main credits</p>
      </aside>
      <!-- Articles can also contain footers. If you have footnotes for an article place them into a footer element -->
      <footer class="article-foot-notes">
        <!-- The time element can be used to annotate a timestamp. Use the datetime attribute to specify ISO time
         while the actual text in the time element can also be more human readable / relative -->
        <p>This article was created by David <time datetime="2014-01-01 00:00" class="time">1 month ago</time></p>
      </footer>
    </article>

    <!-- In a section, footnotes or similar information can also go into a footer element -->
    <footer class="section-footer">
      <p>Related sections: Events, Public holidays</p>
    </footer>
  </section>
</main>

<!-- Your page footer should go into a global footer element -->
<footer class="page-footer">
  Copyright 2014
</footer>

```

***

**2.4. Multimedia fallback(多媒体回溯)**

For multimedia, such as images, videos, animated objects via canvas, make sure to offer alternative access. For images
that means use of meaningful alternative text (alt) and for video and audio transcripts and captions, if available.

Providing alternative contents is important for accessibility reasons: A blind user has few cues to tell what an
image is about without @alt, and other users may have no way of understanding what video or audio contents are about
either.

(For images whose alt attributes would introduce redundancy, and for images whose purpose is purely decorative which
you cannot immediately use CSS for, use no alternative text, as in alt="".)

对页面上的媒体而言，像图片、视频、canvas 动画等，要确保其有可替代的接入接口。图片文件我们可采用有意义的备选文本（alt），视频和音频文件我们可以为其加上说明文字或字幕。

提供可替代内容对可用性来说十分重要。试想，一位盲人用户如何能知晓一张图片是什么，要是没有 @alt 的话。

（图片的 alt 属性是可不填写内容的，纯装饰性的图片就可用这么做：alt=""）。

**Not recommended**
```
<img src="luke-skywalker.jpg">
```

**Recommended**
```
<img src="luke-skywalker.jpg" alt="Luke skywalker riding an alien horse">
```

When writing alt tags always try to describe the image as if you'd need to describe what's on the image to somebody
over the phone or who can't see the real picture.
尽量用 alt 标签去描述图片，设想你需要对于那些只能通过语音或者看不见图片的用户表达图片到底是什么。

**Not recommended**
```
<img src="huge-spaceship-approaching-earth.jpg" alt="Header image">
```

**Recommended**
```
<img src="huge-spaceship-approaching-earth.jpg" alt="A huge spaceship that is approaching the earth">
```

***

**2.4. Separation of Concerns(关注点分离)**

It's very important that you understand the different concerns in web and that you know how to and why to separate them.
In the web we have information (html markup), appearance (css) and behavior (Javascript) and we need to separate them as
far as possible in order to keep a maintainable and clean code.

Strictly keep structure (markup), presentation (styling), and behavior (scripting) apart, and try to keep the
interaction between the three to an absolute minimum.

That is, make sure documents and templates contain only HTML and HTML that is solely serving structural purposes.
Move everything presentational into style sheets, and everything behavioral into scripts.

In addition, keep the contact area as small as possible by linking as few style sheets and scripts as possible from
documents and templates.

Clean separation of concerns implies the following things:

1.  Don't use more than one or two stylesheets (i.e. main.css, vendor.css)
1.  Don't use more than one or two scripts (use concatination)
1.  Don't use inline styles (`<style>.no-good {}</style>`)
1.  Don't use element style attributes (`<hr style="border-top: 5px solid black">`)
1.  Don't use inline scripts (`<script>alert('no good')</script>`)
1.  Don't use presentational elements (i.e. `<b>`, `<u>`, `<center>`, `<font>`, `<b>`
1.  Don't use presentational class names (i.e. red, left, center)

理解 web 中如何和为何区分不同的关注点，这很重要。这里的关注点主要指的是：信息（HTML 结构）、外观（CSS）和行为（JavaScript）。为了使它们成为可维护的干净整洁的代码，我们要尽可能的将它们分离开来。

严格地保证结构、表现、行为三者分离，并尽量使三者之间没有太多的交互和联系。

就是说，尽量在文档和模板中只包含结构性的 HTML；而将所有表现代码，移入样式表中；将所有动作行为，移入脚本之中。

在此之外，为使得它们之间的联系尽可能的小，在文档和模板中也尽量少地引入样式和脚本文件。

清晰的分层意味着：

* 不使用超过一到两张样式表（i.e. main.css, vendor.css）
* 不使用超过一到两个脚本（学会用合并脚本）
* 不使用行内样式（<style>.no-good {}</style>）
* 不在元素上使用 style 属性（`<hr style="border-top: 5px solid black">`）
* 不使用行内脚本（`<script>alert('no good')</script>`）
* 不使用表象元素（`i.e. <b>, <u>, <center>, <font>, <b>`）
* 不使用表象 class 名（`i.e. red, left, center`）

**Not recommended**
```
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="base.css">
  <link rel="stylesheet" href="grid.css">
  <link rel="stylesheet" href="type.css">
  <link rel="stylesheet" href="modules/teaser.css">
</head>
<body>
  <h1 style="font-size: 3rem"></h1>
  <b>I'm a subtitle and I'm bold!</b>
  <center>Dare you center me!</center>
  <script>
    alert('Just dont...');
  </script>
  <div class="red">I'm important!</div>
</body>
</html>
```

**Recommended**
```
<!DOCTYPE html>
<html>
<head>
  <!-- Concatinate your style sheets into a single one -->
  <link rel="stylesheet" href="main.css">
</head>
<body>
  <!-- Don't use style attributes but assign sensible classes and apply styles in the stylesheet -->
  <h1 class="title"></h1>
  <!-- Don't use presentational elements and assign sensible classes -->
  <div class="sub-title">I'm a subtitle and I'm bold!</div>
  <!-- Maybe your comments get centered in your presentation but that decision is up to the stylesheet -->
  <span class="comment">Dare you center me!</span>
  <!-- You wanted to make it red because it's important so then also name the class important and decide in the stylesheet
   what you want to do with it -->
  <div class="important">I'm important!</div>

  <!-- Put all your scripts into files and concatinate them into a single one -->
  <script async src="main.js"></script>
</body>
</html>
```

***

**2.5. HTML is content only(HTML 内容至上)**

Don't pollute your HTML markup with non-content information. There is a tendency to solve design problems at
the information's cost. The HTML markup should only contain content relevant information and design problems should
never be solved within the markup.

The only purpose of HTML markup is to represent content information.

- Don't introduce a specific HTML structure just to solve some visual design problems
- Don't use `<img>` elements for visual design elements

The following examples show two common things that are done wrong when it comes to solving design problems.

不要让非内容信息污染了你的 HTML。现在貌似有一种倾向：通过 HTML 来解决设计问题，这是显然是不对的。HTML 就应该只关注内容。

HTML 标签的目的，就是为了不断地展示内容信息。

 - 不要引入一些特定的 HTML 结构来解决一些视觉设计问题
 - 不要将 img 元素当做专门用来做视觉设计的元素
 
以下例子展示了误将 HTML 用来解决设计问题的这两种情况：

**Not recommended**
```
<!-- We should not introduce an additional element just to solve a design problem  -->
<span class="text-box">
  <span class="square"></span>
  See the square next to me?
</span>

```
```
.text-box > .square {
  display: inline-block;
  width: 1rem;
  height: 1rem;
  background-color: red;
}
```


**Recommended**
```
<!-- That's clean markup! -->
<span class="text-box">
  See the square next to me?
</span>

```
```
// We use a :before pseudo element to solve the design problem of placing a colored square in front of the text content
.text-box:before {
  content: "";
  display: inline-block;
  width: 1rem;
  height: 1rem;
  background-color: red;
}
```

The only reason for images and svg graphics to be included in the markup is because they represent content relevant
information.

图片和 SVG 图形能被引入到 HTML 中的唯一理由是它们呈现出了与内容相关的一些信息。

**Not recommended**
```
<!-- Content images should never be used for design elements!  -->
<span class="text-box">
  <img src="square.svg" alt="Square" />
  See the square next to me?
</span>
```

**Recommended**
```
<!-- That's clean markup! -->
<span class="text-box">
  See the square next to me?
</span>

```
```
// We use a :before pseudo element with a background image to solve the problem
.text-box:before {
  content: "";
  display: inline-block;
  width: 1rem;
  height: 1rem;
  background: url(square.svg) no-repeat;
  background-size: 100%;
}
```

***

**2.6. Type attributes(Type 属性)**

Omit type attributes for style sheets and scripts. Do not use type attributes for style sheets (unless not using CSS)
and scripts (unless not using JavaScript). Specifying type attributes in these contexts is not necessary as
HTML5 implies text/css and text/javascript as defaults. This can be safely done even for older browsers.

省略样式表与脚本上的 type 属性。鉴于 HTML5 中以上两者默认的 type 值就是 text/css 和 text/javascript，所以 type 属性一般是可以忽略掉的。甚至在老旧版本的浏览器中这么做也是安全可靠的。

**Not recommended**
```
<link rel="stylesheet" href="main.css" type="text/css">
<script src="main.js" type="text/javascript"></script>
```

**Recommended**
```
<link rel="stylesheet" href="main.css">
<script src="main.js"></script>
```

***

**2.7. General Accessibility(可用性)**

If you use proper HTML5 semantics a lot of accessibility issues are already solved. ARIA is using some default roles
for most of the semantic elements which, if used correctly, solves a lot of the issues already. If you use `nav`,
`aside`, `main`, `footer` etc. ARIA will use some related default roles. For more details you can reference the
[ARIA specification](http://rawgit.com/w3c/aria-in-html/master/index.html#recommendations-table) recommendation table
which contains the defaults for the HTML semantic elements.

Additional roles can be used to give more accessibility context (i.e. `role="tab"`).

如果 HTML5 语义化标签使用得当，许多可用性问题已经引刃而解。[ARIA specification](http://rawgit.com/w3c/aria-in-html/master/index.html#recommendations-table)规则在一些语义化的元素上可为其添上默认的可用性角色属性，使用得当的话已使网站的可用性大部分成立。假如你使用 nav, aside, main, footer 等元素，ARIA 规则会在其上应用一些关联的默认值。
更多细节可参考 ARIA specification

另外一些角色属性则能够用来呈现更多可用性情景（i.e. `role="tab"`）。

***

**2.8. Tab Index for Accessibility(Tab Index 在可用性上的运用)**

Check your document for tab order and assign tabindex values in order to change the tab flow based on priority. You
can disable the tab index of an element by setting `tabindex="-1"` on any element.

If you add functionality to a element that is not focusable by default, you should always add a `tabindex` in order to
make the element focusable. This will also enable the CSS pseudo selector `:focus`. Choose an appropriate index value
for `tabindex` or use `tabindex="0"` to group elements into one tab order level and enforce ordering in natural reading
order.

检查文档中的 tab 切换顺序并传值给元素上的 tabindex，这可以依据元素的重要性来重新排列其 tab 切换顺序。你可以设置 `tabindex="-1"` 在任何元素上来禁用其 tab 切换。

当你在一个默认不可聚焦的元素上增加了功能，你应该总是为其加上 tabindex 属性使其变为可聚焦状态，而且这也会激活其 CSS 的伪类 `:focus  `。选择合适的 `tabindex` 值，或是直接使用 `tabindex="0"` 将元素们组织成同一 `tab` 顺序水平，并强制干预其自然阅读顺序。

***

**2.9. Microdata for SEO and Accessibility(微格式在 SEO 和可用性上的运用)**

If the SEO relevance and / or accessibility environment is given then you should consider to use microdata where
possible. Microdata is a way to annotate your data in your markup that follows some specific semantics.

Google, Microsoft and Yahoo! have more or less agreed on how to use this additional data and using it correctly has
great influence on your searches.

You can visit [schema.org](http://schema.org/) for more details.

Simple example of a movie on a web page:

如果 SEO 和可用性环境条件允许的话，建议考虑采用微格式。微格式是通过在元素标签上申明一系列特定数据来达成特定语义的方法。

谷歌、微软和雅虎对如何使用这些额外的数据一定程度上的达成一致，如果正确的使用，这将给搜索引擎优化带来巨大的好处。

你可以访问 [schema.org](http://schema.org/)  获得更多内容细节。

看一个电影网站的简单例子：

**Without microdata(不带微格式)**
```
<div>
 <h1>Avatar</h1>
 <span>Director: James Cameron (born August 16, 1954)</span>
 <span>Science fiction</span>
 <a href="../movies/avatar-theatrical-trailer.html">Trailer</a>
</div>
```

**With microdata(带微格式)**
```
<div itemscope itemtype ="http://schema.org/Movie">
  <h1 itemprop="name">Avatar</h1>
  <div itemprop="director" itemscope itemtype="http://schema.org/Person">
  Director: <span itemprop="name">James Cameron</span> (born <span itemprop="birthDate">August 16, 1954)</span>
  </div>
  <span itemprop="genre">Science fiction</span>
  <a href="../movies/avatar-theatrical-trailer.html" itemprop="trailer">Trailer</a>
</div>
```

***

**2.10. IDs for anchors(ID 和锚点)**

It's generally a good practice to give all headings on a page a ID. With these ID's on headings you can use the
browsers default behavior and include the ID names as hash tags in the URL. By default this causes the browser to scroll
to the position this element.

If you'd enter the URL `http://your-site.com/about#best-practices` in your browser then the browser would scroll down
so that the H3 below would be scrolled into the view.

通常一个比较好的做法是将页面内所有的头部标题元素都加上 ID. 这样做，页面 URL 的 hash 中带上对应的 ID 名称，即形成描点，方便跳转至对应元素所处位置。

打个比方，当你在浏览器中输入 URL `http://your-site.com/about#best-practices`，浏览器将定位至以下 H3 上。

```
<h3 id="best-practices">Best practices</h3>
```

***

**2.11. General formatting(格式化规则)**

Use a new line for every block, list, or table element, and indent every such child element.
Independent of the styling of an element (as CSS allows elements to assume a different role per display property),
put every block, list, or table element on a new line.

Also, indent them if they are child elements of a block, list, or table element.

(If you run into issues around whitespace between list items it’s acceptable to put all li elements in one line.
A linter is encouraged to throw a warning instead of an error.)

在每一个块状元素，列表元素和表格元素后，加上一新空白行，并对其子孙元素进行缩进。内联元素写在一行内，块状元素还有列表和表格要另起一行。

（如果由于换行的空格引发了不可预计的问题，那将所有元素并入一行也是可以接受的，格式警告总好过错误警告）。

**Recommended**
```
<blockquote>
  <p><em>Space</em>, the final frontier.</p>
</blockquote>

<ul>
  <li>Moe</li>
  <li>Larry</li>
  <li>Curly</li>
</ul>

<table>
  <thead>
    <tr>
      <th scope="col">Income</th>
      <th scope="col">Taxes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>$ 5.00</td>
      <td>$ 4.50</td>
    </tr>
  </tbody>
</table>
```

***
**2.12. HTML quotation marks(HTML 引号)**

When quoting attributes values, use double quotation marks. Use double ("") rather than single quotation marks ('')
around attribute values.

使用双引号(“”) 而不是单引号(”) 。

**Not recommended**
```
<div class='news-article'></div>
```

**Recommended**
```
<div class="news-article"></div>
```

***

## Javascript style guide(JavaScript 规范)

***

### Global namespace pollution and IIFE(全局命名空间污染与 IIFE)

Always wrap your code into a IIFE (Immediately-Invoked Function Expression) in order to create an isolated closure
scope. This prevents you from polluting the global namespace.

IIFE can also secure your code from modifications that happened in the global namespace (i.e. 3rd party libraries,
window reference, overridden undefined keyword etc.)

总是将代码包裹成一个 IIFE(Immediately-Invoked Function Expression)，用以创建独立隔绝的定义域。这一举措可防止全局命名空间被污染。

IIFE 还可确保你的代码不会轻易被其它全局命名空间里的代码所修改（i.e. 第三方库，window 引用，被覆盖的未定义的关键字等等）。

**Not recommended**
```
var x = 10,
    y = 100;

// Declaring variables in the global scope is resulting in global scope pollution. All variables declared like this
// will be stored in the window object. This is very unclean and needs to be avoided.
console.log(window.x + ' ' + window.y);
```

**Recommended**
```
// We declare a IIFE and pass parameters into the function that we will use from the global space
(function(log, w, undefined){
  'use strict';

  var x = 10,
      y = 100;

  // Will output 'true true'
  log((w.x === undefined) + ' ' + (w.y === undefined));

}(window.console.log, window));
```

***

### IIFE (Immediately-Executed Function Expression)IIFE（立即执行的函数表达式）

Use IIFE whenever you want to create a new closure scope. This can be used to create privacy and to keep memory clean.

Every javascript file should start with an IIFE.

The IIFE should be written so you're keeping the execution brackets inside of the surrounding brackets. Although the
writing the executing brackets outside of the surrounding brackets is valid the second example should be used as this
sets clear boundaries for the IIFE as the surrounding brackets isolate the whole IIFE.

无论何时，想要创建一个新的封闭的定义域，那就用 IIFE。它不仅避免了干扰，也使得内存在执行完后立即释放。

所有脚本文件建议都从 IIFE 开始。

立即执行的函数表达式的执行括号应该写在外包括号内。虽然写在内还是写在外都是有效的，但写在内使得整个表达式看起来更像一个整体，因此推荐这么做。

**Not recommended**
```
(function(){})();
```

**Recommended**
```
(function(){}());
```

The following pattern should be used to format your IIFE:

如果你想引用全局变量或者是外层 IIFE 的变量，可以通过下列方式传参：

```
(function(){
  'use strict';

  // Code goes here

}());
```

If you want to use global variables or variables form an outer IIFE you should pass them as parameters to your IIFE:
```
(function($, w, d){
  'use strict';

  $(function() {
    w.alert(d.querySelectorAll('div').length);
  });
}(jQuery, window, document));
```

***

### Strict mode(严格模式)

ECMAScript 5 strict mode can be enabled globally in your script or on function level. It enables more strict error
handling as well different javascript semantics. Strict mode also enforces a syntax that allows engines to optimize
the javascript better and strict more scripts can run faster than normal scripts.

Strict mode also blocks the usage of reserved words that possibly get introduced in the future.

You should always enforce strict mode in your scripts. Do so by applying it in your isolation IIFE. Don't apply it to
your whole script by include it as first statement in your script. This could possibly cause issues with 3rd party
libraries.

ECMAScript 5 严格模式可在整个脚本或独个方法内被激活。它对应不同的 javascript 语境会做更加严格的错误检查。严格模式也确保了 javascript 代码更加的健壮，运行的也更加快速。

严格模式会阻止使用在未来很可能被引入的预留关键字。

你应该在你的脚本中启用严格模式，最好是在独立的 IIFE 中应用它。避免在你的脚本第一行使用它而导致你的所有脚本都启动了严格模式，这有可能会引发一些第三方类库的问题

**Not recommended**
```
// Script starts here
'use strict';

(function(){

  // Your code starts here

}());
```

**Recommended**
```
(function(){
  'use strict';

  // Your code starts here

}());
```

***

### Variable declarations(变量声明)

Always use `var` to declare your variables. When you fail to specify var, the variable gets placed in the global
context, potentially clobbering existing values. Also, if there's no declaration, it's hard to tell in what scope a
variable lives (e.g., it could be in the Document or Window just as easily as in the local scope).
So always declare with var.

Using strict mode can help to identify issues where you might mistyped a variable name resulting in a ReferenceError.

总是使用 var 来声明变量。如不指定 var，变量将被隐式地声明为全局变量，这将对变量难以控制。如果没有声明，变量处于什么定义域就变得不清（可以是在 Document 或 Window 中，也可以很容易地进入本地定义域）。所以，请总是使用 var 来声明变量。

采用严格模式带来的好处是，当你手误输入错误的变量名时，它可以通过报错信息来帮助你定位错误出处。

**Not recommended**
```
x = 10;
y = 100;
```

**Recommended**
```
var x = 10,
    y = 100;
```

***

### Understand Javascript scope and hoisting(理解 JavaScript 的定义域和定义域提升)

In Javascript variable and function declarations will be hoisted before execution. Javascript only knows function scope
and there is no block scope as you know it from other programming languages. This means that if you declare a variable
inside a if statement or for loop this variable is declared for the whole function scope and not only locally in the
block statement.

To illustrate this check the following example that will show how a javascript interpreter is hoisting the declarations
in a function scope:

在 JavaScript 中变量和方法定义会自动提升到执行之前。JavaScript 只有 function 级的定义域，而无其他很多编程语言中的块定义域，所以使得你在某一 function 内的某语句和循环体中定义了一个变量，此变量可作用于整个 function 内，而不仅仅是在此语句或循环体中，因为它们的声明被 JavaScript 自动提升了。

我们通过例子来看清楚这到底是怎么一回事：

**Raw function(原 function)**
```
(function(log){
  'use strict';

  var a = 10;

  for(var i = 0; i < a; i++) {
    var b = i * i;
    log(b);
  }

  if(a === 10) {
    var f = function() {
      log(a);
    };
    f();
  }

  function x() {
    log('Mr. X!');
  }
  x();

}(window.console.log));
```

**Hoisted by Javscript engine(被 JS 提升过后)**
```
(function(log){
  'use strict';
  // All variables used in the closure will be hoisted to the top of the function
  var a,
      i,
      b,
      f;
  // All functions in the closure will be hoisted to the top
  function x() {
    log('Mr. X!');
  }

  a = 10;

  for(i = 0; i < a; i++) {
    b = i * i;
    log(b);
  }

  if(a === 10) {
    // Function assignments will only result in hoisted variables but the function body will not be hoisted
    // Only by using a real function declaration the whole function will be hoisted with its body
    f = function() {
      log(a);
    };
    f();
  }

  x();

}(window.console.log));
```

Considering now the hoisting above you can now see that you could also run the following code without any exceptions:

**Valid code(有效代码)**
```
(function(log){
  'use strict';

  var a = 10;

  i = 5;

  x();

  for(var i; i < a; i++) {
    log(b);
    var b = i * i;
  }

  if(a === 10) {
    f = function() {
      log(a);
    };
    f();

    var f;
  }

  function x() {
    log('Mr. X!');
  }

}(window.console.log));
```

As you can see this looks very confusing and misunderstanding hoisting can lead to unexpected results. To minimize the
risk of errors and bugs that resulted from misunderstanding hoisting your should follow the style rule of hoisted
declarations in the next section.

正如你所看到的这段令人充满困惑与误解的代码导致了出人意料的结果。只有良好的声明习惯，也就是下一章节我们要提到的声明规则，才能尽可能的避免这类错误风险。

***

### Use hoisted declarations(提升声明)

To minimize risk of misunderstanding and misinterpreting results from hoisted variable and function declarations (see
previous section) you should always try to hoist your variable and function declarations manually. This means that
you should declare all your variables that you're using in a function as a fist statement in the function.

Use only one `var` keyword and comma separate multiple declarations.

为避免上一章节所述的变量和方法定义被自动提升造成误解，把风险降到最低，我们应该手动地显示地去声明变量与方法。也就是说，所有的变量以及方法，应当定义在 function 内的首行。
只用一个 `var` 关键字声明，多个变量用逗号隔开。

**Not recommended**
```
(function(log){
  'use strict';

  var a = 10;
  var b = 10;

  for(var i = 0; i < 10; i++) {
    var c = a * b * i;
  }

  function f() {

  }

  var d = 100;
  var x = function() {
    return d * d;
  };
  log(x());

}(window.console.log));
```

**Recommended**
```
(function(log){
  'use strict';

  var a = 10,
      b = 10,
      i,
      c,
      d,
      x;

  function f() {

  }

  for(i = 0; i < 10; i++) {
    c = a * b * i;
  }



  d = 100;
  x = function() {
    return d * d;
  };
  log(x());

}(window.console.log));
```

Being pragmatic you should directly initialize your variables during hoisted declaration.

把赋值尽量写在变量申明中。

**Not recommended**
```
var a,
    b,
    c;

a = 10;
b = 10;
c = 100;
```

**Recommended**
```
var a = 10,
    b = 10,
    c = 100;
```

***

### Always use strict equal(总是使用带类型判断的比较判断)

Always use `===` explicit comparison operators and avoid the hassle you can go through by debugging issues resulted
from the very much overcomplicated javascript type coercion.

If you're using `===` operators both operands need to be from the same type in order to be valid and there will no
type coercion be performed.

If you'd like to get more information on type coercion you should read
[this article by Dmitry Soshnikov](http://dmitrysoshnikov.com/notes/note-2-ecmascript-equality-operators/).

By using only `==` you're telling javascript to use type coercion where needed which can be very complicated to trace
down. A few examples can be seen below that should give you a indication how strange type coercion can feel:

总是使用 === 精确的比较操作符，避免在判断的过程中，由 JavaScript 的强制类型转换所造成的困扰。

如果你使用 === 操作符，那比较的双方必须是同一类型为前提的条件下才会有效。

如果你想了解更多关于强制类型转换的信息，你可以读一读 [this article by Dmitry Soshnikov](http://dmitrysoshnikov.com/notes/note-2-ecmascript-equality-operators/) 的这篇文章。

在只使用 == 的情况下，JavaScript 所带来的强制类型转换使得判断结果跟踪变得复杂，下面的例子可以看出这样的结果有多怪了：

```
(function(log){
  'use strict';

  log('0' == 0); // true
  log('' == false); // true
  log('1' == true); // true
  log(null == undefined); // true

  var x = {
    valueOf: function() {
      return 'X';
    }
  };

  log(x == 'X');

}(window.console.log));
```

***

### Use truthy / falsy checks wisely(明智地使用真假判断)

By only putting one variable or expression into a if statement you're creating a truthy / falsy check. The expression
`if(a == true)` is not the same as `if(a)`. The later expression is creating a special check which is called truthy /
falsy check. This check performs some special operations in order to evaluate to true or false. The following
expressions are falsy in javascript `false`, `0`, `undefined`, `null`, `NaN`, `''` (empty string).

Truthy / falsy checks are very helpful as they allow you to quickly react on a group of conditions that you'd like to
take care of but you need to be sure about what you actually want to do.

The following example shows how truthy / falsy checks work:

当我们在一个 if 条件语句中使用变量或表达式时，会做真假判断。`if(a == true)` 是不同于 `if(a)` 的。后者的判断比较特殊，我们称其为真假判断。这种判断会通过特殊的操作将其转换为 true 或 false，下列表达式统统返回 `false：false, 0, undefined, null, NaN, ''`（空字符串）.

这种真假判断在我们只求结果而不关心过程的情况下，非常的有帮助。

以下示例展示了真假判断是如何工作的：

```
(function(log){
  'use strict';

  function logTruthyFalsy(expr) {
    if(expr) {
      log('truthy');
    } else {
      log('falsy');
    }
  }

  logTruthyFalsy(true); // truthy
  logTruthyFalsy(1); // truthy
  logTruthyFalsy({}); // truthy
  logTruthyFalsy([]); // truthy
  logTruthyFalsy('0'); // truthy

  logTruthyFalsy(false); // falsy
  logTruthyFalsy(0); // falsy
  logTruthyFalsy(undefined); // falsy
  logTruthyFalsy(null); // falsy
  logTruthyFalsy(NaN); // falsy
  logTruthyFalsy(''); // falsy

}(window.console.log));
```

***

### Logical operators for variable assignments(变量赋值时的逻辑操作)

The logical operators `||` and `&&` can also be used to return non-boolean values. If used with non booleans the
operands will evaluate each expression from left to right and performs a falsy check. Depending on the operation, one
of the expressions will be returned. This can be very helpful for variable assignments and should be considered in
order to simplify your code.

逻辑操作符 || 和 && 也可被用来返回布尔值。如果操作对象为非布尔对象，那每个表达式将会被自左向右地做真假判断。基于此操作，最终总有一个表达式被返回回来。这在变量赋值时，是可以用来简化你的代码的。

**Not recommended**
```
if(!x) {
  if(!y) {
    x = 1;
  } else {
    x = y;
  }
}
```

**Recommended**
```
x = x || y || 1;
```

This shorthand is often used to validated function parameters. The following example illustrates one usage example:

这一小技巧经常用来给方法设定默认的参数。

```
(function(log){
  'use strict';

  function multiply(a, b) {
    a = a || 1;
    b = b || 1;

    log('Result ' + a * b);
  }

  multiply(); // Result 1
  multiply(10); // Result 10
  multiply(3, NaN); // Result 3
  multiply(9, 5); // Result 45

}(window.console.log));
```

***

### Semicolons(分号)

Always use semicolons. Relying on implicit insertion can cause subtle, hard to debug problems. Don't do it.
You're better than that. There are a couple places where missing semicolons are particularly dangerous:

总是使用分号，因为隐式的代码嵌套会引发难以察觉的问题。当然我们更要从根本上来杜绝这些问题[1] 。以下几个示例展示了缺少分号的危害：

```
// 1.
MyClass.prototype.myMethod = function() {
  return 42;
}  // No semicolon here.

(function() {
  // Some initialization code wrapped in a function to create a scope for locals.
})();


var x = {
  'i': 1,
  'j': 2
}  // No semicolon here.

// 2.  Trying to do one thing on Internet Explorer and another on Firefox.
// I know you'd never write code like this, but throw me a bone.
[ffVersion, ieVersion][isIE]();


var THINGS_TO_EAT = [apples, oysters, sprayOnCheese]  // No semicolon here.

// 3. conditional execution a la bash
-1 == resultOfOperation() || die();
```

**So what happens?**

1.  JavaScript error - first the function returning 42 is called with the second function as a parameter, then
the number 42 is "called" resulting in an error.
1.  You will most likely get a 'no such property in undefined' error at runtime as it tries to
call `x[ffVersion, ieVersion][isIE]()`.
1.  `die` is always called since the array minus 1 is `NaN` which is never equal to anything (not even if
`resultOfOperation()` returns `NaN`) and `THINGS_TO_EAT` gets assigned the result of `die()`.

1. JavaScript 错误 —— 首先返回 42 的那个 function 被第二个 function 当中参数传入调用，接着数字 42 也被“调用”而导致出错。
2. 八成你会得到 ‘no such property in undefined’ 的错误提示，因为在真实环境中的调用是这个样子：`x[ffVersion, ieVersion][isIE]().`
3. `die` 总是被调用。因为数组减 1 的结果是 NaN，它不等于任何东西（无论 resultOfOperation 是否返回 `NaN`）。所以最终的结果是 `die()` 执行完所获得值将赋给 `THINGS_TO_EAT`.

**Why?**

JavaScript requires statements to end with a semicolon, except when it thinks it can safely infer their existence.
In each of these examples, a function declaration or object or array literal is used inside a statement. The closing
brackets are not enough to signal the end of the statement. Javascript never ends a statement if the next token is an
infix or bracket operator.

This has really surprised people, so make sure your assignments end with semicolons.

JavaScript 中语句要以分号结束，否则它将会继续执行下去，不管换不换行。以上的每一个示例中，函数声明或对象或数组，都变成了在一句语句体内。要知道闭合圆括号并不代表语句结束，JavaScript 不会终结语句，除非它的下一个 token 是一个中缀符[2] 或者是圆括号操作符。

这真是让人大吃一惊，所以乖乖地给语句末加上分号吧。

**Clarification: Semicolons and functions**

Semicolons should be included at the end of function expressions, but not at the end of function declarations.
The distinction is best illustrated with an example:

澄清：分号与函数

分号需要用在表达式的结尾，而并非函数声明的结尾。区分它们最好的例子是：

```
var foo = function() {
  return true;
};  // semicolon here.

function foo() {
  return true;
}  // no semicolon here.
```

***

### Nested functions(嵌套函数)

Nested functions can be very useful, for example in the creation of continuations and for the task of hiding helper
functions. Feel free to use them.

嵌套函数是非常有用的，比如用在持续创建和隐藏辅助函数的任务中。你可以非常自由随意地使用它们。

***

### Function declaration within blocks(语句块内的函数声明)

Do not declare functions in blocks. This is not valid in ECMAScript 5 strict mode. Functions should be declared on
top level. Don't hesitate to use variables initialized with function expressions inside of blocks though:

切勿在语句块内声明函数，在 ECMAScript 5 的严格模式下，这是不合法的。函数声明应该在定义域的顶层。但在语句块内可将函数申明转化为函数表达式赋值给变量。

**Not recommended**
```
if (x) {
  function foo() {}
}
```

**Recommended**
```
if (x) {
  var foo = function() {};
}
```

***

### Exceptions(异常)

You basically can't avoid exceptions if you're doing something non-trivial (using an application development framework,
etc.).

Without custom exceptions, returning error information from a function that also returns a value can be tricky, not to
mention inelegant. Bad solutions include passing in a reference type to hold error information or always returning
Objects with a potential error member. These basically amount to a primitive exception handling hack.
Feel free to use custom exceptions when appropriate.

In complex environments you should consider throwing objects rather than just strings (default throws).

基本上你无法避免出现异常，特别是在做大型开发时（使用应用开发框架等等）。

在没有自定义异常的情况下，从有返回值的函数中返回错误信息一定非常的棘手，更别提多不优雅了。不好的解决方案包括了传第一个引用类型来接纳错误信息，或总是返回一个对象列表，其中包含着可能的错误对象。以上方式基本上是比较简陋的异常处理方式。适时可做自定义异常处理。

在复杂的环境中，你可以考虑抛出对象而不仅仅是字符串（默认的抛出值）。

```
if(name === undefined) {
  throw {
    name: 'System Error',
    message: 'A name should always be specified!'
  }
}
```

***

### Standard features(标准特性)

Always preferred over non-standards features. For maximum portability and compatibility, always prefer standards
features over non-standards features (e.g., `string.charAt(3)` over `string[3]` and element access with DOM functions
instead of using an application-specific shorthand).

总是优先考虑使用标准特性。为了最大限度地保证扩展性与兼容性，总是首选标准的特性，而不是非标准的特性（例如：首选 string.charAt(3) 而不是 string[3]；首选 DOM 的操作方法来获得元素引用，而不是某一应用特定的快捷方法）。

***

### Simple prototypical inheritance(简易的原型继承)

If you need inheritance of your objects in Javascript follow a simple pattern to create inheritance. If you know that
you'll end up with complex object inheritance consider a inheritance library like
[Proto.js by Axel Rauschmayer](https://github.com/rauschma/proto-js).

For simple cases use  like the bellow.

如果你想在 JavaScript 中继承你的对象，请遵循一个简易的模式来创建此继承。如果你预计你会遇上复杂对象的继承，那可以考虑采用一个继承库，比如 [Proto.js by Axel Rauschmayer](https://github.com/rauschma/proto-js).
简易继承请用以下方式

```
(function(log){
  'use strict';

  // Constructor function
  function Apple(name) {
    this.name = name;
  }
  // Defining a method of apple
  Apple.prototype.eat = function() {
    log('Eating ' + this.name);
  };

  // Constructor function
  function GrannySmithApple() {
    // Invoking parent constructor
    Apple.prototype.constructor.call(this, 'Granny Smith');
  }
  // Set parent prototype while creating a copy with Object.create
  GrannySmithApple.prototype = Object.create(Apple.prototype);
  // Set constructor to the sub type, otherwise points to Apple
  GrannySmithApple.prototype.constructor = GrannySmithApple;

  // Calling a super method
  GrannySmithApple.prototype.eat = function() {
    // Be sure to apply it onto our current object with call(this)
    Apple.prototype.eat.call(this);

    log('Poor Grany Smith');
  };

  // Instantiation
  var apple = new Apple('Test Apple');
  var grannyApple = new GrannySmithApple();

  log(apple.name); // Test Apple
  log(grannyApple.name); // Granny Smith

  // Instance checks
  log(apple instanceof Apple); // true
  log(apple instanceof GrannySmithApple); // false

  log(grannyApple instanceof Apple); // true
  log(grannyApple instanceof GrannySmithApple); // true

  // Calling method that calls super method
  grannyApple.eat(); // Eating Granny Smith\nPoor Grany Smith

}(window.console.log));
```

***

### Use Closures(使用闭包)

The ability to create closures is perhaps the most useful and often overlooked feature of JS.
Here is [a good description of how closures work](http://jibbering.com/faq/faq_notes/closures.html).

闭包的创建也许是 JS 最有用也是最易被忽略的能力了。关于闭包如何工作的合理解释[a good description of how closures work](http://jibbering.com/faq/faq_notes/closures.html).。

***

### Don't create functions in loops(切勿在循环中创建函数)

It's generally a potential source for bugs if you write functions that create a closure inside of simple loops. The
following example illustrates a common pitfall.

在简单的循环语句中加入函数是非常容易形成闭包而带来隐患的。下面的例子就是一个典型的陷阱：

**Not recommended**
```
(function(log, w){
  'use strict';

  // numbers and i is defined in the current function closure
  var numbers = [1, 2, 3],
      i;

  for(i = 0; i < numbers.length; i++) {
    w.setTimeout(function() {
      // At the moment when this gets executed the i variable, coming from the outer function scope
      // is set to 3 and the current program is alerting the message 3 times
      // 'Index 3 with number undefined
      // If you understand closures in javascript you know how to deal with those cases
      // It's best to just avoid functions / new closures in loops as this prevents those issues

      w.alert('Index ' + i + ' with number ' + numbers[i]);
    }, 0);
  }

}(window.console.log, window));
```

The following variation of the above example solves our problem / bug but still violates our policy to not create
functions / closures inside of loops.

接下来的改进虽然已经解决了上述例子中的问题或 bug，但还是违反了不在循环中创建函数或闭包的原则。

**Not recommended**
```
(function(log, w){
  'use strict';

  // numbers and i is defined in the current function closure
  var numbers = [1, 2, 3],
      i;

  for(i = 0; i < numbers.length; i++) {
    // Creating a new closure scope with an IIFE solves the problem
    // The delayed function will use index and number which are
    // in their own closure scope (one closure per loop iteration).
    // ---
    // Still this is not recommended as we violate our rule to not
    // create functions within loops and we are creating two!

    (function(index, number){
      w.setTimeout(function() {
        // Will output as expected 0 > 1, 1 > 2, 2 > 3
        w.alert('Index ' + index + ' with number ' + number);
      }, 0);
    }(i, numbers[i]));
  }

}(window.console.log, window));
```

The following variation solves our problem / bug and we also comply with our style guide. However, this seems to be
heavily overcomplicated and we should look for a better / easier way.

接下来的改进已解决问题，而且也遵循了规范。可是，你会发现看上去似乎过于复杂繁冗了，应该会有更好的解决方案吧。

**Partially recommended**
```
(function(log, w){
  'use strict';

  // numbers and i is defined in the current function closure
  var numbers = [1, 2, 3],
      i;

  // Create a function outside of the loop that will accept arguments to create a
  // function closure scope. This function will return a function that executes in this
  // closure parent scope.
  function alertIndexWithNumber(index, number) {
    return function() {
      w.alert('Index ' + index + ' with number ' + number);
    };
  }

  // First parameter is a function call that returns a function.
  // ---
  // This solves our problem and we don't create a function inside our loop
  for(i = 0; i < numbers.length; i++) {
    w.setTimeout(alertIndexWithNumber(i, numbers[i]), 0);
  }

}(window.console.log, window));
```

By using a functional approach for our loop we solve the problem immediately as we create a new closure with every loop.
Functional style is recommended and will also lead to more natural and expected results.

将循环语句转换为函数执行的方式问题能得到立马解决，每一次循环都会对应地创建一次闭包。函数式的风格更加值得推荐，而且看上去也更加地自然和可预料。

**Recommended**
```
(function(log, w){
  'use strict';

  // numbers and i is defined in the current function closure
  var numbers = [1, 2, 3],
      i;

  numbers.forEach(function(number, index) {
    w.setTimeout(function() {
      w.alert('Index ' + index + ' with number ' + number);
    }, 0);
  });

}(window.console.log, window));
```

***

### The (evil) eval function(eval 函数（魔鬼）)

`eval()` makes for confusing semantics and is dangerous to use if the string being eval()'d contains user input.
There's usually a better, clearer, and safer way to write your code, so its use is generally not permitted.

`eval()`不但混淆语境还很危险，总会有比这更好、更清晰、更安全的另一种方案来写你的代码，因此尽量不要使用 evil 函数。



***

### The this keyword(this 关键字)

Use the `this` keyword only in object constructors, methods, and in setting up closures. The semantics of this can be
tricky. At times it refers to the global object (in most places), the scope of the caller (in eval), a node in the DOM
tree (when attached using an event handler HTML attribute), a newly created object (in a constructor), or some other
object (if function was call()ed or apply()ed).

Because this is so easy to get wrong, limit its use to those places where it is required:

- in constructors
- in methods of objects (including in the creation of closures)

只在对象构造器、方法和在设定的闭包中使用 this 关键字。this 的语义在此有些误导。它时而指向全局对象（大多数时），时而指向调用者的定义域（在 eval 中），时而指向 DOM 树中的某一节点（当用事件处理绑定到 HTML 属性上时），时而指向一个新创建的对象（在构造器中），还时而指向其它的一些对象（如果函数被 call() 和 apply() 执行和调用时）。

正因为它是如此容易地被搞错，请限制它的使用场景：

- 在构造函数中
- 在对象的方法中（包括由此创建出的闭包内）

***

### Functional is preferred(首选函数式风格)

Using functional style programming you can simplify your code and reduce maintenance cost by gaining easy re-usability,
proper isolation and less dependencies.

The following example compares two solutions for the same problem of summing up all number elements in an array. The
first example is a classical procedural approach while the second one makes use of functional style programming and the
ECMA Script 5.1 array functions.

Exception: In situations where performance is considered to be more important than maintainability then you might
consider the most performant solution over the most maintainable (i.e. using simple for loop over forEach)

函数式编程让你可以简化代码并缩减维护成本，因为它容易复用，又适当地解耦和更少的依赖。

接下来的例子中，在一组数字求和的同一问题上，比较了两种解决方案。第一个例子是经典的程序处理，而第二个例子则是采用了函数式编程和 ECMA Script 5.1 的数组方法。

例外：往往在重代码性能轻代码维护的情况之下，要选择最优性能的解决方案而非维护性高的方案（比如用简单的循环语句代替 forEach）。

**Not recommended**
```
(function(log){
  'use strict';

  var arr = [10, 3, 7, 9, 100, 20],
      sum = 0,
      i;


  for(i = 0; i < arr.length; i++) {
    sum += arr[i];
  }

  log('The sum of array ' + arr + ' is: ' + sum)

}(window.console.log));
```

**Recommended**
```
(function(log){
  'use strict';

  var arr = [10, 3, 7, 9, 100, 20];

  var sum = arr.reduce(function(prevValue, currentValue) {
    return prevValue + currentValue;
  }, 0);

  log('The sum of array ' + arr + ' is: ' + sum);

}(window.console.log));
```

An other example would be to filter an array for certain criteria so that we can create a new array that only contains
those elements that match the criteria.

另一个例子通过某一规则对一个数组进行过滤匹配来创建一个新的数组。

**Not recommended**
```
(function(log){
  'use strict';

  var numbers = [11, 3, 7, 9, 100, 20, 14, 10],
      numbersGreaterTen = [],
      i;


  for(i = 0; i < numbers.length; i++) {
    if(numbers[i] > 10) {
      numbersGreaterTen.push(numbers[i]);
    }
  }

  log('From the list of numbers ' + numbers + ' only ' + numbersGreaterTen + ' are greater than ten');

}(window.console.log));
```

**Recommended**
```
(function(log){
  'use strict';

  var numbers = [11, 3, 7, 9, 100, 20, 14, 10];

  var numbersGreaterTen = numbers.filter(function(element) {
    return element > 10;
  });

  log('From the list of numbers ' + numbers + ' only ' + numbersGreaterTen + ' are greater than ten');

}(window.console.log));
```

***

### Use ECMA Script 5(使用 ECMA Script 5)

Use the syntactical sugar and functional style that was added with ECMA Script 5. It's simplifying your programming
style and makes your code more flexible and re-usable.

建议使用 ECMA Script 5 中新增的语法糖和函数。这将简化你的程序，并让你的代码更加灵活和可复用。

***

### Array and object property iteration(数组和对象的属性迭代)

The ECMA5 way to iterate over an array is preferred. Use Array.forEach or Array.every if you would like to cancel the
iteration at a certain condition.

用 ECMA5 的迭代方法来迭代数组。使用 Array.forEach 或者如果你要在特殊场合下中断迭代，那就用 `Array.every`。

```
(function(log){
  'use strict';

  // Iterate over an array and break at a certain condition
  [1, 2, 3, 4, 5].every(function(element, index, arr) {
    log(element + ' at index ' + index + ' in array ' + arr);

    if(index !== 5) {
      return true;
    }
  });

  // Defining a simple javascript object
  var obj = {
    a: 'A',
    b: 'B',
    'c-d-e': 'CDE'
  };

  // Iterating over the object keys
  Object.keys(obj).forEach(function(element, index, arr) {
    log('Key ' + element + ' has value ' + obj[element]);
  });

}(window.console.log));
```

***

### Don't use switch(不要使用 switch)

switch is a very error prone control statement in every programming language. Use if else if instead.

switch 在所有的编程语言中都是个非常错误的难以控制的语句，建议用 if else 来替换它。

***

### Array and Object literals(数组和对象字面量)

Use Array and Object literals instead of Array and Object constructors. Array constructors are error-prone due to their
arguments.

用数组和对象字面量来代替数组和对象构造器。数组构造器很容易让人在它的参数上犯错。

**Not recommended**
```
// Length is 3.
var a1 = new Array(x1, x2, x3);

// Length is 2.
var a2 = new Array(x1, x2);

// If x1 is a number and it is a natural number the length will be x1.
// If x1 is a number but not a natural number this will throw an exception.
// Otherwise the array will have one element with x1 as its value.
var a3 = new Array(x1);

// Length is 0.
var a4 = new Array();
```

Because of this, if someone changes the code to pass 1 argument instead of 2 arguments, the array might not have the
expected length. To avoid these kinds of weird cases, always use the more readable array literal.

正因如此，如果将代码传参从两个变为一个，那数组很有可能发生意料不到的长度变化。为避免此类怪异状况，请总是采用更多可读的数组字面量。

**Recommended**
```
var a = [x1, x2, x3];
var a2 = [x1, x2];
var a3 = [x1];
var a4 = [];
```

Object constructors don't have the same problems, but for readability and consistency object literals should be used.

对象构造器不会有类似的问题，但是为了可读性和统一性，我们应该使用对象字面量。

**Not recommended**
```
var o = new Object();

var o2 = new Object();
o2.a = 0;
o2.b = 1;
o2.c = 2;
o2['strange key'] = 3;
```

Should be written as:

**Recommended**
```
var o = {};

var o2 = {
  a: 0,
  b: 1,
  c: 2,
  'strange key': 3
};
```

***

### Modifying prototypes of builtin objects(修改内建对象的原型链)

Modifying builtins like `Object.prototype` and `Array.prototype` are strictly forbidden. Modifying other builtins like
`Function.prototype` is less dangerous but still leads to hard to debug issues in production and should be avoided.

修改内建的诸如 `Object.prototype` 和 `Array.prototype` 是被严厉禁止的。修改其它的内建对象比如 `Function.prototype`，虽危害没那么大，但始终还是会导致在开发过程中难以 debug 的问题，应当也要避免。

***

### Custom toString() methods(自定义 toString() 方法)

You can control how your objects string-ify themselves by defining a custom `toString()` method. This is fine, but you
need to ensure that your method (1) always succeeds and (2) does not have side-effects. If your method doesn't meet
these criteria, it's very easy to run into serious problems. For example, if `toString()` calls a method that does an
assert, assert might try to output the name of the object in which it failed, which of course requires
calling `toString()`.

你可以通过自定义 `toString()` 来控制对象字符串化。这很好，但你必须保证你的方法总是成功并不会有其它副作用。如果你的方法达不到这样的标准，那将会引发严重的问题。如果 `toString()`调用了一个方法，这个方法做了一个断言[3] ，当断言失败，它可能会输出它所在对象的名称，当然对象也需要调用 `toString()`。

***

### Parentheses(圆括号)

Use sparingly and in general only where required by the syntax and semantics. Never use parentheses for unary
operators such as `delete`, `typeof` and `void` or after keywords such as `return`, `throw` as well
as others (`case`, in or `new`).

一般在语法和语义上真正需要时才谨慎地使用圆括号。不要用在一元操作符上，例如 `delete`, `typeof` and `void` or after keywords such as `return`, `throw` as well
as others (`case`, in or `new`).

***

### Strings(字符串)

For consistency single-quotes (') are preferred to double-quotes ("). This is helpful when creating
strings that include HTML:

统一使用单引号(‘)，不使用双引号(“)。这在创建 HTML 字符串非常有好处：

```
var msg = 'This is some HTML <div class="makes-sense"></div>';
```

***

### Conditional Ternary Operator (shorthand if)(三元条件判断（if 的快捷方法）)

Use the ternary operator for assignments or return statements. Use it only in simple conditions and avoid it in complex
ones. No body likes to wrap his brain around 10 lines of nested ternary operators.

用三元操作符分配或返回语句。在比较简单的情况下使用，避免在复杂的情况下使用。没人愿意用 10 行三元操作符把自己的脑子绕晕。

**Not recommended**
```
if(x === 10) {
  return 'valid';
} else {
  return 'invalid';
}
```

**Recommended**
```
return x === 10 ? 'valid' : 'invalid';
```

***

## CSS and Sass (SCSS) style rules(CSS 和 Sass (SCSS) 规范)

***

### ID and class naming(ID和class(类)命名)

Instead of presentational or cryptic names, always use ID and class names that reflect the purpose of the element in
question, or that are otherwise generic.

Names that are specific and reflect the purpose of the element should be preferred as these are most understandable
and the least likely to change.

Generic names are simply a fallback for elements that have no particular or no meaning different from their siblings.
They are typically needed as “helpers.”

Even though class names and ID's have no semantic meaning to computer interpreters, semantic names are often the right
choice as they represent the information meaning and don't introduce presentational constraints.

ID和class(类)名总是使用可以反应元素目的和用途的名称，或其他通用名称。代替表象和晦涩难懂的名称。

应该首选具体和反映元素目的的名称，因为这些是最可以理解的，而且发生变化的可能性最小。

通用名称只是多个元素的备用名，他们兄弟元素之间是一样的，没有特别意义。
区分他们，使他们具有特殊意义，通常需要为“帮手”。

尽管class(类)名和ID 的语义化对于计算机解析来说没有什么实际的意义，
语义化的名称 通常是正确的选择，因为它们所代表的信息含义，不包含表现的限制。

**Not recommended**
```
.fw-800 {
  font-weight: 800;
}

.red {
  color: red;
}
```

**Recommended**
```
.heavy {
  font-weight: 800;
}

.important {
  color: red;
}
```

***

### Avoid ID's where possible(合理的避免使用ID)

In general ID's should not be used to apply style. Styles on ID's can't be re-used and you can only use them once per
page. The only valid location for using an ID would be to identify a page or a whole site. Still you should always
consider using a class that you use once instead of an id.

一般情况下ID不应该被应用于样式。
ID的样式不能被复用并且每个页面中你只能使用一次ID。
使用ID唯一有效的是确定网页或整个站点中的位置。
尽管如此，你应该始终考虑使用class，而不是id，除非只使用一次。

**Not recommended**
```
#content .title {
  font-size: 2em;
}
```

**Recommended**
```
.content .title {
  font-size: 2em;
}
```

One other argument against using ID's would be that selector chains containing ID's are over-prioritized. A selector
containing just one ID is weighted higher than a selector containing 1000 class names only which makes it very odd.

另一个反对使用ID的观点是含有ID选择器权重很高。
一个只包含一个ID选择器权重高于包含1000个class(类)名的选择器，这使得它很奇怪。

```
// This selecor is considered with higher priority
#content .title {
  color: red;
}

// than this selector!
html body div.content.news-content .title.content-title.important {
  color: blue;
}
```

***

### Avoid elements in CSS selectors(CSS选择器中避免标签名)

When building your selectors use clear, precise and sensible class names. Don't use element selectors. If you're only
concerned about your class names and not about your elements your code gets a lot more maintainable.

From a separation of concerns perspective you don't want to dictate the markup / semantics from the presentation layer.
It might be that a ordered list needs to be changed to an unordered list or that a div will be converted to an article.
If you only care about sensible class names and don't use element selectors you'd only need to change your markup and
not your css.

当构建选择器时应该使用清晰， 准确和有语义的class(类)名。不要使用标签选择器。 如果你只关心你的class(类)名
，而不是你的代码元素，这样会更容易维护。

从分离的角度考虑,在表现层中不应该分配html标记/语义。
它可能是一个有序列表需要被改成一个无序列表，或者一个div将被转换成article。
如果你只使用具有实际意义的class(类)名，
并且不使用元素选择器，那么你只需要改变你的html标记，而不用改动你的CSS。

**Not recommended**
```
div.content > header.content-header > h2.title {
  font-size: 2em;
}
```

**Recommended**
```
.content > .content-header > .title {
  font-size: 2em;
}
```

***

### Be as precise as possible(尽可能的精确)

A lot of front-end developers don't use direct child selectors when they write their selector chains. Sometimes this
can cause painful design issues and other times it's just a performance eater. However, in any case, it's a very bad
practice. If you don't write very generic selectors that need to match down to the bottom of the DOM you should always
consider direct child selectors.

Consider the following DOM:

很多前端开发人员写选择器链的时候不使用 直接子选择器（注：直接子选择器和后代选择器的区别）。
有时，这可能会导致疼痛的设计问题并且有时候可能会很耗性能。
然而，在任何情况下，这是一个非常不好的做法。
如果你不写很通用的，需要匹配到DOM末端的选择器， 你应该总是考虑直接子选择器。

考虑下面的DOM:

```
<article class="content news-content">
  <span class="title">News event</span>
  <div class="content-body">
    <div class="title content-title">
      Check this out
    </div>

    <p>This is a news article content</p>

    <div class="teaser">
      <div class="title">Buy this</div>
      <div class="teaser-content">Yey!</div>
    </div>
  </div>
</article>
```

The following CSS would apply to all three elements that have a title class. This then would need to be overridden again
with more granular selectors in order to fix the content title and the teaser title.

下面的CSS将应用于有title类的全部三个元素。
然后，要解决content类下的title类 和 teaser类下的title类下不同的样式，这将需要更精确的选择器再次重写他们的样式。

**Not recommended**
```
.content .title {
  font-size: 2rem;
}
```

**Recommended**
```
.content > .title {
  font-size: 2rem;
}

.content > .content-body > .title {
  font-size: 1.5rem;
}

.content > .content-body > .teaser > .title {
  font-size: 1.2rem;
}
```

***

### Shorthand Properties(缩写属性)

CSS offers a variety of shorthand properties (like font) that should be used whenever possible, even in cases where
only one value is explicitly set.

Using shorthand properties is useful for code efficiency and understandability.

CSS提供了各种缩写属性（如 font 字体）应该尽可能使用，即使在只设置一个值的情况下。

使用缩写属性对于代码效率和可读性是有很有用的。

**Not recommended**
```
border-top-style: none;
font-family: palatino, georgia, serif;
font-size: 100%;
line-height: 1.6;
padding-bottom: 2em;
padding-left: 1em;
padding-right: 1em;
padding-top: 0;
```

**Recommended**
```
border-top: 0;
font: 100%/1.6 palatino, georgia, serif;
padding: 0 1em 2em;
```

***

### 0 and units(0 和 单位)

Omit unit specification after “0” values. Do not use units after 0 values unless they are required.

省略“0”值后面的单位。不要在0值后面使用单位，除非有值。

**Not recommended**
```
padding-bottom: 0px;
margin: 0em;
```

**Recommended**
```
padding-bottom: 0;
margin: 0;
```

***

### Hexadecimal Notation(十六进制表示法)

Use 3 character hexadecimal notation where possible. For color values that permit it, 3 character hexadecimal notation
is shorter and more succinct.

Always use lower case hex digits.

在可能的情况下，使用3个字符的十六进制表示法。
颜色值允许这样表示，
3个字符的十六进制表示法更简短。

始终使用小写的十六进制数字。

**Not recommended**
```
color: #FF33AA;
```

**Recommended**
```
color: #f3a;
```

***

### ID and Class Name Delimiters(ID 和 Class（类） 名的分隔符)

Separate words in ID and class names by a hyphen. Do not concatenate words and abbreviations in selectors by any
characters (including none at all) other than hyphens, in order to improve understanding and scannability.

Also as the standard foresees attribute selectors that recognise hyphens as separator of words `[attribute|=value]`
it's best to stick to the hyphen as separator.

使用连字符（中划线）分隔ID和Class（类）名中的单词。为了增强课理解性，在选择器中不要使用除了连字符（中划线）以为的任何字符（包括没有）来连接单词和缩写。

另外，作为该标准，预设属性选择器能识别连字符（中划线）作为单词[attribute|=value]的分隔符，
所以最好的坚持使用连字符作为分隔符。

**Not recommended**
```
.demoimage {}
.error_status {}
```

**Recommended**
```
#video-id {}
.ads-sample {}
```

***

### Hacks

Avoid user agent detection as well as CSS “hacks”—try a different approach first. It’s tempting to address styling
differences over user agent detection or special CSS filters, workarounds, and hacks. Both approaches should be
considered last resort in order to achieve and maintain an efficient and manageable code base. Put another way, giving
detection and hacks a free pass will hurt projects in the long run as projects tend to take the way of least
resistance. That is, allowing and making it easy to use detection and hacks means using detection and hacks more
frequently—and more frequently is too frequently.

避免用户代理检测以及CSS“hacks” – 首先尝试不同的方法。通过用户代理检测或特殊的CSS滤镜，变通的方法和 hacks 很容易解决样式差异。为了达到并保持一个有效的和可管理的代码库，这两种方法都应该被认为是最后的手段。换句话说，从长远来看，用户代理检测和hacks
会伤害项目，作为项目往往应该采取阻力最小的途径。也就是说，轻易允许使用用户代理检测和hacks 以后将过于频繁。

***

### Declaration Order(声明顺序)

This example should give a rough outline of how to order CSS properties within a selector. This is important in order
to guarantee better readability and better scannability.

As a best practice we should follow the following ordering (in the same order as the listing):

1.  structural
  1.  display
  1.  position, left, top, right etc.
  1.  overflow, float, clear etc.
  1.  margin, padding
1.  skin
  1.  background, border etc.
  1.  font, text

这是一个选择器内书写CSS属性顺序的大致轮廓。这是为了保证更好的可读性和可扫描重要。

作为最佳实践，我们应该遵循以下顺序（应该按照下表的顺序）：

1. 结构性属性：
  - display
  - position, left, top, right etc.
  - overflow, float, clear etc.
  - margin, padding
2. 表现性属性：
  - background, border etc.
  - font, text

**Not recommended**
```
.box {
  font-family: 'Arial', sans-serif;
  border: 3px solid #ddd;
  left: 30%;
  position: absolute;
  text-transform: uppercase;
  background-color: #eee;
  right: 30%;
  isplay: block;
  font-size: 1.5rem;
  overflow: hidden;
  padding: 1em;
  margin: 1em;
}
```

**Recommended**
```
.box {
  display: block;
  position: absolute;
  left: 30%;
  right: 30%;
  overflow: hidden;
  margin: 1em;
  padding: 1em;
  background-color: #eee;
  border: 3px solid #ddd;
  font-family: 'Arial', sans-serif;
  font-size: 1.5rem;
  text-transform: uppercase;
}
```

***

### Declaration Stops(声明结束)

End every declaration with a semicolon for consistency and extensibility reasons and put each declaration on a new line.

为了保证一致性和可扩展性，每个声明应该用分号结束，每个声明换行。

**Not recommended**
```
.test {
  display: block; height: 100px
}
```

**Recommended**
```
.test {
  display: block;
  height: 100px;
}
```

***

### Property Name Stops(属性名结束)

Use a space after a property name’s colon. Always use a single space between property and value (but no space between
property and colon) for consistency reasons.

属性名的冒号后使用一个空格。出于一致性的原因，
属性和值（但属性和冒号之间没有空格）的之间始终使用一个空格。

**Not recommended**
```
h3 {
  font-weight:bold;
}
```

**Recommended**
```
h3 {
  font-weight: bold;
}
```

***

### Selector and Declaration Separation(选择器和声明分离)

Always start a new line for each selector and declaration.

每个选择器和属性声明总是使用新的一行。

**Not recommended**
```
a:focus, a:active {
  position: relative; top: 1px;
}
```

**Recommended**
```
h1,
h2,
h3 {
  font-weight: normal;
  line-height: 1.2;
}
```

***

### Rule Separation(规则分隔)

Always put a blank line (two line breaks) between rules.

规则之间始终有一个空行（双换行符）分隔。

**Recommended**
```
html {
  background: #fff;
}

body {
  margin: auto;
  width: 50%;
}
```

***

### CSS Quotation Marks(CSS引号)

Use double ("") rather than single ('') quotation marks for attribute selectors or property values.
Do not use quotation marks in URI values (url()).

属性选择器或属性值用双引号（””），而不是单引号（”）括起来。
URI值（url()）不要使用引号。

**Not recommended**
```
@import url('//cdn.com/foundation.css');

html {
  font-family: 'open sans', arial, sans-serif;
}

body:after {
  content: 'pause';
}
```

**Recommended**
```
@import url(//cdn.com/foundation.css);

html {
  font-family: "open sans", arial, sans-serif;
}

body:after {
  content: "pause";
}
```

***

### Nested selectors (SCSS)(选择器嵌套 (SCSS))

In Sass you can nest selectors which is much cleaner and the code becomes much more readable. Nest all selectors but
try to avoid nesting without any content. If you need to specify some style attributes for a child element where the
parent element will not receive any styling use a regular CSS selector chain. This will prevent your script to look
overcomplicated.

在Sass中你可以嵌套选择器，这可以使代码变得更清洁和可读。嵌套所有的选择器，但尽量避免嵌套没有任何内容的选择器。
如果你需要指定一些子元素的样式属性，而父元素将不什么样式属性，
可以使用常规的CSS选择器链。
这将防止您的脚本看起来过于复杂。

**Not recommended**
```scss
// Not a good example by not making use of nesting at all
.content {
  display: block;
}

.content > .news-article > .title {
  font-size: 1.2em;
}
```

**Not recommended**
```scss
// Using nesting is better but not in all cases
// Avoid nesting when there is no attributes and use selector chains instead
.content {
  display: block;

  > .news-article {
    > .title {
      font-size: 1.2em;
    }
  }
}
```

**Recommended**
```scss
// This example takes the best approach while nesting but use selector chains where possible
.content {
  display: block;

  > .news-article > .title {
    font-size: 1.2em;
  }
}
```

***

### Introducing space while nesting (SCSS)(嵌套中引入 空行 (SCSS))

If you nest your selectors introduce blank line between your nested selectors and the css attributes.

嵌套选择器和CSS属性之间空一行。

**Not recommended**
```scss
.content {
  display: block;
  > .news-article {
    background-color: #eee;
    > .title {
      font-size: 1.2em;
    }
    > .article-footnote {
      font-size: 0.8em;
    }
  }
}
```

**Recommended**
```scss
.content {
  display: block;

  > .news-article {
    background-color: #eee;

    > .title {
      font-size: 1.2em;
    }

    > .article-footnote {
      font-size: 0.8em;
    }
  }
}
```

***

### Contextual media queries (SCSS)(上下文媒体查询(SCSS))

While nesting your selectors you can also make use of contextual media queries within Sass. With Sass you can use media
queries at any given nesting level. The resulting CSS will be converted so that the media query gets rendered around the
selector.

This technique is very handy and helps to keep media queries in the context where they belong to. With a mobile first
approach this allows you to write your mobile styles first and then use contextual media queries where ever you need
them in order to provide the desktop styles.

在Sass中，当你嵌套你的选择器时也可以使用上下文媒体查询。
在Sass中，你可以在任何给定的嵌套层次中使用媒体查询。
由此生成的CSS将被转换，这样的媒体查询将包裹选择器的形式呈现。

这技术非常方便，
有助于保持媒体查询属于的上下文。

第一种方法这可以让你先写你的手机样式，然后在任何你需要的地方
用上下文媒体查询以提供桌面样式。

**Not recommended**
```scss
// This mobile first example looks like plain CSS where the whole structure of SCSS is repeated
// on the bottom in a media query. This is error prone and makes maintenance harder as it's not so easy to relate
// the content in the media query to the content in the upper part (mobile style)

.content-page {
  font-size: 1.2rem;

  > .main {
    background-color: whitesmoke;

    > .latest-news {
      padding: 1rem;

      > .news-article {
        padding: 1rem;

        > .title {
          font-size: 2rem;
        }
      }
    }

    > .content {
      margin-top: 2rem;
      padding: 1rem;
    }
  }

  > .page-footer {
    margin-top: 2rem;
    font-size: 1rem;
  }
}

@media screen and (min-width: 641px) {
  .content-page {
    font-size: 1rem;

    > .main > .latest-news > .news-article > .title {
      font-size: 3rem;
    }

    > .page-footer {
      font-size: 0.8rem;
    }
  }
}
```

**Recommended**
```scss
// This is the same example as above but here we use contextual media queries in order to put the different styles
// for different media into the right context.

.content-page {
  font-size: 1.2rem;

  @media screen and (min-width: 641px) {
    font-size: 1rem;
  }

  > .main {
    background-color: whitesmoke;

    > .latest-news {
      padding: 1rem;

      > .news-article {
        padding: 1rem;

        > .title {
          font-size: 2rem;

          @media screen and (min-width: 641px) {
            font-size: 3rem;
          }
        }
      }
    }

    > .content {
      margin-top: 2rem;
      padding: 1rem;
    }
  }

  > .page-footer {
    margin-top: 2rem;
    font-size: 1rem;

    @media screen and (min-width: 641px) {
      font-size: 0.8rem;
    }
  }
}
```

***

### Nesting order and the parent selector (SCSS)(嵌套顺序和父级选择器(SCSS))

While using the nesting features of Sass it's important to have a clear order to put your nesting in. A SCSS block
should have the following content order.

1.  Current selector's style attributes
1.  Pseudo selectors with parent selector (:first-letter, :hover, :active etc)
1.  Pseudo elements (:before and :after)
1.  State classe with parent selector (.selected, .active, .enlarged etc.)
1.  Contextual media queries with Sass
1.  Sub selectors as the last part

当使用Sass的嵌套功能的时候，重要的是有一个明确的嵌套顺序，以下内容是一个SCSS块应具有的顺序。

1. 当前选择器的样式属性
2. 父级选择器的伪类选择器 (:first-letter, :hover, :active etc)
3. 伪类元素 (:before and :after)
4. 父级选择器的声明样式 (.selected, .active, .enlarged etc.)
5. 用Sass的上下文媒体查询
6. 子选择器作为最后的部分


The following example should illustrate how this ordering will achieve a clear structure while making use of the Sass
parent selector.

下面的例子将会阐述，当使用 Sass parent 选择器会获得  这样的顺序 清晰的结构 

**Recommended**
```scss
.product-teaser {
  // 1. Style attributes
  display: inline-block;
  padding: 1rem;
  background-color: whitesmoke;
  color: grey;

  // 2. Pseudo selectors with parent selector
  &:hover {
    color: black;
  }

  // 3. Pseudo elements with parent selector
  &:before {
    content: "";
    display: block;
    border-top: 1px solid grey;
  }

  &:after {
    content: "";
    display: block;
    border-top: 1px solid grey;
  }

  // 4. State classes with parent selector
  &.active {
    background-color: pink;
    color: red;

    // 4.2. Pseuso selector in state class selector
    &:hover {
      color: darkred;
    }
  }

  // 5. Contextual media queries
  @media screen and (max-width: 640px) {
    display: block;
    font-size: 2em;
  }

  // 6. Sub selectors
  > .content > .title {
    font-size: 1.2em;
git 
    // 6.5. Contextual media queries in sub selector
    @media screen and (max-width: 640px) {
      letter-spacing: 0.2em;
      text-transform: uppercase;
    }
  }
}
```

