#JS 常用函数总结

*日常代码编写中使用到的一些基本函数*

- 对数组进行操作:
	- join(separator): 将数组各个元素是通过指定的分隔符进行连接成为一个字符串。其作用和toString()相同
		- 将数组中的所有元素转为一个字符串
		- separator为空则默认用逗号分隔数组元素
	- slice():md 从已有的数组中返回选定的元素
		- arrayObject.slice(start,end(不包括))
        - 返回一个新的数组
		- 负值从数组的尾部选取元素,如果end未被规定，那么 slice() 方法会选取从 start 到数组结尾的所有元素。
    - splice(index): 用于插入、删除或替换数组的元素
        + 返回值: 若从arrayObject中删除了元素，则返回的是含有被删除的元素的数组。
        + splice()方法与slice()方法不同，会直接对数组进行修改
- 对字符串进行操作:
	- split(separator):
    - 
