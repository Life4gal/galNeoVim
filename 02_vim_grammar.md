### tips: 

###### 如果没有在命令上加上 `# xxxxx`表示例外，则该命令默认是`快捷键`命令

## Vim语言只有一种语法规则：verb + noun

### Nouns (Motions)

```bash
h		# 向左
j		# 向下
k		# 向上
l		# 向右
w		# 直到下一个单词开头
}		# 直到下一段落(paragraph)
$		# 直到该行结尾
```

### Verbs (Operators)

```bash
y		# 拷贝(yank, copy)
d		# 剪切(delete)
c		# 剪切并进入`插入模式`(change)
```

### Verb And Noun

```bash
y$		# 拷贝从当前位置至行尾之间的全部内容
dw		# 剪切从当前位置到下一个单词开头之间的内容
c}		# 剪切从当前位置到下一个段落开头之间的内容并进入插入模式

y2h		# 拷贝左边两个字符
d2w		# 删除接下来两个单词
c2j		# 改变接下来两行

yy		# 拷贝一行
dd		# 删除一行
cc		# 改变一行
```

### More Nouns (Text Objects)

```bash
i + object		# 内部文本对象，不含有空白部分和括号包围
a + object		# 外部文本对象，含有空格和括号
```

```c++
#include <iostream>
int main()
{
	std::cout << "Hello World!" << std::endl;
	return 0;               
}
```

```bash
# 注意光标定位
di"		# 删除 Hello World!，不包括""
di{		# 删除{}内所有内容，不包括{}
diw		# 删除 Hello，不包括后面的空格

da"		# 删除 Hello World!，包括""
da{		# 删除{}内所有内容，包括{}
daw		# 删除 Hello，包括后面的空格

# w -> word, p -> paragraph, s -> sentence, h还有一些括号以及成对符号都可以组合
```

