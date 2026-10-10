# Makefile

## 规则的三个组成部分

- 目标
- 依赖
- 命令

> make 会根据时间戳决定是否生成目标，以提升效率
> make 只执行第一条 rule，依赖找不到才向下执行

```makefile
# makefile

# rule1
target1: depend1, depend2, ...
        ...
# rule2
target2: dependa, dependb, ...
        ...
# rule3
target3:
        echo "target3"
```

如果要直接执行某条规则: `make target2`

## 变量

### 自定义变量

```makefile
# 定义变量
x = 123
# 取变量
$(x)
```

### 预定义变量

| 变量       | 含义           | 默认值      |
| -------- | ------------ | -------- |
| AR       | 生成静态库的程序     | ar       |
| ARFLAGS  | 生成静态库的程序的选项  | 无        |
| AS       | 汇编器的名称       | as       |
| ASFLAGS  | 汇编器的编译选项     | 无        |
| CC       | C语言编译器       | gcc      |
| CFLAGS   | C语言编译器编译选项   | 无        |
| CXX      | C++语言编译器     | g++      |
| CXXFLAGS | C++语言编译器编译选项 | 无        |
| CPP      | C语言预编译器      | $(CC) -E |
| RM       | 删除           | rm -f    |

应用案例：

```makefile
# makefile
target=app
obj=test1.o test2.o
CFLAGS=-O3
$(target):$(obj)
        $(CC) $(obj) -o $(target) $(CFLAGS)
```

### 自动变量

> 自动变量只能在规则中的命令中使用

| 变量  | 含义                          |
| --- | --------------------------- |
| $*  | 表示目标文件的名称，不含扩展名             |
| $@  | 表示目标文件的名称，含扩展名              |
| $+  | 表示所有的依赖，以空格分开，按照出现的先后顺序，不去重 |
| $^  | 表示所有的依赖，以空格分开，去重            |
| $<  | 表示依赖项中的第一个依赖的名称             |
| $?  | 表示依赖项中，所有比目标文件时间戳晚的依赖，以空格分开 |

## 模式匹配

```makefile
# 通过一个公式，代表若干个满足条件的规则
.o:.c
    $(CC) -c $(CFLAGS) $(CPPFLAGS)

# %是通配符
%.o:%.c
    gcc $< -c
```

## 函数

> 所有函数都有返回值

```makefile
# wildcard
# 搜索当前目录下 C 源文件
src = $(wildcard *.c)
# 搜索两个目录下的 C 源文件
src = $(wildcard a/*.c b/*.c *.c)

# patsubst
# 把变量 src 中所有文件的后缀从 c 替换为 o
obj = $(patsubst %.c, %.o, $(src))
```

## 伪目标

```makefile
# PHONY
# 如果项目刚好有一个文件叫 clean，需要声明 clean 为伪目标
.PHONY: clean
clean:
    rm $(obj) $(target)

# 如果规则中的一个命令执行失败了，脚本不会继续执行
# 如果要继续执行，在命令前加上 “-”
clean:
    -mkdir /test
    rm $(obj) $(target)
```
