#jQuery 选择器
*jQuery 元素选择器和属性选择器允许您通过标签名、属性名或内容对 HTML 元素进行选择*
***

###1.1 jQuery 元素选择器
 * `$(this)`
 * `$('p')`
 * `$(ul li:first)`
 * `$('p.className')`
 * `$('p#idName')`

###1.2 jQuery 属性选择器
 * `$("[href='#']")`
 * `$("[href!='#']")`
 * `$("[href$='.jpg']")`
 * `$("input[name="inputName"][type="radio"]:checked")`

###1.3 jQuery CSS选择器
 * `$('p').css("background-color","red");`

###1.4 jQuery 模糊匹配
 * 完全匹配:`[attr = value]`
 * 模糊匹配:`[attr* = value]`
 * 不能为这个值:`[attr != value ]`
 * 结尾为此值:`[attr $= value]`
 * 开头为此值:`[attr ^=value]`
 * 匹配多个条件中的一个:`[attr1][attr2]`

