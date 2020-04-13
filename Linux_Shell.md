# Linux Shell学习

## 一、 Linux_Shell基础和使用

### 1.1   初识Linux_Shell  
#### 1.1.1  Shell在Linux环境里的角色

#### 1.1.2   与登陆Shell相关的文件
    /etc/profile
        系统级的初始化文件，定义了一些环境变量，由登陆 Shell 调用执行
        
    /etc/bash.bashrc  或   /etc/bashrc
        其文件名根据不同版本的Linux发行版而异，每个交互式Shell的系统级的启动脚本，定义了一些函数和别名
        
    /etc/bash.logout
        系统级的登陆 Shell 清理脚本，当登陆Shell推出时执行，部分Linux发行版默认没有此文件
        
    $HOME/.bash_profile  $HOME/.bash_login   #HOME/.profile
        用户个人初始化脚本，由登陆Shell时调用执行，这三个脚本只会执行一个，按照此顺序执行，第一个存在的将被执行
        
    $HOME/.bashrc
        用户个人的每个交互式Shell的启动脚本
    
    $HOME/.bash_logout
        用户个人的登陆 Shell 清理脚本，当登陆Shell推出时执行
    
    $HOME/.inputrc
        用户个人的由readline使用的启动脚本，定义了处理某些情况下的键盘映射


#### 1.1.3  Shell中的变量



#### 1.1.4  Shell环境进阶



### 1.2  常用Shell命令  

##### 1.2.1  ls使用 查看文件和目录

    ls (-l):
        共7个字段   -rw-r--r-- 1 zx zx 8980 3月  26 22:26 examples.desktop
        字段1：文件权限。 9个字符
        字段2：链接数
        字段3：所有者
        字段4：用户组
        字段5：文件大小
        字段6：文件最近一次被修改的日期时间
        字段7：文件名
    
    ls -lh
    ls -F：
        使用不同的特殊符号归类不同的文件类型。
        /  表示目录
        无特殊字符  表示普通文件
        @  表示链接文件
        *  表示可执行文件
    
    ls -R：
        将递归地列出子目录的内容
    
    ls -ltr:
        以长列表格式按文件或目录的修改时间倒序地列出文件和目录
    
    ls -a:
        列出包括隐藏文件
    
    ls -i:
        显示文件或目录的 inode 编号
    
    ls -n:
        显示uid和gid,代替显示所有者和租户
    

##### 1.2.2  cat使用  连接显示文件内容
    语法： 1、  cat [option] [file1] ...
          2、  cat   (没有参数,接受标准输入的内容，并显示到标准输出上，也可以重定向： cat > test)
                    可以利用这个特性将多个文件写入一个文件, 推出时按住  CTRL + D
                          
    cat -n file:
        显示文件内容的行号
    
    cat -b file:
        显示非空白行的行号
        
    cat -e file:
        将在每一行结尾显示 “$”字符,  在多行转换成一行时可以用到


​    
##### 1.2.3  less、more    分屏显示文件



### 1.3  Shell命令进阶

#### 1.3.1  文件处理和归档

|命令           |作用|
|---------------|----|
|paster         | 合并文件|
|dd             | 备份和拷贝|
|gzip、bzip     | 压缩和归档文件|
|gunzip、bunzip | 解压缩文件|
|tar            | 打包和解包文件|

##### 1.3.1.1  paster : 合并文件


##### 1.3.1.2  dd : 备份和拷贝


##### 1.3.1.3  gzip、bzip ： 压缩和归档文件


##### 1.3.1.4  gunzip、bunzip : 解压缩文件


##### 1.3.1.5  tar ： 打包和解包文件


#### 1.3.2  检测和管理磁盘

|命令           |作用|
|---------------|----|
|mount、umount | 挂载和卸载存储介质|
|df            | 报告文件系统磁盘空间利用率|
|du            | 评估文件系统利用率|

##### 1.3.2.1  mount、umount : 挂载和卸载存储介质

##### 1.3.2.2  df : 报告文件系统磁盘空间利用率

##### 1.3.2.3  du : 评估文件系统利用率



#### 1.3.3  后台执行命令

|命令           |作用|
|---------------|----|
|cron、crontab | 执行计划任务|
|at | 在指定时间执行命令|
|& |控制操作符,将任务放在后台运行|
|nohub | 运行一个对挂起免疫的命令|

##### 1.3.3.1  cron、crontab : 执行计划任务

##### 1.3.3.2  at : 在指定时间执行命令


##### 1.3.3.3  & ：控制操作符,将任务放在后台运行

##### 1.3.3.4  nohub ： 运行一个对挂起免疫的命令





## 二、 Shell脚本编程

### 2.1  Shell编程基础  
pattern: 模式
parameter: 参数

#### 2.1.1  Shell 脚本第一行 #!
    脚本中的 #！ 行(第一行) 用于指示一个解释文件

#### 2.1.2  Shell 中的注释

    # 是注释标识符
        除了 $#
    
    还可以利用 Bash 的HERE DOCUMENT特性添加多行注释


#### 2.1.3  设置脚本权限和执行脚本
    添加权限：
        chmod u+x ./test.sh
        chmod +x ./test.sh     给所有用户权限 
    
    运行脚本：
        绝对路径：
        相对路径：

#### 2.1.4  Shell变量进阶

##### Bash 中的参数扩展

    1、基本的参数扩展：
        $parameter
        ${parameter}
    
    2、间接参数扩展：
        ${!parameter}
            被引用的不是 pattern 参数本身， 而是 pattern 的值
    
    3、变量名扩展：
        列出所有 PARAM 开头的变量名， 默认用空格分割
        ${!PARAM*}
        ${!PARAM@}
    
    4、字符串移除：
        用指定的模式描述 从 参数值字符串中 移除
            #：从开头匹配指定的模式
            %：从结尾匹配指定的模式     
        ${parameter#pattern}
        ${parameter##pattern}
        ${parameter%pattern}
        ${parameter%%pattern}
        
        常用：
            1、移除文件名，保留后缀
            2、移除后缀，保留文件名
            3、移除文件名，保留目录
            4、移除目录，保留文件名
    
    5、字符串搜索与替换：
        ${parameter/pattern/string}    # 匹配替换一次
        ${parameter//pattern/string}   # 匹配替换全部
        ${parameter/pattern}           # 替换为空字符(即删除)
        ${parameter//pattern}
    
    6、求字符串长度：
        ${#parameter}
    
    7、子字符串扩展：
        扩展参数值的一部分。 从指定位置开始截取到 参数尾部/指定长度字符(截取某个长度字符串) 
        ${parameter:offset}
        ${parameter:offset:length}
        
        使用默认值：
            ${parameter:-WORD}  # a、parameter未定义或者为NULL时，这种模式会扩展WORD，否则扩展参数parameter
            ${parameter-WORD}   # b、parameter 未定义时才会使用WORD
        指定默认值：
            与使用默认值类似,区别在于 这种模式不仅扩展 WORD，还会将WORD 赋值给参数
            ${parameter:=WORD}  #
            ${parameter=WORD}   # 
        使用替代值：
            # parameter未定义或者为NULL时，这种模式不会扩展任何内容，  若参数parameter已定义且不为空，只扩展WORD
            ${parameter:+WORD}  #
            ${parameter+WORD}   # 
            
    8、参数扩展：



|大小写修改：    |  结果           |
|--------------|-----------------|
|$test_ABC     | 原字母|
|${test_ABC^}  | 第一个字符改为大写|
|${test_ABC^^} |    所有为大写|
|${test_ABC,}  | 第一个字符改为小写|
|${test_ABC,,} |    所有为小写|
|${test_ABC~}  | 第一个字符改为相反|
|${test_ABC~~} |    所有为相反|

已定义的变量，可以被重新定义，如：
复制代码 代码如下:

your_name="tom"
echo $your_name

your_name="alibaba"
echo $your_name

##### Bash的内部变量
    Bash 的内部变量会影响 Bash 脚本的行为。
    
    1、 $BASH : 用于引用Bash实例的全路经名
    2、 $HOME : 当前用户的 home 目录， 通常是 /home/zx
    3、 $IFS  : ISF是内部分隔符的缩写。 此变量决定当 Bash 解析字符串时将怎么识别字段，或单词分界线
                变量 $ISF 的默认值是空格(空格、制表符、换行)，但可以被修改
    4、 $OSTYPE : 擦作系统类型
    5、 $SECONDS : 脚本以运行的秒数 
                 
    6、 $TMOUT : 如果非0，则为超时的秒数
                设置命令等待时间长度
    7、 $UID : 当前用户的账号表示码， 与 /etc/passwd记录相同
                判断当前账号是否为 root


##### Bash 中的位置参数和特殊参数
    位置参数： Bash 中的位置参数是由 除0 以外的一个或多个数字表示的参数。
        位置参数是当Shell或Shell的函数 被引用时 由 Shell或Shell函数的参数赋值，并且可以使用Bash的内部命令set来重新赋值。
        注意： 多余一个数字的位置参数必须放在大括号中
        位置参数不能通过赋值语句来赋值，只能通过 Bash 内部命令 set 和 shift 来设置和取消它们
    
    特殊参数： Bash对一些参数的处理比较特殊。 这些参数只能被引用，但不能修改它们的值

|特殊参数 |作用|举例|
|----|----|----|
| *  | 将扩展为从1开始的所有位置参数  |  |
| @  | 将扩展为从1开始的所有位置参数  |  |
| ?  | 将扩展为最近一个在前台执行的命令的退出状态| 检查Shell脚本是否成功执行，成功返回0 |
| -  | 将扩展为当前的选项标志|  |
| $  | 将扩展为当前Shell的进程号|  |
| !  | 将扩展为最近一次执行的后台命令的进程号|  |
| 0  | 将扩展为Shell或Shell脚本的名字|  |
| _  | 在Shell启动时，它被设置为开始运行的Shell或Shell脚本的路径|  |



##### 使用 declare 指定变量的类型
    declare 是Bash 的内部命令，用于声明变量和修改变量的属性。
    declare 与 另一Bash内部变量 typeset 的用法完全一样
    
    1、declare :
        直接使用declare命令 (没有指定变量),显示所有变量的值
    2、declare -r :
        把指定的变量指定为只读变量， 这些变量将不能再被赋予新值或被清除
    3、declare -i :
        把指定的变量定义为整数型变量，赋予整数型变量的任何值都会被转换为整数
    4、declare -x :
        把指定的变量通过环境输出到后续命令
    5、declare -p :
        显示指定变量的属性和值        

nohup command [ARG] ... $
    让运行的命令或脚本在退出系统后继续在后台运行
    

    command : Shell脚本或者命令的名称
    [ARG] : 脚本或命令的参数
    $ : nohup 命令不能自动的将人物放在后台运行， 必须明确的在 nohup 命令的末尾添加操作控制符 $



##### Bash 中的数组变量
    一个数组是包含多个值的变量。
    任何变量也可以作为一个数组使用。
    数组的大小没有限制，也不需要成员变量是连续分配的  数组下标从0 开始
    
    声明一个数组变量的语法：
        间接声明：
            array_name[index]=value
                index：是一个正数， 或值为正数的算术表达式
        显示声明：
            数组的属性可以使用 Bash 的内部命令 declare 和 readonly 指定，这些属性被应用到所有的数组变量中
            declare -a array_name
                例如： declare -a linux=('Debian' 'Redhat' 'Suse' ...)
        复合赋值：
            array_name=(value1 value2 value3 .....)        
    
    使用数组变量：
        必须使用花括号 {}
        如果 索引是 {@} 或 {*} , 则表示数组的所有成员将被引用
        
        如果不加索引，默认为使用数组的第一个元素
        
        可以使用 unset 清除一个 数组 或 数组成员变量
            array_name{3}  # 删除索引为3的变量
            array_name{@}  # 删除数组


##### Shell 算术运算符
    Shell可以对算术表达式求值
        1、 Shell 算术扩展
        2、 内部命令 let 

###### Bash 的算术运算符
    操作符优先级分组：
|操作符   |  用途     |
|-----------------|-------|
| id++  id--      | 变量 后递增/递减      |
| ++id  --id      | 变量 前递增/递减         |
| -+             |  单目 正号/负号        |
| !~             |  逻辑取反 按位取反        |
| **           | 求幂         |
| */%          | 乘 除 求余         |
| +-           | 双目 加/减         |
| << >>        | 按位左移/按位右移         |
| <= >= < >     | 比较        |
| == !=         | 相等/不相等       |
| $             | 按位与      |
| ^             | 按位异或       |
| \| |          |
| &&             |          |
|              |          |
| expr? expr: expr  | 条件运算符          |
|              | 赋值         |
| expr1,expr2  | 逗号运算          |

###### 数字常量
    默认情况下，Shell算术表达式用的都是十进制数，除非数字有特殊开头
        0x/0X : 十六进制
        0 ： 八进制


​        
######　使用算数扩展和　let 进行算数运算
    1、 算数扩展--- 只能是整数
        $(算数表达式)
        
    2、 let运算符
        let命令按照从左到右顺序讲提供给它的每一个参数进行算术表达式的求值。(分开了要加双引号)
        let i=i+5
        let "i = i + 5"


###### 使用expr命令
    用于对表达式进行求值并输出相应结果的命令行工具 (同时，只支持整数运算)  (表达式两边必须分开)
    expr 6 + 8

  







​    


##### 退出脚本
    exit N ： 命令语句 用于从Shell脚本中退出并返回指定的退出状态码N，来表示 Shell脚本是否成功结束 (0:表示成功)
              如果省略 N， 则返回最后一条语句的退出状态

##### 调试脚本
    1、 运行命令时 加参数 -x
        bash -x test.sh
    
    2、 Shell脚本里     调试一段代码或全部代码
        set -x
        .....
        .....
        (set +x)


    3、 运行时参数 -v 或者 -vx
        bash -vx test.sh


​    




### 2.2  Shell的条件执行  


#### 2.2.1、 条件测试

##### 2.2.1.1test 命令
    可用于：
        1、 文件属性测试
        2、 字符串测试
        3、 算术测试
    
    语法：
        test expressio


文件属性测试操作符表：

|  操作符 |  描述 &#60;file&#62; |
|----|----|
| -e &#60;file&#62;   | 如果 file 存在, 则为真 |
| -f &#60;file&#62;   | 如果 file 存在, 且是一个常规文件, 则为真 |
| -d &#60;file&#62;  | 如果 file 存在, 且是一个目录, 则为真 |
| -c &#60;file&#62;   | 如果 file 存在, 且是一个特殊字符文件, 则为真 |
| -b &#60;file&#62;   | 如果 file 存在, 且是一个特殊块文件, 则为真 |
| -p &#60;file&#62;   | 如果 file 存在, 且是一个命令管道, 则为真 |
| -S &#60;file&#62;   | 如果 file 存在, 且是一个套接字文件, 则为真|
| -L &#60;file&#62;  | 如果 file 存在, 且是一个符号链接, 则为真 |
| -h &#60;file&#62;   | 如果 file 存在, 且是一个符号链接, 则为真 |
| -g &#60;file&#62;   | 如果 file 存在, 且设置了sgid位, 则为真 |
| -u &#60;file&#62;   | 如果 file 存在, 且设置了ugid位, 则为真 |
| -r &#60;file&#62;   | 如果 file 存在, 且可读的, 则为真 |
| -w &#60;file&#62;  | 如果 file 存在, 且可写的, 则为真|
| -x &#60;file&#62;  | 如果 file 存在, 且可执行的, 则为真|
| -s &#60;file&#62;  | 如果 file 存在, 且不为空, 则为真 |
| -t &#60;fd&#62;     | 如果 文件描述符 &#60;fd&#62; 已经打开了,并且引用了一个终端, 则为真 |
| &#60;file1&#62; -nt &#60;file2&#62;  | 如果 &#60;file1&#62; 比 &#60;file2&#62;新, 则为真 |
| &#60;file1&#62; -ot &#60;file2&#62;  | 如果 &#60;file1&#62; 比 &#60;file2&#62;旧, 则为真 |
| &#60;file1&#62; -ef &#60;file2&#62;  | 如果 &#60;file1&#62; 有硬链接到 &#60;file2&#62;新, 则为真 |



字符串测试操作符表：

| 操作符  | 描述  |
|---|---|
| -z &#60;string&#62;  |如果 &#60;string&#62; 为空, 则为真  |
| -n &#60;string&#62;  |如果 &#60;string&#62; 不为空, 则为真  |
| &#60;string1&#62; = &#60;string2&#62;  |如果 &#60;string1&#62; 与 &#60;string2&#62; 相同, 则为真  |
| &#60;string1&#62; != &#60;string2&#62;  |如果 &#60;string1&#62; 与 &#60;string2&#62; 不相同, 则为真  |
| &#60;string1&#62; < &#60;string2&#62;  |如果 &#60;string1&#62; 的字典排序在 &#60;string2&#62; 之前, 则为真 (ASCII码顺序) |
| &#60;string1&#62; > &#60;string2&#62;  |如果 &#60;string1&#62; 的字典排序在 &#60;string2&#62; 之后, 则为真 (ASCII码顺序)|


算数测试操作符：

| 操作符  | 描述  |
|---|---|
| &#60;int1&#62; -eq &#60;int2&#62;  |如果 &#60;int1&#62; 与 &#60;int2&#62; 相等, 则为真  |
| &#60;int1&#62; -ne &#60;int2&#62;  |如果 &#60;int1&#62; 与 &#60;int2&#62; 不相等, 则为真  |
| &#60;int1&#62; -le &#60;int2&#62;  |如果 &#60;int1&#62; 小于或等于 &#60;int2&#62; 相等, 则为真  |
| &#60;int1&#62; -ge &#60;int2&#62;  |如果 &#60;int1&#62; 大于或等于 &#60;int2&#62; 相等, 则为真  |
| &#60;int1&#62; -lt &#60;int2&#62;  |如果 &#60;int1&#62; 小于 &#60;int2&#62; 相等, 则为真  |
| &#60;int1&#62; -gt &#60;int2&#62;  |如果 &#60;int1&#62; 大于 &#60;int2&#62; 相等, 则为真  |



##### 2.2.1.2  if 结构的语法格式     
```shell
# (注意: 中括号[] 里面需要左右空一格)  

if test-commands; then
    test-1
elif test-com
    test
else
    test-2
fi
```

##### 2.2.1.3  条件执行

    在Bash下，你可以把最后一个命令的退出状态当做条件 使用条件执行来连接两个命令。
        1、 逻辑与 &&  
            前一个命令执行成功时才能执行后面的命令
        2、 逻辑或 ||
            前一个命令执行失败时才能执行后面的命令


```bash
# 语法：
#     1、 commands1 && commands2
#     2、 commands1 || commands2
    
# 实例:
    if [ -n $var ] && [ -e $var ]; then
    
    if [[ -n $var && -e $var ]]; then
```


​        
​    逻辑非：
​        !



##### 2.2.1.4  case 语句



### 2.3  Bash循环  

#### 2.3.1  for 循环
```bash
# for 循环语法：
#     in : 后面可以是  字符串、数字、命令行参数、文件名、Linux命令的输出 
    
    # 1、 基本语法
        for var in itme1 itme2 ... itmeN; do
            command1
            .....
        done
    
    # 2、 循环变量
        for var in $file_names; do
            command1
            .....
        done
    
    # 3、 循环命令替换
        for var in $(Linux-commands-name); do
        或：
        for var in "Linux-commands-name"; do
        
        done
    
    # 4、 三项表达式
        for var in ((exp1; exp2; exp3;)); do
            commands
        done
        注释：
            exp1：初始化式
            exp2：循环条件
            exp3: 计算表达式   

# 嵌套for循环：
```


​        
#### 2.3.2  while 循环
    重复的执行一个命令列表   条件为真，继续循环
    
    while 语法：
        while [condition]; do
            commands
        done
        
    无限循环：
        1、
            while : do       
        
        2、
            while true; do
            
    while + read : 读取文件


​       
#### 2.3.3  until 循环
```shell
#条件为假时， 继续循环

# until 语法：
until [condition]
   commands
done
```

#### 2.3.4  select 循环

```bash
# select 语法：
select var in List; do
   commands
done

# select 特点：
```


#### 2.3.5  循环控制
    1、 break语句
        break 语法：
            break [n]
            n 代表嵌套循环层数，如果指定了 n, break讲退出 n 级嵌套循环
                             如果没有指定n, 或者 n <=1, 则退出状态码为 0, 否则为 n
        
    2、continue语句
        跳过循环体中剩余的命令, 直接跳转到循环体的 顶部.
        
        continue 可用于 for、while、until循环
        
        continue语法：
            continue [n]    





### 2.4  Shell函数  

    定义：
        Shell 函数是 Shell脚本中由命令集和语句组成的代码块，这个代码块可以被其它脚本或脚本中其它部分所调用。
        
    任务：
        1、 定义一个函数
        2、 函数传参、处理参数
        3、 函数中的变量(范围、作用域)
        4、 函数的返回
        5、 函数的调用
        6、 后台运行函数或其它应用


#### 2.4.1、 函数的定义
    方法a：
        # 函数名
        function_name()
        {
            # 函数体
            commands.....
        
            # 参数返回  
            [return n]
            return语句是可选的。
            1、 没有return ： 返回函数最后一条命令的结果
            2、 有return   : 返回 n (0~255)      
        }
    
    方法b:
        加上 function 关键字：
        function function_name()
        {
            commands.....
        }
    
    方法c:
        在一行内定义
        function function_name() { command1; command2; ... }


​    
可以使用 unset 的 -f命令来取消函数的定义


#### 2.4.2、 函数变量、参数、返回值

###### 2.4.2.1、 像函数传递参数
    Shell函数有自己的命令行参数。
    函数使用特殊变量 $1 $2 $3 .... $n 来访问传递给它的参数
        $0 : 代指脚本的名字
        $* 或 $@ : 保存传递给函数的所有参数
        $# : 保存传递给函数的位置参数个数

```shell script
name(){
arg1=$1
arg2=$2
command on $arg1
}

name foo bar
```

###### 2.4.2.2、 本地变量
    默认情况下，脚本中所有的变量都是全局的。
    
    local 命令：
        只能在函数内部使用
        讲变量名的可见范围限制在函数内部


###### 2.4.2.3、 return
    特殊参数：$?
        可以得到最近一次执行命令的退出状态
```shell script
# 调用函数 checkpid
checkpid $pid1 $pid2 $pid3

# 如果上述命令执行成功， 则 $? = 0
if [ $? = 0 ]; then
  echo "OK"
else 
  echo "Error"
fi
```




#### 2.4.3、 函数的调用
    1、 Shell命令调用函数
    2、 脚本中调用函数
    3、 从函数文件中调用函数
    4、 递归调用函数



#### 2.4.4、 讲函数放在后台运行
    $ 操作符:
        可以将命令放在后台运行并释放你的终端

```shell script
# 定义函数 name
name()
{
  echo "Do something"
  sleep 1
}

# 将函数放在后台运行
name $

# 继续执行其它命令
# .........
```


### 2.5  正则表达式  
### 2.6  脚本输入处理  


#### 2.6.1、 参数处理

    1、 使用 case 语句处理命令行参数
    2、 使用 shift 命令处理命令行参数
    3、 使用 for 循环读取多个参数
    4、 读取脚本名
    5、 测试命令行参数


#### 2.6.2、 选项处理
    1、 使用 case 语句处理命令行选项
    2、 使用 getopts 处理多命令选项
    3、 使用 getopt 处理多命令行选项


#### 2.6.3、 获得用户输入
    1、 基本读取
        read [-p prompt] [value1 vlaue2 ...]
    
    2、 输入超时
    3、 隐藏方式读取
    4、 从文件中读取


​    

### 2.7  Shell重定向

    定义：
        改变输入或输出的默认路径

#### 2.7.1、 输入和输出
    Linux中一切皆文件， 所以硬件在Linux中也表示为文件
    
    文件描述符：
        0：
            标准输入, 键盘  -- 从文件(默认是键盘) 读取输入
        1：
            标准输出, 屏幕  -- 发生数据到文件(默认是屏幕)
        2：
            标准错误, 屏幕  -- 发生所有错误信息到一个文件(默认是文件)


##### 2.7.1.1、 标准输入

标准输入特点：

- 默认的输入方式，被所有命令使用 来读取输入
- 用数字 0 表示
- 被称为 stdin
- 默认标准输入设备是 键盘

  
    操作符 " < " 是输入重定向操作符
    语法：
        commands  < input_filename

##### 2.7.1.2、 标准输出

标准输出特点：

- 被命令用来写入或显示命令自身的输出
- 用数字 1 表示
- 被称为 stdout
- 默认标准输入设备是 屏幕


    操作符 " > " 是输出重定向操作符
    语法：
        commands > output_filename


##### 2.7.1.3、 标准错误

标准输出特点：

- 被命令用来写入或显示命令自身的输出
- 用数字 2 表示
- 被称为 stderr
- 默认标准输入设备是 屏幕


    操作符 " 2> " 是输出重定向操作符
    语法：
        commands 2> output_filename


### 2.8  管道和过滤器
#### 2.8.1  管道
    定义：
        将两个或多个程序连接到一起，使得一个程序的输出变成另一个程序的输入，以这种方式链接到一起的程序形成了管道
    
    语法：
        command1 | command2 {| command3 ....}


​    
##### 2.8.1.1  操作符 "|" 和 ">"  之间的去区别
    1、 由管道符 "|" 执行的重定向      讲第一个命令的输出作为第二个命令的输入
        command1 | command2
    
    2、 由重定向 ">" 执行的重定向      将命令与文件连接
        command1 > file1





#### 2.8.2  过滤器

    定义：
        一个Linux命令从标准输入接受它的输入数据，并在标准输出上产生它的输出数据，这样的命令被称为 过滤器

##### 2.8.2.1  常被用作过滤器使用的命令如下：
|命令   | 作用  |
|------|---|
|awk   |用于文本处理的解释性程序设计语言，常被用作数据的提取和报告的工具   |
|cut   |用于将每个输入文件(没有指定则默认为标准输入)的每行的指定部分输出到标准输出|
|grep  |用于搜索一个或多个文件中匹配指定模式的行|
|tar   |用于归档文件的应用程序|
|head  |用于读取文件的开头部分(默认是10行，如果没有指定文件，默认为标准输入读取)|
|paste |用于合并文件的行|
|sed   |用于过滤和转换文本的流编辑器|
|sort  |用于对文件进行排序|
|split |用于讲文件分割成块|
|strings|用于打印文件中可打印的字符串|
|tac   |与cat命令相反，用于倒序显示文件或者连接文件|
|tail  |用于显示文件的结尾部分|
|tee   |用于从标准输入读取内容并写到标准输出和文件|
|tr    |用于转换或删除字符|
|uniq  |用于报告或忽略重复的行|
|wc    |用于打印文件中的总行数、单词数或字节数|


### 2.9  捕获

#### 2.9.1  信号

##### 2.9.1.1  Linux中的信号
    定义：
        在Linux系统中，信号被用于进程间通信。
        信号是发送到某个进程或同一进程的特定线程的异步通知，用于通知发生的一个事件


    进程接收到信号，可能会发生以下 3 种情况：
        1、 进程可能会忽略此信号
        2、 进程可能会捕获此信号，并执行一个信号处理器的特殊函数
        3、 进程可能执行信号的默认行为
            例如： 信号15 表示结束进程
    
    当一个进程执行信号处理时，如果还有其它信号到达，那么新的信号会被阻断，知道处理器返回为止

##### 2.9.1.2  信号的名称和变量
每个信号都有以 "SIG" 开头的名称，并定义为唯一的正整数
    
    查看所有信号值和对应的信号名：
        kill -l
    
    信号值被定义在文件 /usr/XXX 
    源文件在
    
    可是使用 man 7 signal   查看

```shell script
# zx@zx:~$ kill -l
 1) SIGHUP	 2) SIGINT	 3) SIGQUIT	 4) SIGILL	 5) SIGTRAP
 6) SIGABRT	 7) SIGBUS	 8) SIGFPE	 9) SIGKILL	10) SIGUSR1
11) SIGSEGV	12) SIGUSR2	13) SIGPIPE	14) SIGALRM	15) SIGTERM
16) SIGSTKFLT	17) SIGCHLD	18) SIGCONT	19) SIGSTOP	20) SIGTSTP
21) SIGTTIN	22) SIGTTOU	23) SIGURG	24) SIGXCPU	25) SIGXFSZ
26) SIGVTALRM	27) SIGPROF	28) SIGWINCH	29) SIGIO	30) SIGPWR
31) SIGSYS	34) SIGRTMIN	35) SIGRTMIN+1	36) SIGRTMIN+2	37) SIGRTMIN+3
38) SIGRTMIN+4	39) SIGRTMIN+5	40) SIGRTMIN+6	41) SIGRTMIN+7	42) SIGRTMIN+8
43) SIGRTMIN+9	44) SIGRTMIN+10	45) SIGRTMIN+11	46) SIGRTMIN+12	47) SIGRTMIN+13
48) SIGRTMIN+14	49) SIGRTMIN+15	50) SIGRTMAX-14	51) SIGRTMAX-13	52) SIGRTMAX-12
53) SIGRTMAX-11	54) SIGRTMAX-10	55) SIGRTMAX-9	56) SIGRTMAX-8	57) SIGRTMAX-7
58) SIGRTMAX-6	59) SIGRTMAX-5	60) SIGRTMAX-4	61) SIGRTMAX-3	62) SIGRTMAX-2
63) SIGRTMAX-1	64) SIGRTMAX	
```


POSIX标准信号表：



##### 2.9.1.3  Bash中的信号



#### 2.9.2  进程
    概念：
    
    前台进程：
    后台进程：

##### 2.9.2.1  进程状态：
|状态缩写   |含义   |
|---|---|
|D (不可中断休眠状态)   |进程正在休眠并且不能恢复，直到一个事件发生为止   |
|R (运行状态)   |进程正在运行   |
|S (休眠状态) |进程没有在运行，在等待一个事件或信号   |
|T (停止状态) |进程被信号停止   |
|Z (僵死状态) |标记为 <defunct>的进程是僵死的进程，他们之所以残留，是应为父进程适当的销毁它们，如果父进程退出，这些进程将被 init进程销毁   |

##### 2.9.2.2  查看进程方法：

    ps:
        查看当前进程(默认只会显示当前用户并且是当前终端Shell)下调用的进程信息
        例如：
            ps 
            ps -ef   (显示系统中的每一个进程)
            ps -aux  (显示系统中的每一个进程)
        
    pstree：
        显示进程树的信息，以树形结构显示当前系统中运行的所有进程信息
        
    pgrep：
        基于名称或其它属性查找进程
        例如：
            查看root用户的sshd进程的PID
            pgrep -u root sshd

##### 2.9.2.3  向进程发送信号
    可以使用键盘、pkill、kill、killall命令向进程发生各种信号
    
    1、键盘
    
    2、pkill
    3、kill
    4、killall


#### 2.9.3  子进程

#### 2.9.4  捕获
    trap语句：
        在Shell脚本内捕获特定的信号并对它们进程处理
    语法：
        trap command signal {signal ....}
        command: 一个脚本或者函数
        signal: 可以是信号名或者信号值
        
        如果不使用任何参数，直接 trap命令， 会打印每个要捕获的信号相关联的命令的列表
    
    当Shell收到信号signal时，command将被读取和执行



每次调整终端窗口大小的时候都会被捕捉，然后执行 while里的    
```shell script
#!/bin/bash 

echo "Adjust the size of your windows now"

trap "echo windows size changed." SIGWINCH

COUNT=0

while [ $COUNT -lt 30 ]; do
    COUNT=$(( COUNT + 1))
    sleep 1
done

```

Bash中有两个内部变量： LINEND 和 BASH_COMMAND
    可以方便的在处理信号时，为我们提供更多的与脚本相关的信息
```shell script
#!/bin/bash 

# 捕获 SIGHUP、SIGINT 和 SIGQUIT信号， 如果捕获到这些信号，将会执行 my_exit 后退出
trap 'my_exit $LINENO $BASH_COMMAND; exit' SIGHUP SIGINT SIGQUIT

# 函数 my_exit
function my_exit()
{
   # 打印脚本名称、信号以及被捕获时 运行的命令和行号
   echo "$(basename "$0")  caught error on line : $1 command was : $2"

   # 导出为日志
   echo "script: $(basename "$0") was terminated: line: $1, command was $2" > test.log

   # 其它一些清理命令
}


# 执行无限循环
while true; do
    sleep 1
    count=$(( count + 1 ))
    echo $count
done
```

移除捕获
```shell script
#!/bin/bash 
set -ex

# 定义函数 clearup
function clearup()
{
  # 如果变量 msgfile所指的文件存在
  if [[ -e $msgfile ]]; then
    # 将此文件重命名或者移除
    mv "$msgfile" "$msgfile".dead
  fi

  # 退出
  exit
}

# 捕获 INT和TERM信号
trap clearup INT TERM

# 创建一个临时文件(执行Linux命令)
msgfile=$(mktemp /tmp/test_trap.$$.XXXXX)
# 通过命令向此临时文件写入
cat test.sh > "$msgfile"

# 删除临时文件
rm "$msgfile"

# 移除信号 INT 和 TERM 的捕获
trap - INT TERM

```
输出：
```shell script
zx@zx:~$ bash test.sh 
+ trap clearup INT TERM
++ mktemp /tmp/test_trap.7458.XXXXX
+ msgfile=/tmp/test_trap.7458.0WeXM
+ cat test.sh
+ rm /tmp/test_trap.7458.0WeXM
+ trap - INT TERM

```


### 2.10  sed/awk
    sed 和 awk 都是处理文本的有力工具
    
    相同点：
        1、 使用相同的语法调用
        2、 都是面向字符流的，都是从文本文件中每一行读取输入，并将输出直接送到标准输出端
        3、 都使用正则表达式进行模式匹配
        4、 都允许用户将命令放在文件中一起执行



#### 2.10.1  sed 编辑器基础
    sed 是用来解析和转换文本的工具， 它使用简单，是简洁的程序设计语言

##### 2.10.1.1  sed简介
    sed 是非交互式的面向数据流的编辑器
    
    可使用 sed 做如下操作：
        1、 自动化的编程一个或多个文件
        2、 简化在多个文件中执行相同编辑的任务
        3、 编写转换程序

##### 2.10.1.2  sed的模式空间
    sed 维护一种模式空间， 即一个工作区域或临时缓冲区。 当使用编辑命令时，将在那里存储单个输入行
    
    注意：
        sed 一次处理一行输入的优点是 在读取非常庞大的文件时不会出现问题。
        一般的文件编辑器必须将整个文件读入内存，这将产生内存溢出或者在处理庞大文件时速度非常慢
    
##### 2.10.3  基本的sed编辑命令
    sed 命令语法：
        1、 sed [options]... `command` [file]...
        2、 sed [options] -f scriptfile [file]...
    
    sed 有如下常用选项：
        -e :
            它告诉 sed 将下一个参数解释为 sed指令。 只有命令行上给出多个sed指令时才需要使用 -e 选项
        -f :
            指定由sed指令组成的脚本名称。
        -i :
            直接修改已读的内容，而不是输出到终端
        -n :
            取消默认输出。 
            在一般sed用法中，所有来自标准输入的数据都会显示到终端上， 但是加上 -n 后，只有经过sed处理过的行才会被显示  
           
##### 2.10.4  sed 实例

```shell script
# 假设我们有一文件名为  ab

# 增
#   “a”:追加文本到指定行后，记忆方法：a的全拼是apend，意思是追加。
#   “i“：插入文本到指定行前，记忆方法：i的全拼是insert，意思是插入

sed '1a drink tea' ab    # 第一行后增加字符串"drink tea"
sed '$a drink tea' ab    # 最后一行后增加字符串"drink tea"
sed '1,3a drink tea' ab  # 第一行到第三行后增加字符串"drink tea"
sed '1a drink tea\nor coffee' ab   # 第一行后增加多行，使用换行符\n

# 删  “d”:删除文本，记忆方法：d的全拼是delete，意思是删除。
sed '1d' ab              # 删除第一行 
sed '$d' ab              # 删除最后一行
sed '1,2d' ab            # 删除第一行到第二行
sed '2,$d' ab            # 删除第二行到最后一行
sed '2,3!d' ab           # 取反  删除2 3行以外的行

# 改 “c”：用新行取代旧行，记忆方法：c的全拼是change，意思是替换
sed '1c Hi' ab           # 第一行代替为Hi
sed '1,2c Hi' ab         # 第一行到第二行代替为Hi

# 查 “p”：输出指定内容，但默认会输出2次匹配的结果，因此使用-n选项取消默认输出，记忆方法：p的全拼是print，意思是打印
sed '1,3p' ab            # 复制1，3行(会重复)
sed -n '1,3p' ab         # 打印出1.3复制的内容
sed -n '/ninth/p' ab     # 匹配 ninth 的行

# 替换一行中的某部分      格式：　sed 's/要替换的字符串/新的字符串/g'   （要替换的字符串可以用正则表达式）
sed -n '/ruby/p' ab | sed 's/ruby/bird/g'    #　替换ruby为bird
sed -n '/ruby/p' ab | sed 's/ruby//g'        #　删除ruby


# 显示某行
sed -n '1p' ab           # 显示第一行 
sed -n '$p' ab           # 显示最后一行
sed -n '1,2p' ab         # 显示第一行到第二行
sed -n '2,$p' ab         # 显示第二行到最后一行

# 使用模式进行查询
sed -n '/ruby/p' ab      # 查询包括关键字ruby所在所有行
sed -n '/\$/p' ab        # 查询包括关键字$所在所有行，使用反斜线\屏蔽特殊含义

# 多点编辑
sed -e '/^#/d' -e '/^$/d' test  # 去除文件中的注释行和空白行

# 插入
sed -i '$a bye' ab         # 在文件ab中最后一行直接输入"bye"

# 删除匹配行
sed -i '/匹配字符串/d'  filename  # (注：若匹配字符串是变量，则需要“”，而不是‘’。记得好像是)

# 替换匹配行中的某个字符串
sed -i '/匹配字符串/s/替换源字符串/替换目标字符串/g' filename
```


####  2.10.2  awk 基础

##### 2.10.2.1  awk 简介
    awk 被设计用于文本处理，并通常被用作数据提取和报告工具的解释性程序设计语言
    
    awk 具有的功能：
        1、 使用变量操作由文本记录和字段组成的文本文件
        2、 具有普通的程序设计结构，例如循环 和条件
        3、 生成格式化报告
        4、 定义函数
        5、 从 awk 脚本中执行Linux命令
        6、 处理Linux命令的结果
        7、 更加巧妙的处理命令行的参数
        8、 更容易处理多个输入流

##### 2.10.2.2  awk 基本语法
    awk '{pattern + action}' {filenames}
    
    1、 截取文件中某一段
        -F： 选项的作用是指定分隔符，如果不加-F指定，则以空格或者tab为分隔符。 print为打印的动作，用来打印出某个字段。$1为第一个字段，$2为第二个字段，依次类推，有一个特殊的那就是$0，它表示整行。
            awk -F ':' '{print $1}' /etc/passwd
        注意awk的格式，-F后紧跟单引号，然后里面为分隔符，print的动作要用 { } 括起来，否则会报错。print还可以打印自定义的内容，但是自定义的内容要用双引号括起来。
    2、 匹配功能
        awk可以跟sed一样的用法用于匹配，awk '/root/' /etc/passwd
        也可搭配截取某段的功能用于匹配特殊字段中的关键字，awk -F ':' '$1~/root/' /etc/passwd,此处‘~‘表示匹配，
                                                   awk -F ':' '/root/ {print $1} /test/ {print $1}' /etc/passwd     awk可以多次匹配，如上例中匹配完root，再匹配test，并只打印所匹配的段。
    3、 条件操作符
        awk中是可以用逻辑符号判断的，比如 ‘==’ 就是等于，也可以理解为 ‘精确匹配’ 另外也有 >, ‘>=, ‘<, ‘<=, ‘!= 等等，
        值得注意的是，在和数字比较时，若把比较的数字用双引号引起来后，那么awk不会认为是数字，而认为是字符，不加双引号则认为是数字。
        awk -F ':' '$3=="501"' /etc/passwd;awk -F ':' '$3!="501"' /etc/passwd



























































## 三、 使用注意
```shell script
# 创建临时文件

# 不推荐方法
msgfile1=`mktemp /tmp/test_trap.$$.XXXXX`

# 推荐方法
msgfile2=$(mktemp /tmp/test_trap.$$.XXXXX)
```


变量加双引号以防止全局搜索和分词
"$abcd"


