### Shell

> https://www.learnshell.org/



- $#：表示执行脚本传入参数的个数
- $@：表示执行脚本传入参数的所有个数（不包括$0），即把每个参数当成独立整体
- $*：表示执行脚本传入参数的列表（不包括$0），即把所有参数当成一个整体
- $0：表示执行的脚本名称
- $1：表示第一个参数；$2：表示第二个参数；...
- $?：表示脚本执行的状态，0表示正常，其他表示错误
- $$：表示进程的id；Shell本身的PID（ProcessID，即脚本运行的当前 进程ID号）
- $!：Shell最后运行的后台Process的PID(后台运行的最后一个进程的 进程ID号)




#### 运算符

```shell script
add=$((1+2)))     # 3
sub=$((2-1))      # 1
mult=$((2*2))     # 4
divide=$((4/2))   # 2
modulo=$((5%2))   # 1
power=$((2**3))   # 8
```



#### 字符串

```shell script
str="this is a is string"
subStr="hat"
expr index "$str" "$subStr"     # 1；str中第一个与subStr相匹配的字符下标，下标从1开始

echo ${#str}                    # 19；str长度，空格算1
echo ${str:2:4}                 # is i；截取str下标2~4
echo ${str:1}                   # his is a is string；截取str从下标1到尾的字符

echo ${str[@]/is/ab}            # thab is a is string；替换第一个is字符串为ab
echo ${str[@]//is/ab}           # thad ab a ab string；替换所有is字符串为ab

echo ${str[@]/ is/}             # this a is string；删除第一个is字符串（连续）
echo ${str[@]// is/}            # this a string；删除所有is字符串（连续）

echo ${str[@]/#his/dc}          # this is a is string；字符串开头的his替换为dc
echo ${str[@]/#this/dc}         # dc is a is string

echo ${str[@]/%in/on}           # this is a is string；字符串结尾的in替换为on
echo ${str[@]/%ing/ong}         # this is a is strong
```



#### 数组

```shell script
new_array=(apple tea cat)
other_array[1]=1
echo ${new_array[2]}
# 输出数组数量
echo ${#new_array[@]}
echo ${other_array[1]}
echo ${other_array[2]}
```



#### if

```shell script
NAME="George"
if [ "$NAME" = "John" ]; then
  echo "John Lennon"
elif [ "$NAME" = "George" ]; then
  echo "George Harrison"
else
  echo "This leaves us with Paul and Ringo"
fi

if [[ $VAR_A[0] -eq 1 && ($VAR_B = "bee" || $VAR_T = "tee") ]] ; then
    command...
fi
```



#### 比较

```shell script
$a -lt $b    $a < $b
$a -gt $b    $a > $b
$a -le $b    $a <= $b
$a -ge $b    $a >= $b
$a -eq $b    $a is equal to $b
$a -ne $b    $a is not equal to $b
```

```shell script
"$a" = "$b"     $a is the same as $b
"$a" == "$b"    $a is the same as $b
"$a" != "$b"    $a is different from $b
-z "$a"         $a is empty
```

```shell script
case "$variable" in
    "$condition1" )
        command...
    ;;
    "$condition2" )
        command...
    ;;
esac

myCase=1
case $myCase in
    1) echo "You selected bash";;
    2) echo "You selected perl";;
    3) echo "You selected phyton";;
    4) echo "You selected c++";;
    5) exit
esac
```



#### 循环

##### for

```shell script
for arg in [list]
do
 command(s)...
done
```

```shell script
# 输出每个元素
NAMES=(Joe Jenny Sara Tony)
for N in ${NAMES[@]} ; do
  echo "My name is $N"
done

# 输出目录下级的所有文件及文件夹
for f in $( ls /etc ) ; do
  echo "File is: $f"
done
```


##### while

```shell script
while [ condition ]
do
 command(s)...
done

支持break continue
```

```shell script
COUNT=4
while [ $COUNT -gt 0 ]; do
  echo "Value of count is: $COUNT"
  COUNT=$(($COUNT - 1))
done
```

##### until(与while相反)

```shell script
until [ condition ]
do
 command(s)...
done

支持break continue
```

```shell script
COUNT=1
until [ $COUNT -gt 5 ]; do
  echo "Value of count is: $COUNT"
  COUNT=$(($COUNT + 1))
done
```



#### trap

trap <arg/function> <signal>

> http://mywiki.wooledge.org/SignalTrap



#### 常见

```shell script
# -e 判断文件是否存在
filename="ripen.sh"
if [ -e "$filename" ]; then
   echo "$filename exist"
else
   echo "$filename not exist"
fi

# -d 判断文件夹是否存在
# -r 判断用户是否有 执行 文件权限
# -w 判断用户是否有 写入 文件权限
```


