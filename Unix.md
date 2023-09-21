### Unix


#### awk

> https://en.wikipedia.org/wiki/AWK

注：单引号内为awk脚本语法，双引号为字符串

- -F "n"：按n分割字符串，不加时默认以空格分割

```shell script
# ripen.txt
123-abc test1
456-fgh test2

awk -F "-" '{print $1}' ripen.txt
# 输出：
# 123
# 456

awk -F "-" '{print $1,$2}' ripen.txt
# 输出：(abc test1是一个完整字符串，并非两个)
# 123 abc test1
# 456 ghj test2

awk -F "-" '$1 > 124 {print $1,$2}' ripen.txt
# 输出
# 456 ghj test2

# 匹配以123为开头的
awk -F "-" '/^123/ {print $1,$2}' ripen1.txt
# 输出：
# 123 abc test1
```

```shell script
awk 'BEGIN {print sqrt(625)}'           # 输出625的平方根：25
awk 'BEGIN {print atan2(0, -1)*100}'    # 输出：314.159
```

```shell script
# ripen.awk文件
awk -F "-" '{print $1}' $1

# 添加执行权限
chmod +x ripen.awk

# 执行
./ripen.awk ripen.txt
# 输出：
# 123
# 456
```



拓展：

- nawk：BWK awk
- gawk：GNU awk
- ...



#### tr

> https://www.geeksforgeeks.org/tr-command-in-unix-linux-with-examples/

tr [OPTION] SET1 [SET2]

处理包括大写到小写、压缩重复字符、删除特定字符以及基本的查找和替换等

```shell script
# 小写转大写
tr [a-z] [A-Z] 或 tr [:lower:] [:upper:]

# 空字符（包括换行符）替换成tab
tr [:space:] "\t"

# {}替换成()
tr "{}" "()"      # {abc} -》 (abc)

# 压缩字符
tr -s " "         # "a  b   c"-》"a b c"

# 删除字符
tr -d w           # "while"-》"hile"
tr -d [:digit:]   # 删除所有数字
tr -cd [:digit:]  # 删除所有非数字
```



#### 字符组

> https://en.wikipedia.org/wiki/Regular_expression#Character_classes

|                         Description                          | 描述 |    POSIX     | Perl/Tcl |   Vim   |        Java         |                ASCII                 |
| :----------------------------------------------------------: | :--: | :----------: | :------: | :-----: | :-----------------: | :----------------------------------: |
|                       ASCII characters                       |   ASCII 字符   |              |          |         |     `\p{ASCII}`     |            `[\x00-\x7F]`             |
|                   Alphanumeric characters                    | 字母数字字符 | `[:alnum:]`  |          |         |     `\p{Alnum}`     |            `[A-Za-z0-9]`             |
|               Alphanumeric characters plus "_"               | 字母数字字符加“_” |              |   `\w`   |  `\w`   |        `\w`         |            `[A-Za-z0-9_]`            |
|                     Non-word characters                      | 非单词字符 |              |   `\W`   |  `\W`   |        `\W`         |           `[^A-Za-z0-9_]`            |
|                    Alphabetic characters                     | 字母字符 | `[:alpha:]`  |          |  `\a`   |     `\p{Alpha}`     |              `[A-Za-z]`              |
|                        Space and tab                         | 空格和制表符 | `[:blank:]`  |          |  `\s`   |     `\p{Blank}`     |               `[ \t]`                |
|                       Word boundaries                        | 单词边界 |              |   `\b`   | `\< \>` |        `\b`         |    `(?<=\W)(?=\w)|(?<=\w)(?=\W)`     |
|                     Non-word boundaries                      | 非单词边界 |              |          |         |        `\B`         |    `(?<=\W)(?=\W)|(?<=\w)(?=\w)`     |
| [Control characters](https://en.wikipedia.org/wiki/Control_character) | 控制字符 | `[:cntrl:]`  |          |         |     `\p{Cntrl}`     |          `[\x00-\x1F\x7F]`           |
|                            Digits                            | 数字 | `[:digit:]`  |   `\d`   |  `\d`   | `\p{Digit}` or `\d` |               `[0-9]`                |
|                      Hexadecimal digits                      | 十六进制数字 | `[:xdigit:]` |          |  `\x`   |    `\p{XDigit}`     |            `[A-Fa-f0-9]`             |
|                          Non-digits                          | 非数字 |              |   `\D`   |  `\D`   |        `\D`         |               `[^0-9]`               |
|                      Visible characters                      | 可见字符 | `[:graph:]`  |          |         |     `\p{Graph}`     |            `[\x21-\x7E]`             |
|          Visible characters and the space character          | 可见字符和空格字符 | `[:print:]`  |          |  `\p`   |     `\p{Print}`     |            `[\x20-\x7E]`             |
|                    Punctuation characters                    | 标点符号 | `[:punct:]`  |          |         |     `\p{Punct}`     | `[][!"#$%&'()*+,./:;<=>?@\^_`{|
| [Whitespace characters](https://en.wikipedia.org/wiki/Whitespace_character) | 空白字符（包括换行符） | `[:space:]`  |   `\s`   |  `\_s`  | `\p{Space}` or `\s` |           `[ \t\r\n\v\f]`            |
|                  Non-whitespace characters                   | 非空白字符 |              |   `\S`   |  `\S`   |        `\S`         |           `[^ \t\r\n\v\f]`           |
|                      Lowercase letters                       | 小写字母 | `[:lower:]`  |          |  `\l`   |     `\p{Lower}`     |               `[a-z]`                |
|                      Uppercase letters                       | 大写字母 | `[:upper:]`  |          |  `\u`   |     `\p{Upper}`     |               `[A-Z]`                |



#### tee

> https://phoenixnap.com/kb/linux-tee

[command] | tee [options] [filename] [filename2]...

```shell script
# 覆盖文件内容
echo "hello" | tee ripen.txt

# 文件末尾追加内容
echo "hello" | tee -a ripen.txt

# 上一个命令被中断后也能正确退出
ping www.baidu.com | tee -i ripen.txt
```



