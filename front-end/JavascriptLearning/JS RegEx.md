# JavaScript Regular Expression
***

### 元字符(meta character)
- `\b\`: 单词的开头和结尾；
- `.`: 匹配除了换行符以外的任意字符
- `^`: 匹配字符串的开始(^\d{5,12}&)
- `$`: 匹配字符串的结束
- `*`: 表示数量,*前面的内容可以连续重复使用任意次,可以为0次
- `+`: 表示数量,匹配最少一次
- `{2}`：连续匹配2次
- `\d`: 匹配一位数字
- `\s`: 匹配任意的空白符(空格,制表符,换行符,中文全角空格)
- `\w`: 匹配字母或数字或下划线或汉字

### 转义字符: \
	- `\.`:
	- `\*`:
	- `\\`:

### 重复:
	- `*`: 重复零次或更多次
	- `+`: 重复一次或更多次
	- `?`: 重复零次或一次
	- `{n,}`: 重复n次或更多次
	- `{n,m}`: 重复n到m次

### 字符类:
	- `[a,e,i,o,u]`: 匹配任何一个英文元音字母
	- `[.?!]`: 匹配标点符号(.或?或!)
	- `[0-9]`: \d
	- `[a-z0-9A-Z]`: \w
	- `\(?0\d{2}[) -]?\d{9}`: (010)88886666 022-22334455 02912345678

### 分支条件:
	-
	-
	-
	-

