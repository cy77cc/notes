# **Go语言**

## 基础知识

go build指令将go源码文件编译成可执行文件(.exe)

go run指令直接执行go文件

两种执行流程的方式区别

1. 如果我们先编译成了可执行文件，那么我们可以将可执行文件拷贝到没有go开发环境的机器上，仍然可运行

  2. 如果我们直接go run go源码，那么如果要在另外一个机器上可以运行，也需要go开发环境，否则无法执行
  3. 在编译时，编译器会将程序运行依赖的库文件包含在可执行文件中，所以，可执行文件变大了很多

指定生成可执行文件的名称

```go
go build -o myHello.exe hello.go   指定生成的可执行文件名为myHello
```

如果程序没有错误，没有任何提示

如果程序有错，编译时，会在错误的那行报错

## 常见转义字符

| escape char | 表示的意思                                           |
| ----------- | ---------------------------------------------------- |
| \t          | 一个制表符，实现对齐的功能                           |
| \n          | 换行符                                               |
| \\\         | 一个\                                                |
| \"          | 一个"                                                |
| \r          | 一个回车，从当前行的最前面开始输出，覆盖掉以前的内容 |

gofmt -w main.go该指令可以将格式化后的内容重写到文件

go test -v 测试

一行最多80个字符

```go
package main   包名必须的 
import "fmt"    引入这个包 这个包实现输入输出 i/o流 
func main() {     
    main函数 最先执行的函数 如果有init()函数就先执行init()   
    fmt.Println("hello world") 换行输出    
    fmt.Print("hello world")  不换行输出 
} 
```

go语言结尾不需要分号 如果多条语句写在同一行就要使用分号分隔

## 进制

对于整数，有四种表示方式

1. 二进制：0，1，满2进1

    ​	在Golang，不能直接使用二进制来表示一个整数

2. 十进制：0-9，满10进1

3. 八进制：0-7，满8进1，以数字0开头表示

4. 十六进制：0-9和A-F，满16进1，以0x开头

    ​	A-F不区分大小写，0x也不区分大小写

### 进制的转换

 1. 其他进制转十进制

  2. 二进制转十进制

     ​	每一位乘以2的(n - 1)次方

     ```
     二进制数101
     1 * 2的二次方 + 0 * 2的一次方 + 1 * 2的零次方
     ```

  3. 八进制转十进制

     ​	每一位乘以8的(n - 1)次方

     ```
     八进制数101
     1 * 8的二次方 + 0 * 8的一次方 + 1 * 8的零次方
     ```

  4. 十六进制转十进制

     ​	每一位乘以16的(n - 1)次方

     ```
     十六进制数101
     1 * 16的二次方 + 0 * 16的一次方 + 1 * 16的零次方
     ```

  5. 十进制转其他进制

         1. 十进制转二进制

     ​	将该数不断除以2，直到商为0为止，然后将每步得到的余数倒过来，就是对应的二进制

     2. 十进制转八进制

     ​	将该数不断除以8，直到商为0为止，然后将每步得到的余数倒过来，就是对应的二进制

     3. 十进制转十六进制

     ​	将该数不断除以16，直到商为0为止，然后将每步得到的余数倒过来，就是对应的二进制

  6. 二进制转其他进制

         1. 二进制转八进制

     将二进制数的每三位为一组(从低位开始组合)，转成对应的八进制数即可

     ```
     二进制数11010101
     11 010 101 对应的数是 3 2 5
     所以对应的八进制数是 0325
     ```

     2. 二进制转十六进制

     将二进制数的每四位为一组(从低位开始组合)，转成对应的十六进制数即可

     ```
     二进制数11010101
     1101 0101 对应的数是 D 5
     所以对应的八进制数是 0xD5
     ```

  7. 二进制转其他进制

       1. 八进制转二进制

     将八进制数的每1位，转成一个对应的3位的二进制数即可

     2. 十六进制转二进制

     将十六进制数的每1位，转成一个对应的4位的二进制数即可

 8. 十进制小数和二进制小数互转

        1. 十进制转二进制

              ```
              0.125 * 2 = 0.25   0
              0.25 * 2 = 0.5     0
              0.5 * 2 = 1        1
              所以0.125转换成二进制为0.001
              ```

        2. 二进制转十进制

              每一位一次乘以2的n次方

              ```
              0.001
              第一位 0 * 2 的 -1 次方
              第二位 0 * 2 的 -2 次方
              第三位 0 * 2 的 -3 次方
              ```

### 原码，反码，补码

对于有符号的而言

 1. 二进制的最高位是符号位：0表示正数，1表示负数

    ```go
    1 的二进制表示 0000 0001 		
    -1 的二进制表示 1000 0001
    ```

 2. 正数的原码，反码，补码都一样

 3. 负数的反码=它的原码符号位不变，其他位取反(1 -> 0, 0 -> 1)

    ```
    1 的原码 0000 0001 反码 0000 0001 补码 0000 0001
    -1 的原码 1000 0001 反码 1111 1110 补码 1111 1111
    ```

 4. 负数的补码=它的反码+1

 5. 0的反码，补码都是0

 6. 在计算机运算的时候，都是以补码的形式来运行的

## **关键字**

下面列举了 Go 代码中会使用到的 25 个关键字或保留字：

| break    | default     | func   | interface | select |
| -------- | ----------- | ------ | --------- | ------ |
| case     | defer       | go     | map       | struct |
| chan     | else        | goto   | package   | switch |
| const    | fallthrough | if     | range     | type   |
| continue | for         | import | return    | var    |

除了以上介绍的这些关键字，Go 语言还有 36 个预定义标识符：

| append | bool    | byte    | cap     | close  | complex | complex64 | complex128 | uint16  |
| ------ | ------- | ------- | ------- | ------ | ------- | --------- | ---------- | ------- |
| copy   | false   | float32 | float64 | imag   | int     | int8      | int16      | uint32  |
| int32  | int64   | iota    | len     | make   | new     | nil       | panic      | uint64  |
| print  | println | real    | recover | string | true    | uint      | uint8      | uintptr |

## **变量  **

### 变量的使用步骤

1. 声明变量
2. 赋值
3. 使用

### 变量使用的注意事项

1. 变量表示该内存中的一个存储区域

2. 该区域有自己的名称（变量名）和类型（数据类型）

3. Golang变量声明使用的三种方式

    3.1. 第一种 指定变量类型 声明后若不赋值则使用默认值

```go
var 变量名 变量类型 var a int = 10   默认值0 
```

​		3.2. 第二种 不指定声明的变量类型 会根据值判断变量类型

```go
var 变量名 = 值 var b = 10 
```

​		3.3. 第三种 省略var使用 :=声明变量不能是已存在的变量   只能在函数体内用

```go
c := 10
```

4. 多变量声明

```go
var a, b, c int 
var a, b, c = 1, 2, 3 
d, e, f := 1, 2, 3 
声明多个不同类型的 
var () 在函数体外使用
var (    
    变量名1 变量类型    
    变量名2 变量类型   
    ... 
) 
```

5. 匿名变量

```go
i, _ := 10, 20   _ 就是匿名变量  丢弃数据不做处理  配合函数返回值使用才有优势 
```

### 同类型的值可以直接通过等号来交换值

```go
a1, b1 := 20, 30 
fmt.Printf("a1=%d,b2=%d\n", a1, b1) 
b1, a1 = a1, b1 同类型的直接等号交换值 
fmt.Printf("a1=%d,b2=%d\n", a1, b1) 输出 
交换前 
a1=20,b2=30 
交换后 
a1=30,b2=20 
```

## 变量的数据类型

![img](.\image\a761fb4452a4486599d36ab2ab731008.jpg)

![image-20200523210859064](C:\Users\48356\Desktop\笔记\image\image-20200523210859064.png)

### 整数类型

int和uint类型占的字节数大小跟操作系统位数有关

#### 整型的使用细节

​	1. Golang整型类型分为有符号和无符号，int、uint的大小和操作系统位数有关

​	2. Golang的默认整型是int

​	3. 查看一个变量的数据类型和占用字节大小

```go
fmt.Printf("%T", n)  // %T格式化输出变量的数据类型
fmt.Printf("n2 所占的字节数大小 %d", unsafe.Sizeof(n2))  
// unsafe包下的Sizeof可以返回变量所占字节大小
```

​	4. Golang程序中整型数据变量在使用时，遵守保小不保大的原则，即：在程序正确运行下，尽量使用占用空间小的数据类型

​	5. bit：计算机中的最小存储单位，byte：计算机中基本存储单元，1byte = 8bit

### 浮点型/小数类型

1. 基本介绍

    小数类型就是用于存放小数的，默认是float64

2. 小数类型分类

    单精度：float32	4个字节

    双精度：float64	8个字节

3. 浮点数在机器中的存放形式：浮点数 = 符号位 + 指数位 + 尾数位

    3.56

    11110000111.111111111111111111000

4. 尾数部分可能丢失，造成精度损失

5. 浮点数的存储分为三部分： 符号位 + 指数位 + 尾数位 在存储过程中，精度会有丢失

6. 0.几的小数可以省略0 例：0.12 可以写成 .12

7. 支持科学计数法：5.1234e2就是512.34 e2代表10的2次方， e可以大写也可以小写数字为负数就代表除

8. 通常情况下，应该使用float64，它比float32更精确

### 字符类型

1. Golang中没有专门的字符类型，如果要存储单个字符（字母），一般用byte来保存
2. 字符类型的直接输出，输出的是字符对应的ASCII值
3. 字符常量是用单引号括起来的单个字符
4. 允许使用转义字符 ’ \ ‘ 来将其后的字符转变成特殊字符型常量
5. Go语言的字符使用utf-8编码  英文字母1个字节，汉字3个字节
6. 在Go中，字符的本质是一个整数，直接输出时，是该字符对应的utf-8编码的码值
7. 可以直接给某个变量赋一个数字，然后按格式化输出是%c会输出该数字对应的Unicode字符
8. 字符类型是可以进行运算的，相当于一个整数，因为它都有对应的Unicode码

### 布尔类型bool

1. 布尔类型也叫bool类型，bool类型数据只允许取true或false
2. 布尔类型占1个字节
3. bool类型适于逻辑运算，一般用于程序流程控制

### 字符串类型string

1. 字符串就是一串固定长度的字符连接起来的字符序列。Go的字符串是有单个字节连接起来的

2. Golang的字符串一旦声明赋值，就不能再修改，在Go中字符串是不可变的

3. 字符串的两种表示形式

    1. 双引号会识别转义字符
    2. 反引号， 以字符串的原生形式输出，包括换行和特殊字符，可以实现防止攻击、输出源代码等效果

4. 字符串拼接方式

    1. 两个字符串相加

        ```go
        var str string = "Hello" + "World"
        ```

    2. 当一行字符串太长时，需要用到多行字符串，加号留在上面

        ```go
        var str string = "Hello" + "World" + 
        "Hello" + "World"
        ```

### 基本数据类型的转换

1. Go在不同类型的变量之间赋值是需要显式转换，没有自动类型转换

2. 基本语法 T(v) 将值 v 转换成类型 T 

    1. T：就是数据类型
    2. v：就是需要转换的变量

    ```go
    var i int = 10
    var f float64 = float64(i)
    ```

3. 被转换的数据本身的数据类型是不会改变的

4. 从数据范围大的转成数据范围小的时，会造成数据溢出

5. 进行赋值运算的时候等号两边的数据类型也要一致，否则会报错

### 基本数据类型和string的转换

1. 在程序开发中，我们经常需要将基本数据类型转成string类型，或string类型转成基本数据类型

2. 基本数据类型转string类型

    1. fmt.Sprintf("%参数", 表达式）

        ```go
        func Sprintf(format string, a ...interface{}) string
        Sprintf根据format参数生成格式化的字符串并返回该字符串。
        ```

        1. 参数需要和表达式的数据类型相匹配
        2. fmt.Sprintf() 会返回转换后的字符串

    2. 使用 strconv 包的函数

        ```go
        func FormatBool(b bool) string
        根据b的值返回"true"或"false"。
        
        func FormatInt(i int64, base int) string
        返回i的base进制的字符串表示。base 必须在2到36之间，结果中会使用小写字母'a'到'z'表示大于10的数字
        
        func FormatUint(i uint64, base int) string
        是FormatInt的无符号整数版本。
        
        func FormatFloat(f float64, fmt byte, prec, bitSize int) string
        函数将浮点数表示为字符串并返回。
        
        bitSize表示f的来源类型（32：float32、64：float64），会据此进行舍入。
        
        fmt表示格式：'f'（-ddd.dddd）、'b'（-ddddp±ddd，指数为二进制）、'e'（-d.dddde±dd，十进制指数）、'E'（-d.ddddE±dd，十进制指数）、'g'（指数很大时用'e'格式，否则'f'格式）、'G'（指数很大时用'E'格式，否则'f'格式）。
        
        prec控制精度（排除指数部分）：对'f'、'e'、'E'，它表示小数点后的数字个数；对'g'、'G'，它控制总的数字个数。如果prec 为-1，则代表使用最少数量的、但又必需的数字来表示f。
        
        func Itoa(i int) string
        Itoa是FormatInt(i, 10) 的简写
        ```

3. string类型转基本数据类型

    ```go
    func ParseBool(str string) (value bool, err error)
    返回字符串表示的bool值。它接受1、0、t、f、T、F、true、false、True、False、TRUE、FALSE；否则返回错误。
    
    func ParseInt(s string, base int, bitSize int) (i int64, err error)
    返回字符串表示的整数值，接受正负号。
    
    base指定进制（2到36），如果base为0，则会从字符串前置判断，"0x"是16进制，"0"是8进制，否则是10进制；
    
    bitSize指定结果必须能无溢出赋值的整数类型，0、8、16、32、64 分别代表 int、int8、int16、int32、int64；返回的err是*NumErr类型的，如果语法有误，err.Error = ErrSyntax；如果结果超出类型范围err.Error = ErrRange。
    
    func ParseUint(s string, base int, bitSize int) (n uint64, err error)
    ParseUint类似ParseInt但不接受正负号，用于无符号整型。
    
    func ParseFloat(s string, bitSize int) (f float64, err error)
    解析一个表示浮点数的字符串并返回其值。
    
    如果s合乎语法规则，函数会返回最为接近s表示值的一个浮点数（使用IEEE754规范舍入）。bitSize指定了期望的接收类型，32是float32（返回值可以不改变精确值的赋值给float32），64是float64；返回值err是*NumErr类型的，语法有误的，err.Error=ErrSyntax；结果超出表示范围的，返回值f为±Inf，err.Error= ErrRange。
    ```
    
4. string转基本数据类型的注意事项

    1. 在string类型转成基本数据类型时，要确保string类型能够转成有效的数据，比如我们可以把"123",转成一个整数，但是不能把"hello"转成一个整数，如果这样做，Golang直接将其转成0

## 指针

1. 基本数据类型，变量存的就是指，也叫值类型
2. 获取变量地址，用&，比如：var num int，获取num的地址：&num
3. 指针类型变量存的是一个地址，这个地址指向的空间才是值，比如：var ptr *int = &num
4. 获取指针类型所指向的值，使用：* 比如：var ptr \*int，使用\*ptr获取ptr指向的值

<img src="C:\Users\48356\Desktop\笔记\image\image-20200525175855704.png" alt="image-20200525175855704" style="zoom:50%;" /> 

​	指针变量存储的是一个地址值，其本身也有一个地址值

![image-20200525180115804](C:\Users\48356\Desktop\笔记\image\image-20200525180115804.png) 

5. 指针细节
    1. 值类型，都有对应的指针类型，形式为\*数据类型，比如int对应的指针就是\*int
    2. **值类型**包括：基本数据类型 **int系列**、**float系列**、**bool**、**string**、**数组**和**结构体struct**

## 值类型和引用类型

1. **值类型**：基本数据类型 **int系列**、**float系列**、**bool**、**string**、**数组**和**结构体struct**
2. **引用类型**：**指针**、**slice切片**、**map**、**管道chan**、**interface**、等都是引用类型 
3. 值类型：变量直接存储值，内存通常在栈中分配
4. 引用类型：变量存储的是一个地址，这个地址对应的空间才真正存储数据，内存通常在堆中分配，当没有任何变量引用这个地址时，该地址对应的数据空间就成为一个垃圾，用GC来回收

## 标识符的命名规则

### 标识符的概念

1. Golang对自己各种变量、方法等命名时使用的字符序列称为标识符
2. 凡是自己可以起名字的地方都叫标识符

### 标识符的命名规则

1. 由26个英文字母大小写，0-9，_ 组成
2. 不可以数字开头
3. Golang中严格区分大小写
4. 标识符不能包含空格
5. 下划线" _ "本身在Golang中是一个特殊的标识符，称为空标识符。可以代表任何其他空标识符，但是它对应的值会被忽略(比如，忽略某个返回值)，所以仅能作为占位符使用，不能作为标识符使用
6. 不能以系统保留关键字作为标识符，比如break，if等等

### 标识符命名注意事项

1. 包名：保持package的名字和目录保持一致，尽量采取有意义的包名，简短，有意义，不要和标准库命名冲突
2. 变量名、函数名、常量名，采用驼峰法
3. 如果变量名、函数名、常量名、首字母大写，则可以被其他包访问，如果首字母小写，则只能在本包中使用，（可以简单的理解成：首字母大写是公有的，首字母小写是私有的）

## **常量**

### 常量介绍

1. 常量使用const修饰
2. 常量在定义的时候必须初始化
3. 常量不能修改
4. 常量只能是bool，数值类型(int，float类型)，string类型
5. 语法：const name [type] = value
6. 仍然通过首字母的大小写来控制常量的访问范围

使用const关键字声明常量  变量名一般用大写

```go
const A int = 2   变量类型也可以不写 会根据值得类型来自动设置变量类型 
```

### iota常量自动生成器 枚举

​	1、iota常量自动生成器，每隔一行，自动累加1

​	2、iota给常量赋值用

​	3、iota遇到const重置为0

​	4、如果是同一行值都一样

```go
package main 
import "fmt" 
const (   
    a = iota   0   
    b = iota   1   
    c = iota   2 
) 
可以只写一个iota 
const (    
    a = iota    
    b    
    c 
) 
func main(){   
    fmt.Println(a, b, c)  
}
```

## 运算符

### 1. 算术运算符

| 运算符 | 运算         | 范例         | 结果    |
| :----- | :----------- | :----------- | :------ |
| +      | 正号         | +3           | 3       |
| -      | 负号         | -3           | -3      |
| +      | 加           | 5 + 5        | 10      |
| -      | 减           | 10 - 5       | 5       |
| *      | 乘           | 10 * 5       | 50      |
| /      | 除           | 10 / 3       | 3       |
| %      | 取模（求余） | 7 % 5        | 2       |
| ++     | 自增         | a = 2 a++    | a = 3   |
| --     | 自减         | a = 3 a--    | a = 2   |
| +      | 字符串相加   | "He" + "llo" | "Hello" |

除运算的时候只要有浮点数参与运算，那么输出的就是浮点数，否则都就是整数类型

```go
var num = 10 / 2 // num 是int类型的  值为 5
var num = 10.0 / 2 // num 是float64类型的   值为 5
var num = 10 / 2.0 // num 是float64类型的   值为 5
```

模运算的公式：a % b = a - a / b * b

#### 注意细节

	1. Golang的自增和自减只能当做一个独立语句使用，不能使用 b := a++

   	2. Golang的++ 和 -- 只能写在变量后面不能写在变量前面

### 2. 赋值运算符

下表列出了所有Go语言的赋值运算符。

| 运算符 | 描述                                           | 实例                                  |
| ------ | ---------------------------------------------- | ------------------------------------- |
| =      | 简单的赋值运算符，将一个表达式的值赋给一个左值 | C = A + B 将 A + B 表达式结果赋值给 C |
| +=     | 相加后再赋值                                   | C += A 等于 C = C + A                 |
| -=     | 相减后再赋值                                   | C -= A 等于 C = C - A                 |
| *=     | 相乘后再赋值                                   | C *= A 等于 C = C * A                 |
| /=     | 相除后再赋值                                   | C /= A 等于 C = C / A                 |
| %=     | 求余后再赋值                                   | C %= A 等于 C = C % A                 |
| <<=    | 左移后赋值                                     | C <<= 2 等于 C = C << 2               |
| >>=    | 右移后赋值                                     | C >>= 2 等于 C = C >> 2               |
| &=     | 按位与后赋值                                   | C &= 2 等于 C = C & 2                 |
| ^=     | 按位异或后赋值                                 | C ^= 2 等于 C = C ^ 2                 |
| \|=    | 按位或后赋值                                   | C \|= 2 等于 C = C \| 2               |

#### 赋值运算符的特点

1. 运算顺序从右往左

  2. 赋值运算符的左边只能是变量，右边可以是变量、表达式、常量值

交换两个变量的值，但是不可以使用中间变量

```go
var a int = 10
var b int = 20
a = a + b // a = 30
b = a - b // b = 10
a = a - b // a = 20
```

### 3. 关系运算符

1. 关系运算符的结果都是bool型，也就是要么true，要么是false

  2. 关系表达式，经常用在if结构的条件中或循环结构的条件中

| 运算符 | 运算     | 范例   | 结果  |
| ------ | -------- | ------ | ----- |
| ==     | 相等于   | 4 == 3 | false |
| !=     | 不等于   | 4 != 3 | true  |
| <      | 小于     | 4 < 3  | false |
| >      | 大于     | 4 > 3  | true  |
| <=     | 小于等于 | 4 <= 3 | false |
| \>=    | 大于等于 | 4 >= 3 | true  |

### 4. 逻辑运算符

1. 用于连接多个条件（一般就是关系表达式），最终结果也是一个bool值

假设 A 值为true B值为false

| 运算符 | 描述                                                         | 实例             |
| ------ | ------------------------------------------------------------ | ---------------- |
| &&     | 逻辑 与 运算。如果两边的操作都是true，则为true，否则为false  | (A && B)为false  |
| \|\|   | 逻辑 或 运算。如果两边的操作有一个为true，则为true，否则为false | (A \|\| B)为true |
| !      | 逻辑 非 运算。如果条件为true，则逻辑为false，否则为true      | !(A && B)为true  |

### 5. 位运算符

位运算符对整数在内存中的二进制位进行操作。

下表列出了位运算符 &, |, 和 ^ 的计算：

| p    | q    | p & q | p \| q | p ^ q |
| ---- | ---- | ----- | ------ | ----- |
| 0    | 0    | 0     | 0      | 0     |
| 0    | 1    | 0     | 1      | 1     |
| 1    | 1    | 1     | 1      | 0     |
| 1    | 0    | 0     | 1      | 1     |

&：两个都是1才是1 其他都是0

|：两个中有一个或两个是1则是1

^：两个都是1或0就是0 其他情况是 1

<<：左移运算符，符号位不变，低位补0

\>>：右移运算符，低位溢出，符号位不变，并用符号位补溢出的高位

### 6. 其他运算符

&：返回变量存储地址

*：指针变量

### 7. 运算符优先级

有些运算符拥有较高的优先级，二元运算符的运算方向均是从左至右。下表列出了所有运算符以及它们的优先级，由上至下代表优先级由高到低：

| 优先级 | 运算符        |
| ------ | ------------- |
| 7      | ^ !           |
| 6      | * / % <> & &^ |
| 5      | + - \| ^      |
| 4      | == != < = >   |
| 3      | <-            |
| 2      | &&            |
| 1      | \|\|          |

## **条件语句**

​	Go的 if，switch 还有一个强大的地方就是条件判断里面允许声明一个变量，这个变量的作用域该条件逻辑块内，其他地方就不起作用了

​	if 后面的条件加不加括号都没错，if的条件表达式不能是一个赋值语句

```go
单分支if
if 条件表达式 {    
    语句 
} 
if支持一个初始化语句 
if b := 2; b == 2 {
    语句 
}

双分支if
if 条件表达式 {    
    语句 
} else {    
    语句 
} 

多分支if
if 条件表达式 {    
    语句 
} else if 条件表达式{    
    语句 
} else {    
    语句 
} 

var b bool = true
if b = false {  // 这是错误的  可以写成 b = false; b 作为初始化语句
    fmt.Println("a")
} else {
    fmt.Println("b")
}
```

### switch语句

```go
switch语句
fallthrough
使用 fallthrough 会强制执行后面的 case 语句，fallthrough 不会判断下一条 case 的表达式结果是否为 true。
也支持一个初始化语句 
switch a := 1; a {} 
switch 值 {    
    case 值1:         
    value1        
    fallthrough    不会结束会继续执行下一个case语句    
    case 值2：        
    value2    
    case 值3, 值4, ......:  支持多条件匹配用逗号分隔        
    value3    default:     
    } 
还可以switch后面不放值 
score := 65 
switch {    
    case score > 90:        
    fmt.Println("优秀")    
    case score < 90:        
    fmt.Println("垃圾")     
} 
```

#### 注意细节

1. case/switch后是一个表达式（即：常量值，变量，一个有返回值的函数等都可以）

2. case后的各个表达式的值的数据类型，必须和switch的的表达式数据类型一致

3. case后面可以带多个表达式，使用逗号间隔。比如case 表达式1,表达式2

4. case后面的表达式如果是常量值(字面量)，则要求不能重复

5. case后面不需要带break，程序匹配到一个case后就会执行对应的代码块，然后退出switch，如果一个都匹配不到，则执行default

6. default不是必须的

7. switch后面也可以不带表达式，类似多个if-else分支来使用

8. switch后也可以直接声明/定义一个变量，分号结束，不推荐

9. switch穿透fallthrough，如果在case语句块后增加fallthrough，则会执行下一个case，也叫switch穿透

10. Type Switch ：switch语句还可以被用于type-switch来判断某个interface变量中实际指向的变量类型

    ```go
    var x interface{}   // 空接口
    var y = 10.0
    x = y
    switch i := x.(type) {
    case nil:
        fmt.Println("x 的类型：%T", i)
    case int:
        fmt.Println("x 是 int 型的")
    case float64:
        fmt.Println("x 是 float64 型的")
    case func(int) float64:
        fmt.Println("x 是 func(int) 型的")
    case bool, string:
        fmt.Println("x 是 bool 或 string 型的")
    default:
        fmt.Println("未知类型")
    }
    ```

## **循环语句**

### for循环

```go
for i := 0; i < 100; i++ {      
    i := 1 必须使用:=定义循环变量  
    如果已经声明的变量就不用     
    不可以使用var 声明    
    循环体 
} 
j := 0
for j < 10 {  这样写也没错
    循环体
    j++
}
```

### 注意事项和细节说明

1. 循环条件是一个返回布尔值的表达式

2. Golang提供for-range的方式，可以字符串和数组

    ```go
    var str string = "Hello, World"
    遍历字符串的两种方式
    for i := 0; i < len(str); i++ {   // 按照字节来遍历的，所以遍历不了中文，转成rune切片类型
    	fmt.Printf("%d, %c\n", i, str[i])
    }
    // for-range按照字符的形式遍历，而传统方式是按照字节来遍历
    for index, value := range str {
    	fmt.Printf("index=%d, value=%c\n", index, value)
    }
    ```

### 循环控制语句

```go
break 结束循环 
continue 结束当前循环跳转下一次循环 
goto 将控制转移到标记的语句 
package main 
import "fmt" 
func main() {   
    /* 定义局部变量 */   
    var a int = 10   
    str := "ABC"   
    /* 循环 */   
    LOOP: for a < 20 {    
        if a == 15 {      
            /* 跳过迭代 */      
            a = a + 1         
            goto LOOP    
            当执行到这里的时候会跳回循环开始   
        }    
        fmt.Printf("a的值为 : %d\n", a)    
        a++     
    } 
    range循环
    i 是元素的位置，data是元素本身 data第二个参数不写的时候只写i那么就是返回的索引   
    循环打印str   
    for i, data := range str {       
        fmt.Printf("str[%d] = %s", i, data)   
    }  
} 
```

### break

#### 注意事项和细节

1. break语句出现在多层嵌套的语句块中时，可以通过标签指明终止的是哪一层语句块

2. 标签的基本使用

    ```go
    label1: {
    	label2: {
    		label3: {
    			break label2
    		}
    	}
    }
    ```

### continue

1. continue用于结束本次循环，继续执行下一次循环
2. continue出现在多层嵌套的循环语句中时，可以通过标签指明要跳过的是哪一层循环，这个和break的使用规则一样

### goto

1. Go语言的goto语句可以无条件地转移到程序中指定的行
2. goto语句通常与条件语句配合使用，可用来实现条件转移，跳出循环体等功能，
3. 在Go程序设计中**一般不主张使用goto语句**，以免造成程序流程的混乱，使理解和调试程序都产生困难

## **函数**

为完成某一功能的程序指令(语句)的集合，称为函数，在Go中，函数分为：自定义函数，系统函数

### 基本语法

```
func 函数名(形参列表) (返回值类型列表) {
	执行列表
	return 返回值列表
}
```

1. 形参列表：表示函数的输入
2. 函数中的语句：表示为了实现某一功能代码块
3. 函数可以有返回值，也可以没有

### 包的介绍

#### 包的基本概念

1. go的每一个文件都是属于一个包的，也就是说go是以包的形式来管理文件和项目目录结构的

#### 包的三大作用

1. 区分相同名字的函数，变量名的标识符

2. 当程序文件很多时，可以很好的管理项目

3. 控制函数，变量等访问范围，即作用域

4. 打包基本语法

    package 包名

5. 引入包的基本语法

    import \"包的路径\"

#### 包的注意事项和细节

1. 在给一个文件打包时，该包对应一个文件夹，文件的包名通常和文件所在的文件夹名一致，通常为小写字母

2. 当一个文件要使用其他包函数或变量时，需要先引入对应的包

3. package指令在文件第一行，然后是import指令

4. 在import包时，路径从$GOPATH的src下开始，不用带src，编译器会自动从src下开始引入

5. 为了让其它包的文件，可以访问到本包的函数，则该函数名的首字母需要大写，类似其它语言的public，这样才能跨包访问

6. 在访问其它包函数或变量时，其语法是  包名.函数名

7. 如果包名较长，Go支持给包取别名，注意细节：取别名后，原来的包名就不能使用了

    ```go
    import (
    	"fmt"
    	util "Go_code/chapter05/demo01/utils" // 这里就是给包取别名
    )
    ```

8. 在同一个包下，不能有相同的函数名也不能有相同的全局变量名，否则会报错

9. 如果你要编译成一个可执行程序文件，就需要将这个包声明为main，即package main，这个就是一个语法规范，如果你要写一个库，包名可以自定义

### return语句

1. Go函数支持返回多个返回值，这一点是其它编程语言没有的
2. 如果返回多个值时，在接收时，希望忽略某个返回值，则使用 _ 符号表示占位忽略
    1. 如果返回值只有一个，(返回值类型列表) 可以不写()

### 函数递归调用

1. 执行一个函数时，就创建一个新的保护的独立空间（新函数栈）
2. 函数的局部变量是独立的，不会相互影响
3. 函数必须向退出递归的条件逼近，否则就是无限递归了
4. 当一个函数执行完毕，或者遇到return，就会返回，遵守谁调用，就将结果返回给谁，同时当函数执行完毕或者返回时，该函数本身也会被系统销毁

### 函数注意事项和细节讨论

1. 函数的形参列表可以是多个，返回值列表也可以是多个，多个形参类型相同的话可以省略前面的，只写最后的

    ```go
    func test(n1, n2 int) int { // n1, n2 都是int类型，可以省略n1后面的int
    	return n1 + n2
    }
    ```

2. 形参列表和返回值列表的数据类型可以是值类型和引用类型

3. 函数的命名遵守标识符命名规则，首字母不能是数字，首字母大写该函数可以被本包文件和其他包文件使用，首字母小写，只能被本包文件使用，其他包文件不能使用

4. 函数中的变量是局部的，函数外不生效

5. 基本数据类型和数组默认是值传递的，即进行值拷贝，在函数内修改，不会影响原来的值

6. 如果希望函数内的变量能修改函数外的变量（指的是默认以值传递方式的数据类型），可以传入变量的地址&，函数内以指针的方式操作变量，从效果上看类似引用类型

7. Go函数不支持重载

8. 在Go中，函数也是一种数据类型，可以赋值给一个变量。则该变量就是一个函数类型的变量了，通过该函数可以对函数调用

9. 函数既然是一种数据类型，因此在Go中，函数可以作为形参并调用

    ```go
    func getSum(n1 int, n2 int) int {
    	return n1 + n2
    }
    
    func myFun(fn func(int, int) int, num1 int, num2 int) int {
    	return fn(num1, num2)
    }
    
    func main() {
        result := myFun(getSum, 10, 20)
        fmt.Println("resutl =", result) // result = 30
    }
    ```

10. 为了简化数据类型定义，Go支持自定义数据类型

    1. 基本语法：type 自定义数据类型别名 数据类型 // 相当于一个别名

    2. type long int64 // 这时的long就等价于int64来用

        虽然这里 long 和 int64 都是int64类型的，但是Go还是认为 long 和 int64 是两个数据类型

11. 支持对函数返回值命名，一定要加括号

    ```go
    func getSumAndSub(num1 int, num2 int) (sum int, sub int) {
    	sum = num1 + num2
    	sub = num1 - num2
    	return
    }
    ```

12. 使用 _ 标识符，忽略返回值

13. Go支持可变参数

    ```go
    // 支持0到多个参数
    func sum(args...int) sum int {
    }
    // 支持1到多个参数
    func sum(n1, args...int) sum int {
    }
    ```

    1. args是slice 切片，通过args[index] 可以访问到各个值
    2. 如果一个函数的形参列表中有可变参数，则可变参数需要放在形参列表最后

### init函数

1. 每一个源文件都可以包含一个init函数，该函数会在main函数执行前，被Go运行框架调用，也就是说init会在main函数之前调用
2. 如果一个文件同时包含全局变量定义，init函数和main函数，则执行的流程全局变量定义—>init函数—>main函数
3. init函数最主要的作用，就是完成一些初始化的工作
4. 面试题：如果main.go和utils.go都含有变量定义，init函数时，执行流程是执行utils.go里面的变量定义，init函数，然后执行main.go里面的

### 匿名函数

1. Go支持匿名函数，匿名函数就是没有名字的函数，如果我们某个函数只是希望使用一次，可以考虑使用匿名函数，匿名函数也可以实现多次调用

2. 使用方式

    1. 在定义匿名函数时就直接调用

    ```go
    func (n1 int, n2 int) {
    	fmt.Println(n1 + n2)
    }(10, 20)
    ```

    1. 将匿名函数赋给一个变量(函数变量)，再通过该函数来调用匿名函数

    ```go
    fn := func (n1 int, n2 int) int {  // fn是一个函数类型的变量
        return n1 - n2
    }
    fmt.Println(fn(10, 20)) // -10
    ```

3. 全局匿名函数

    1. 如果将匿名函数赋给一个全局变量，那么这个匿名函数，就成为一个全局匿名函数，可以在程序有效

### 闭包

1. 基本介绍：闭包就是一个函数与其相关的引用环境组合的一个整体(实体)

```go
package main
import "fmt"
func addUpper() func (int) int {
	var n int = 10
	return func (x int) int {
		n = n + x
		return n
	}
}
func main() {
	fn := addUpper()
	fmt.Println(fn(1)) // 11
	fmt.Println(fn(2)) // 13
	fmt.Println(fn(3)) // 16
}
```

2. 上面代码总结

    1. addUpper 是一个函数，返回的数据类型是 func (int) int

    2. 闭包的说明

        ```go
        var n int = 10
        return func (x int) int {
            n = n + x
            return n
        }
        ```

        返回的是一个匿名函数，但是这个匿名函数引用到函数外的 n ，因此这个匿名函数就和 n 形成一个整体，构成闭包

    3. 可以这样理解：闭包是类，函数是操作，n是字段，函数和它使用到的 n 构成闭包

    4. 当我们反复的调用 fn 函数时，因为 n 是初始化一次，因此每调用一次就进行累加

    5. 我们要搞清楚闭包的关键，就要分析出返回的函数它使用(引用)到哪些变量，因为函数和它引用到的变量共同构成闭包

### 函数中的defer

1. 为什么需要defer：在函数中，程序员需要创建资源(比如：数据库连接、文件句柄、锁等)，为了**在函数执行完毕后，及时的释放资源**，Go的设计者提供defer(延时机制)
2. 入门案例

```go
package main
import "fmt"
func sum(n1 int, n2 int) int {
    // 当执行到defer时，暂时不执行，会将defer后面的语句压入到独立的栈中(defer栈)
    // 当函数执行完毕后，再从defer栈中，按照先入后出的方式出栈，执行
	defer fmt.Println("ok1 n1 =", n1)
	defer fmt.Println("ok2 n2 =", n2)
	res := n1 + n2
	fmt.Println("ok3 res =", res)
	return res
}
func main() {
	sum(10, 20)
}
输出结果
ok3 res = 30
ok2 n2 = 20
ok1 n1 = 10
```

3. 细节说明
    1. 当执行到defer时，暂时不执行，会将defer后面的语句压入到一个栈中(自己取名叫defer栈)，然后继续执行函数下一个语句
    2. 当函数执行完毕后，再从defer栈中，依次从栈顶取出语句(先入后出)
    3. 在defer将语句放入栈时，也**会将相关的值拷贝同时入栈**

### 函数参数的传递方式

1. 值类型参数默认就是值传递，而引用类型参数默认就是引用传递
2. 两种传递方式
    1. 值传递
    2. 引用传递
3. 不管是值传递还是引用传递，传递给函数的都是变量的副本，不同的是，值传递是值的拷贝，引用传递是地址的拷贝，一般来说，地址拷贝效率高，因为数据量小，而值拷贝由拷贝数据的大小决定，数据越大，效率越低

### 变量的作用域

1. 函数内部声明/定义的变量叫局部变量，作用域仅限于函数内部
2. 函数外部声明/定义的变量叫全局变量，作用域在整个包都有效，如果首字母为大写，则作用域在整个程序有效
3. 如果变量是在一个代码块，比如for / if 中，那么这个变量的作用域就在改代码块

### Go字符串常用函数

```go
1. 统计字符串的长度，按字节：
	len(str)

2. 字符串遍历，同时处理有中文的问题：
	r := []rune(str)  将字符串转成rune切片

3. 字符串转整数：
	n, err := strconv.Atoi("12")

4. 整数转字符串：
	str := strconv.Itoa(123456)

5. 字符串转 []byte切片：
	var bytes = []byte("hello go") // [h e l l o   g o]

6. []byte 转 字符串：
	str := string([]byte{97, 98, 99}) // "abc"

7. 十进制转八，二，十六进制：
	str := strconv.FormatInt(123, 2) // 

下面的都是strings包中的
8. 判断字符串s是否包含子串substr：
	func Contains(s string, substr string) bool
	strings.Contains("hellooo", "o") // true

9. 返回字符串s中有几个不重复的sep子串：
	func Count(s string, sep string) int
	fmt.Println(strings.Count("aeefas", "e")) // 2

10. 判断两个utf-8编码字符串（将unicode大写、小写、标题三种格式字符视为相同）是否相同：
	func EqualFold(s string, t string) bool
	fmt.Println(strings.EqualFold("abc", "ABC")) // true

11. 子串sep在字符串s中第一次出现的位置，不存在则返回-1：
	func Index(s string, sep string) int
	fmt.Println(strings.Index("hello", "lo")) // 3

12. 子串sep在字符串s中最后一次出现的位置，不存在则返回-1
	func LastIndex(s string, sep string) int
	fmt.Println(strings.LastIndex("olnkol", "ol")) // 4

13. 返回将s中前n个不重叠old子串都替换为new的新字符串，如果n<0会替换所有old子串
	func Replace(s string, old string, new string, n int) string
	fmt.Println(strings.Replace("oink oink oink", "k", "ky", 2)) // oinky oinky oink

14. 按照指定某个字符为分割标识，将一个字符串拆分成字符串切片
	func Split(s string, sep string) []string
	fmt.Printf("%q", strings.Split("a,b,c", ",")) // ["a" "b" "c"]

15. 返回将所有字母都转为对应的小写版本的拷贝
    func ToLower(s string) string
	fmt.Println(strings.ToLower("HELLO")) // hello

16. 返回将所有字母都转为对应的大写版本的拷贝
    func ToUpper(s string) string
	fmt.Println(strings.ToLower("hello")) // HELLO

17. 返回将s前后端所有空白都去掉的字符串
	func TrimSpace(s string) string
	fmt.Println(strings.TrimSpace(" abc ")) // abc 没有前后的空格

18. 返回将s前后端指定字符的字符去掉
	func Trim(s string, cutset string) string
	fmt.Println(strings.Trim("!hello!", "!")) // 将前后端的!去掉，结果 hello

19. 将字符串左边指定的字符去掉
	func TrimLeft(s string, cutset string) string
	fmt.Println(strings.TrimLeft("!hello!", "!")) // 结果 hello!

20. 将字符串右边指定的字符去掉
	func TrimRight(s string, cutset string) string
	fmt.Println(strings.TrimRight("!hello!", "!")) // 结果 !hello

21. 判断字符串是否以指定的字符串开头
	func HasPrefix(s, prefix string) bool  prefix前缀
	fmt.Println(strings.HasPrefix("http://192.168.200.128", "http")) // 判断是否是http开头

22. 判断字符串是否以指定的字符串结束
	func HasSuffix(s, suffix string) bool
	fmt.Println(strings.HasSuffix("a.jpg", ".jpg")) // 判断字符串是否以.jpg结尾

```

### Go时间和日期相关函数

时间和日期相关函数，需要导入time包

```
1. time.Time类型，用于表示时间
2. 获取当前时间time.Now()
	fmt.Println(time.Now()) // 2020-06-03 13:11:59.9278745 +0800 CST m=+0.002975501
3. 获取年月日，时分秒
now := time.Now()
	fmt.Println("年", now.Year()) // 年
	fmt.Println("月", int(now.Month())) // 月
	fmt.Println("日", now.Day()) // 日
	fmt.Println("weekday", now.Weekday()) // 周几
	fmt.Println("时", now.Hour()) // 时
	fmt.Println("分", now.Minute()) // 分
	fmt.Println("秒", now.Second()) // 秒
4. 格式化时间日期
	Printf
	fmt.Printf("当前时间是 %d/%d/%d %d:%d:%02d", now.Year(), now.Month(), now.Day(),
	now.Hour(), now.Minute(), now.Second())
	now.Format("2006/01/02 15:04:05")  // 里面的2006/01/02 15:04:05是固定写法
	now.Format("2006/01/02") // 只得到年月日
	now.Format("15:04:05") // 只得到时分秒
5. 时间的常量
	const (
        Nanosecond  Duration = 1   // 纳秒
        Microsecond          = 1000 * Nanosecond  // 微秒
        Millisecond          = 1000 * Microsecond // 毫秒
        Second               = 1000 * Millisecond // 秒
        Minute               = 60 * Second // 分钟
        Hour                 = 60 * Minute // 时
	)
	直接time.时间常量名，如：100*time.Millisecond  表示100毫秒
6. 结合sleep使用时间常量
	time.Sleep(time.Millisecond * 100) // 休眠0.1秒(100毫秒)
7. 获取当前Unix时间戳和UnixNano时间戳(作用是可以获取随机数字)
	Unix时间戳
	UnixNano时间戳
```

### 内置函数

Golang设计者为了编程方便，提供了一些函数，这些函数可以直接使用，我们称为Go的内置函数，builtin里面的

1. len：用来求长度，比如string，array，slice，map，channel

2. new：用来分配内存，主要用来分配值类型，比如int，float32，struct……返回的是指针

    ![image-20200603180754736](C:\Users\48356\Desktop\笔记\image\image-20200603180754736.png)

3. make：用来分配内存，主要用来分配引用类型，比如chan，map，slice

    <img src="C:\Users\48356\Desktop\笔记\image\image-20200603180826691.png" alt="image-20200603180826691"  />

### 错误处理

1. Go语言不支持传统的try……catch……finally
2. Go中引入的处理方式为：defer, panic, recover
3. Go中可以抛出一个panic的异常，然后再defer中通过recover捕获这个异常，然后正常处理

```go
package main
import "fmt"
func test() {
	defer func() {
		err := recover()
		if err != nil {
			fmt.Println("err =", err)
		}
	}()
	num1 := 10
	num2 := 0
	result := num1/num2
	fmt.Println("res=", result)
}
func main() {
	test()
	fmt.Println("test下面的……")
}
```

4. 自定义错误
    1. Go程序中，支持自定义错误，使用 errors.New 和 panic 内置函数
    2. errors.New("错误说明")，会返回一个error类型的值，表示一个错误
    3. panic内置函数，接收一个interface{}类型的值（也就是任何值了）作为参数，可以接收error类型的变量，**输出错误信息，并退出程序**

```go
package main
import (
	"fmt"
	"errors"
)
func readConf(name string) error {
	if name == "init.config" {
		return nil
	} else {
		return errors.New("读取文件发生错误")
	}
}
func test2() {
	err := readConf("init.config")
	if err != nil {
		panic(err)
	}
	fmt.Println("配置文件读取成功")
}
func main() {
	test2()
}
```

## 数组

数组可以存放多个同一类型数据，数组也是一种数据类型，在Go中，**数组是值类型**

1. 使用数组来解决问题，程序的可维护性增加
2. 而且方法代码更加清晰，也容易扩展

### 数组的定义

```
var 数组名 [数组大小]数据类型
```

四种初始化数组的方式

```go
var arr [3]int = [3]int{1, 2, 3}
var arr = [3]int{1, 2, 3}
var arr = [...]int{6, 7, 8}  // 系统自动判断大小
指定元素值对应的下标
var name = [3]string{1:"tome", 0:"jack", 2:"marry"}
name := [3]string{1:"tome", 0:"jack", 2:"marry"}
```

### 数组的内存地址分布

1. 数组的地址可以通过数组名来获取&arr
2. 数组的第一个元素的地址，就是数组的首地址
3. 数组的各个元素的地址之间是依据数组的类型决定 

### 访问数组元素

1. 数组名[下标] 比如：要是用a数组的第三个元素 a[2]

### for-range遍历数组

```go
for index, value := range arr {
	
}
```

1. 第一个返回值index是数组的下标
2. 第二个value是在该下标位置的值
3. 它们都是仅在 for 循环内部可见的局部变量
4. 遍历数组元素的时候，如果不想使用index，可以直接用 _ 下划线忽略
5. index和value的名称不是固定的，可以自定义

### 注意事项和细节

1. 数组是多个相同类型数组的组合，一个数组一旦声明定义，其长度是固定的，不能动态变化

2. var arr []int 这时 arr 就是一个slice切片

3. 数组中的元素可以是任何数据类型，包括值类型和引用类型，但是不能够混用

4. 数组创建后，如果没有赋值，有默认值，

    1. 数值类型数组，默认值是0
    2. 字符串数组，默认值是\"\"
    3. bool数组，默认值是false

5. 使用数组的步骤

    1. 声明数组并开辟空间
    2. 给数组各个元素元素赋值
    3. 使用数组

6. 数组的下标从0开始

7. 数组下标必须在指定范围内使用，否则报panic：数组越界

8. Go的数组是值类型，在默认情况下是值传递，因此会进行值拷贝。数组间不会相互影响

9. 如想在其他的函数中，去修改原来的数组，可以使用引用传递(指针传递)

    ```go
    func test(arr *[3]int) {
    	(*arr)[0] = 88 // (*arr)[0]取数组里面的值
    }
    func main() {
        var arr = [3]int{1, 2, 3}
        test(&arr)
    }
    ```

10. 长度是数组类型的一部分，在传递函数参数时，需要考虑数组的长度

### 二维数组

```
var arr [4][6]int
arr[1][2] = 1
arr[2][1] = 2
arr[2][3] = 3
for i := 0; i < len(arr); i++ {
	for j := 0; j < len(arr[i]); j++ {
		fmt.Print(arr[i][j], " ")
	}
	fmt.Println()
}
```

#### 二维数组的内存布局

![image-20200610094110286](C:\Users\48356\Desktop\笔记\image\image-20200610094110286.png)

#### 初始化的方式

```go
var arr [2][2]int = [2][2]int{{1, 2}, {1, 2}}
var arr = [2][2]int{{1, 2}, {1, 2}}
arr := [2][2]int{{1, 2}, {1, 2}}
var arr = [...][2]int{{1, 2}, {1, 2}}  // 初始化第二个大小不能用...
var arr [2][2]int = [...][2]int{{1, 2}, {1, 2}}
```

## 切片

### 切片的基本介绍

 1. 切片是数组的引用，因此切片是引用类型，在进行传递时，遵守引用传递的机制

 2. 切片的使用和数组类似遍历切片、访问切片的元素和求切片长度 len(slice) 都一样

 3. 切片的长度是可以变化的，因此切片是一个可以动态变化的数组

 4. 切片定义的基本语法

    ```
    var 切片变量名 []数据类型
    比如：var arr []int
    ```

 5. ![image-20200606075341381](C:\Users\48356\Desktop\笔记\image\image-20200606075341381.png)

### 切片的使用

方式1：定义一个切片，让后让切片去引用一个已经创建好的数组

​	slice := arr[1:3]

方式2：通过make来创建切片

​	基本语法：var 切片名 []type = make([]type, len, cap)

​	type：数据类型，len：大小，cap：指定切片容量 可选，cap的大小必须大于等于len

 	1. 通过make方式创建切片可以指定切片的大小和容量
 	2. 如果没有给切片的各个元素赋值，就会使用默认值
 	3. 通过make方式创建的切片对应的数组有make底层维护，对外不可见，只能通过slice去访问各个元素

方式3：定义一个切片，直接就指定具体数组，使用原理类似 make 的方式

​	var slice []int = []int{1, 3, 5}

### 注意事项和细节说明

1. 切片初始化是 var slice = arr[startIndex:endIndex]  从arr数组下标为startIndex，取到下标为endIndex的元素(不包含arr[endIndex])
2. 切片初始化时，仍然不能越界，范围在[0-len(arr)]之间，到时可以动态增长
3. var slice = arr[0:end] 可以简写 var slice = arr[:end]
4. var slice = arr[start:len(arr)] 可以简写 var slice = arr[start:]
5. var slice = arr[0:len(arr)] 可以简写 var slice = arr[:]
6. cap是一个内置函数，用于统计切片的容量，即最大可以存放多少个元素
7. 切片定义完后，还不能使用，因为本身是一个空的，需要让其引用到一个数组，或者make一个空间供切片使用
8. 切片可以继续切片
9. 用append内置函数，可以对切片进行动态追加
    1. 切片append操作的本质就是对数组扩容
    2. go底层会创建一个新的数组newArr(安装扩容后大小)
    3. 将slice原来包含的元素拷贝到新的数组newArr
    4. slice重新引用到newArr，原来的就被gc回收了
    5. 注意newArr是在底层来维护的，程序员不可见
10. 使用for-range 遍历切片时val 是值拷贝所以不能修改切片里面的值

```
var slice []int = []int{1, 2, 3}
追加元素，会返回一个新的切片，没有赋值的话本身slice内容没有变
slice = append(slice, 4, 5)
通过append将切片slice2追加给slice
slice = append(slice, slice2...)
var sli []int = []int{1, 2, 3}
fmt.Printf("sli原来的地址是%v, 值是%v\n", &sli[0], sli)
sli = append(sli, 4, 5, 6)
fmt.Printf("sli改变后的地址是%v, 值是%v", &sli[0], sli)
结果
sli原来的地址是0xc00000c440, 值是[1 2 3]
sli改变后的地址是0xc00000a300, 值是[1 2 3 4 5 6]
```

### 切片的拷贝操作

切片使用copy内置函数完成拷贝

```
func copy(dst, src []Type) int  都要是切片类型
内建函数copy将元素从来源切片复制到目标切片中，也能将字节从字符串复制到字节切片中。copy返回被复制的元素数量，它会是 len(src) 和 len(dst) 中较小的那个。来源和目标的底层内存可以重叠。
```

### 切片删除操作

```go
index := 3 // 指定删除元素位置
if index == -1 {
	return false
}
cs.Customers = append(cs.Customers[:index], cs.Customers[index+1:]...) 
将删除元素前后重新切片赋值
```

### string和slice的关系

1. string底层是一个byte数组，因此string也可以进行切片处理
2. string和切片在内存的形式
3. string是不可变的，也就是说不能通过 str[0] = 'z' 方式来修改字符串
4. 如果要修改字符串，可以先将string转成[]byte或[]rune修改重写然后再转成string

## 数组排序和查找

### 排序

#### 排序基本介绍

排序是将一群数据，按指定的顺序进行排列的过程

排序的分类：

 1. 内部排序

     1. 指将需要处理的所有数据都加载到内部存储器中进行排序

        包括(交换式排序，选择式排序和插入式排序)

 2. 外部排序

     	1. 数据量过大，无法全部加载到内存中，需要借助外部存储进行排序，包括(合并排序法和直接合并排序法)

### 交换式排序

交换式排序属于内部排序法，是运用数据值比较后，依判断规则对数据位置进行交换，以达到排序的目的

交换式排序法又可分为两种

1. 冒泡排序法

    通过对待排序序列从后向前(从下标较大的元素开始)，依次比较相邻元素的排序码，若发现逆序则交换，使排序码较小的元素逐渐向后移向前部(从下标较大的单元移向下标较小的单元)，就像水底下的气泡一样逐渐向上冒，

    因为排序的过程中，各元素不断接近自己的位置，如果一趟比较下来没有进行过交换，说明序列有序，因此要在排序过程中设置一个标志flag判断元素是否进行过交换。从而减少不必要的比较

    1. 一共会经过arr.length-1的轮数比较，每一轮会确定一个数的位置
    2. 每一轮的比较次数再逐渐的减少
    3. 当发现前面的一个数比后面的一个数大的时候，就进行了交换


```go
package main
import "fmt"
func main() {
	var arr = [...]int{3, 4, 23, 34, 123, 2, 66, 90, 48, 29, 98, 903}
	flag := true
	for i := 0; i < len(arr)-1; i++ {
		for j := 0; j < len(arr)-i-1; j++ {
			if arr[j] > arr[j+1] {
				arr[j], arr[j+1] = arr[j+1], arr[j]
				flag = false
			}
		}
		if flag {
			break
		}
	}
	fmt.Println(arr)
}
```

1. 快速排序法

### 查找

在Golang中，我们常用的查找有两种：

1. 顺序查找

```go
方式1
var arr = [...]string{"白眉鹰王", "金毛狮王", "紫衫龙王", "青翼蝠王"}
var heroName string
fmt.Println("输入一个名称：")
fmt.Scanln(&heroName)
for i, val := range arr {
	if val == heroName {
		fmt.Println("找到了", heroName, "下标是", i)
		break
	} else if i == len(arr) - 1 {
		fmt.Println("没有找到", heroName)
	}
}
方式2 推荐使用
var heroIndex int = -1
for i, val := range arr {
	if val == heroName {
		heroIndex = i
		break
	}
}
if heroIndex != -1 {
	fmt.Printf("找到了%s, 下标是%v", heroName, heroIndex)
} else {
	fmt.Println("没有找到", heroName)
}
```

1. 二分查找(该数组是有序的)
    ![image-20200609221715438](C:\Users\48356\Desktop\笔记\image\image-20200609221715438.png)

```go
func binaryFind(arr *[5]int, leftIndex int, rightIndex int,findVal int) {
	if leftIndex > rightIndex {
		fmt.Println("没有找到")
		return
	}
	var middle int = (rightIndex + leftIndex)/2
	if (*arr)[middle] > findVal {
		rightIndex = middle - 1
		binaryFind(arr, leftIndex, rightIndex, findVal)
	} else if (*arr)[middle] < findVal {
		leftIndex = middle + 1
		binaryFind(arr, leftIndex, rightIndex, findVal)
	} else {
		fmt.Println("找到了下标", middle)
	}
}
func main() {
	numArr := [...]int{1, 8, 89, 1000, 1234}
	binaryFind(&numArr, 0, len(numArr) - 1, 1001)
	fmt.Println()
}
```

## map(映射)

map是key-value数据结构，又称为字段或关联数组，类似其他编程语言的集合

### 基本语法

```go
var map变量名 map[keytype]valuetype
```

key可以是什么类型

Golang中的map的key可以是很多种类型，比如 bool、数字、string、指针、channel，还可以是只包含前面几个类型的 接口、结构体、数组  **通常为int、string**

注意：slice、map 还有 function 不可以，因为这几个没法用 == 来判断

value可以是什么类型

value的类型和key基本一样，通常为：数字、string、map、struct

### 举例

```go
var a map[string]string
var a map[string]int
var a map[int]string
var a map[string]map[string]string
```

**注意**：声明是不会分配内存的，初始化需要make，分配内存后才能赋值和使用

map的使用方式

1. ```go
    // 声明，这是map=nil
    var cities map[string]string
    // make(map[string]string, 10) 分配一个map空间
    cities = make(map[string]string, 10)
    ```

2. ```go
    // 声明就直接make
    var cities = make(map[string]string)
    ```

3. ```go
    // 声明，直接赋值，底层还是make了
    var cities map[string]string = map[string]string{
        "no4" : "成都",
    }
    cities := map[string]string{
        "no4" : "成都",
    }
    cities["no1"] = "北京"
    ```

### map的增删改查操作

#### map的增加和更新

```
map["key"] = value // 如果key还没有，就是增加，如果key存在就是修改
```

#### map删除

1. delete(map, "key")，delete是一个内置函数，如果key存在，就删除该key-value，如果key不存在，不操作，但是不会报错
2. 如果我们要删除map的所有key，没有一个专门的方法一次删除，可以遍历一下key，逐个删除
3. 或者 map = make(...)，make一个新的，让原来的成为垃圾，被GC回收

#### map查找

```go
val, findRes = heroes["no1"]
if findRes {
	fmt.Println("找到了val =", val)
} else {
	fmt.Println("没有找到")
}
```

如果heroes这个map中存在 \"no1\" ，那么 findRes 就会返回 true 否则返回 false

### map遍历

map只能用for-range的形式遍历

### map切片

切片的数据类型如果是map，则我们称为 slice of map，map切片，这样使用则map的个数就可以动态变化了

```go
var monster = make([]map[string]string, 2)
monster[0] = make(map[string]string)
monster[0]["name"] = "狐狸精"
monster[0]["age"] = "20"
monster[1] = make(map[string]string)
monster[1]["name"] = "猪精"
monster[1]["age"] = "100"
newMonster := map[string]string{
    "name" : "火云邪神",
    "age" : "20",
}
monster = append(monster, newMonster)
fmt.Println(monster)
fmt.Println()
```

### map排序

#### 基本介绍

1. Golang中没有一个专门的方法map的key进行排序
2. Golang中的map默认是无序的，注意也不是按照添加的顺序存放的，你每次遍历，得到的输出可能不一样
3. Golang中map的排序，是先将 key 进行排序，然后根据 key 值遍历输出即可

```go
package main
import (
	"fmt"
	"sort"
)
func main() {
	map1 := make(map[int]int, 10)
	map1[10] = 3
	map1[2] = 10
	map1[4] = 20
	map1[6] = 20
	fmt.Println(map1)
	var keys []int
	for i := range map1 {
		keys = append(keys, i)
	}
	fmt.Println(keys)
	sort.Ints(keys)
	fmt.Println(keys)
	for _, val := range keys {
		fmt.Println(map1[val])
	}
	fmt.Println()
}
```

### map使用细节

1. map 是引用类型，遵守引用类型传递的机制，在一个函数接收 map，修改后，会直接修改原来的map
2. map 的容量达到后，再想 map 增加元素，会自动扩容，并不会发生 panic，也就是说 map，能动态的增长键值对(key-value)
3. map 的 value 也经常使用 struct 类型，更适合管理复杂的数据(比前面 value 是一个 map 更好)，比如 value 为 Student 结构体

## 面向对象

面向对象编程（OOP），Golang仍然有面向对象编程的继承，封装和多态的特性

### 结构体

```go
type Cat struct {
	Name string
	Age int
	Color string
}
var cat1 Cat
cat1.Name = "tom"
cat1.Age = 20
cat1.Color = "red"
```

#### 结构体声明和使用陷阱

1. 如何声明结构体

```go
type 结构体名 struct {
	field type
	field type
}
举例
type Student struct {
    Name string
    Age int
    Score float32
}
```

#### 字段属性

1. 从概念或叫法上看：结构体字段 = 属性 = field	
2. 字段是结构体组成的一个部分，一般是基本数据类型、数组，也可以是引用类型
3. 字段声明语法同变量
4. 字段的类型可以为，基本类型，数组或引用类型
5. 在创建一个结构体变量后，如果没有给字段赋值，都对应一个零值(默认值)，指针，slice和map的零值都是nil，既没有分配空间
6. 不同结构体变量的字段是独立的，互不影响，一个结构体变量字段的更改，不影响另外一个

创建结构体变量和访问结构体字段

1. 直接声明

    var person Person

2. {}

    var person Person = Person{}

3. &

    var person *Person = new(Person)

    ```go
    type Person struct {
    	Name string
    	Age int
    }
    func main() {
    	var person = new(Person)
    	(*person).Name = "tom" // 括号可以省略，写成person.Name
    	(*person).Age = 20
    	fmt.Println(*person)
    }
    ```

4. {}

    var person *Person = &Person{}

    ```go
    type Person struct {
    	Name string
    	Age int
    }
    func main() {
        var person = &Person{}
    	(*person).Name = "tom" // 括号可以省略，写成person.Name
    	(*person).Age = 20
    	fmt.Println(*person)
        var person *Person = &Person{
            Name: "a",
            Age: 20,
        }
    }
    不能写*person.Name 会报错，因为.的优先级比*高，所以*一个具体的值会报错，除非person.Name是一个地址
    ```

5. 第3种和第4种方式返回的是 结构体指针

6. 结构体指针访问字段的标准方式应该是：(*结构体指针).字段名，比如：(\*person).Name = \"tome\"

7. 但go做了一个简化，也支持 结构体指针.字段名，比如 person.Name = \"tome\"。更加符合程序员使用的习惯，go编译器底层对 person.Name 做了转换 (*person).Name

#### 结构体使用细节和注意事项

1. 结构体的所有字段在内存中是连续的

2. 结构体是用户单独定义的类型，和其他类型进行装换时需要有完全相同的字段（名字、个数和类型）

3. 结构体进行 type 重新定义(相当于起别名)，Golang认为是新的数据类型，但是相互间可以强转。

    ```
    type Student struct {
    	Name string
    	Age int
    }
    type Stu Student
    func main() {
    	var stu1 Student
    	var stu2 Stu
    	stu2 = stu1
    	fmt.Println(stu1, stu2)
    }
    ```

4. struct 的每个字段上，可以写上以 tag ，该 tag 可以通过反射机制获取，常见的使用场景就是序列化和反序列化 json

    ```go
    import (
    	"fmt"
    	"encoding/json"
    )
    // Monster monster
    type Monster struct {
    	Name string `json:"name"` // `json:"name"` 就是struct tag
    	Age int	`json:"age"`
    	Skill string `json:"skill"`
    }
    func main() {
    	var monster Monster
    	monster.Name = "红孩儿"	
    	monster.Age = 10
    	monster.Skill = "吐火"
    	// json.Marshal 函数中使用了反射
    	val, _ := json.Marshal(monster)
    	fmt.Printf(string(val))
    }
    ```

### 方法

基本介绍

​	Golang中的方法是作用在指定的数据类型上的（即和指定数据类型绑定），因此自定义类型都可以有方法，而不仅仅是结构体

```go
package main
import "fmt"
// Person person
type Person struct {
	Name string
}
func (a Person) test() {
	fmt.Println(a.Name)
}
func main() {
	var b = Person{"zhangsan"}
	b.test()
}
```

1. test 方法和 Person 类型绑定
2. test 方法只能通过 Person类型的变量来调用，而不能直接调用，也不能使用其他类型的变量来调用

#### 方法的声明

```go
func (recevier type) mothedName(参数列表) (返回值列表){
	方法体
	return 返回值
}
```

1. 参数列表：表示方法输入
2. recevier type：表示这个方法和type这个类型绑定，或者说该方法作用域type类型
3. recevier type：type可以是结构体，也可以是其它自定义类型
4. recevier：就是一个type类型的一个变量(实例)

#### 注意事项和细节

1. 结构体类型是值类型，在方法调用中，遵守值类型的传递机制，是值拷贝传递方式

2. 如程序员希望在方法中，修改结构体变量的值，可以通过结构体指针的方式来处理

    调用的时候应该是 (&c).area() 但是 go 底层优化可以写成 c.area()

3. Golang中方法作用在指定的数据类型上的(即：和指定的数据类型进行绑定)，因此自定义类型，都可以有方法，而不仅仅是struct，比如int，float32等都可以有方法

    ```
    type integer int
    func (i *integer) change() {
    	*i = *i + 1
    }
    func main() {
    	var i integer = 10
    	i.change()
    	fmt.Println(i) // 11
    }
    ```

4. 方法的访问范围控制的规则，和函数一样，方法名首字母小写，只能在本包访问，大写可以在其他包访问

5. 如果一个类型实现了String()这个方法，fmt.Println默认会调用这个变量的String()进行输出

```go
/*
	1 2 3		1 4 7
	4 5 6	=>	2 5 8
	7 8 9  		3 6 9

	arr[0][0]   <=>   arr[0][0]
	arr[0][1] 	<=>	  arr[1][0]
	arr[0][2] 	<=>	  arr[2][0]
	arr[1][1] 	<=>	  arr[1][1]
	arr[1][2] 	<=>	  arr[2][1]
	arr[2][2] 	<=>	  arr[2][2]

*/
func (methodutils MethodUtils) reversl(arr *[3][3]int) {
	for i := 0; i < len(arr); i++ {
		for j := i; j < len(arr[i]); j++ {
			(*arr)[i][j], (*arr)[j][i] = (*arr)[j][i], (*arr)[i][j]
		}
	}
}
```

### 方法和函数的区别

1. 调用方式不一样

    函数的调用方式： 			函数名(实参列表)

    方法的调用方式：			 变量.方法名(实参列表)

2. 对于普通函数，接收者为值类型时，不能将指针类型的数据直接传递，反之亦然

3. 对于方法（如struct方法），接收者为值类型时，可以直接用指针类型的变量调用方法，反过来也可以，真正决定值拷贝还是地址拷贝，主要是看这个方法是跟哪种类型绑定的

```go
type person struct {
	Name string
}
func (p person) test01() {
	fmt.Println(p.Name)
}
func (p *person) test02() {
	p.Name = "jack"
	fmt.Println(p.Name)
}
func main() {
	var p = person{"张三"}
	p.test01()
	(&p).test01() // 从形式上看是传入地址，但是本质是值拷贝
	(&p).test02() // 等价于 p.test02
	fmt.Println(p.Name)
}
```

### 工厂模式

Golang的结构体没有构造函数，通常可以使用工厂模式来解决这个问题

main.go

```
package main
import (
	"Go_code/chapter08/factory/model"
	"fmt"
)
func main() {
	var stu1 = model.NewStudent("张三", 95.5)
	fmt.Println(stu1.GetScore())
}
```

student.go

```
package model
// Student student
type student struct {
	Name  string
	score float64
}
// NewStudent 用来创建student类型，
func NewStudent(n string, s float64) *student {
	return &student{
		Name:  n,
		score: s,
	}
}
func (stu *student) GetScore() float64 {
	return stu.score
}
```

## 面向对象编程三大特性

### 封装

封装就是把抽象出来的字段和对字段的操作封装在一起，数据被保护在内部，程序的其他包只有通过被授权的操作(方法)，才能对字段进行操作

#### 封装的实现步骤

1. 将结构体、字段(属性)的首字母小写(不能导出，其他包不能使用)
2. 将结构体所在包提供一个工厂模式的函数，首字母大写。类似一个构造函数
3. 写一对 Getter 和 Setter 方法

### 继承

在Golang中，如果一个struct嵌套了另一个匿名结构体，那么这个结构体就可以直接访问匿名结构体的字段和方法，从而实现了继承特性

```go
package main
import "fmt"
type student struct {
	Name  string
	Age   int
	Score int
}
type pupil struct {
	student
}
type graduate struct {
	student
}
func (stu *student) showInfo() {
	fmt.Printf("学生名 = %v 年龄 = %v 成绩 = %v\n", stu.Name, stu.Age, stu.Score)
}
func (stu *student) setScore(score int) {
	stu.Score = score
}
func (p pupil) testing() {
	fmt.Println("小学生考试中......")
}
func (g *graduate) testing() {
	fmt.Println("大学生考试中......")
}
func main() {
    // 下面的 *.student. 都可以简写成 *. 省略student
	var p1 = &pupil{}
	p1.student.Name = "张三"
	p1.student.Age = 12
	p1.testing()
	p1.student.setScore(70)
	p1.student.showInfo()

	var g1 = &graduate{}
	g1.student.Name = "marry~"
	g1.student.Age = 24
	g1.testing()
	g1.student.setScore(90)
	g1.student.showInfo()
}
```

1. 结构体可以使用嵌套匿名结构体所有的字段和方法，即：首字母大小写的字段、方法都可以使用

2. 匿名结构体字段方法可以简化，向上查找

    ```go
    var p1 = &pupil{}
    p1.student.Name = "张三"   ==> 	p1.Name = "张三"
    p1.student.Age = 12  	  ==> 	 p1.Age = 12
    ```

3. 当结构体和匿名结构体有相同的字段或方法时，编译器采用**就近访问原则**，如希望访问匿名结构体的字段和方法，可以通过匿名结构体名来区分

4. 结构体嵌入两个(或多个)匿名结构体，如果两个匿名结构体有相同的字段和方法(同时结构体本身没有同名的字段和方法)，在访问时，就必须要明确指定匿名结构体名字，否则编译报错

5. 如果一个struct嵌套了一个有名结构体，这种模式就是组合，如果是组合关系，那么在访问组合的结构体的字段和方法时，必须带上结构体的名字

    ```go
    type A struct {
    	Name string
    	age int
    }
    type D struct {
    	a A
    }
    func main() {
    	var d D
    	d.a.Name = "张三" // 不能通过d.Name访问
    }
    ```

6. 嵌套匿名结构体后，也可以在创建结构体变量时，直接指定各个匿名结构体字段的值

    ```go
    type Goods struct {
    	Name string
    	Price float64
    }
    type Brand struct {
    	Name string
    	Address string
    }
    type TV struct {
    	Goods
    	Brand
    }
    type TV2 struct {
    	*Goods
    	*Brand
    }
    func main() {
    	vat tv1 = TV{ Goods{"电视机001", 5000}, Brand{"海尔", "山东"}, }
    	var tv2 = TV{
    		Goods{
    			Name: "电视机002",
    			Price: 2000.1,
    		},
    		Brand{
    			Name: "海信",
    			Address: "成都",
    		}
    	}
    	vat tv3 = TV2{ &Goods{"电视机001", 5000}, &Brand{"海尔", "山东"}, }
    	var tv4 = TV2{
    		&Goods{
    			Name: "电视机002",
    			Price: 2000.1,
    		},
    		&Brand{
    			Name: "海信",
    			Address: "成都",
    		},
    	}
    }
    ```

7. 当结构体的匿名字段是基本数据类型

    ```go
    type A struct {
    	Name string
    	Age int
    }
    type Stu struct {
    	A
    	int // 不能有多个同名的匿名字段
    }
    func main() {
    	stu := Stu{}
    	stu.Name = "tom"
    	stu.Age = 20
    	stu.int = 80
    	fmt.Println(stu) // {{"tome" 20} 80}
    }
    ```

8. 一个struct嵌套了多个匿名结构体，那么该结构体可以直接访问嵌套的匿名结构体的字段和方法，从而实现了多重继承

    ```go
    type Goods struct {
    	Name string
    	Price float64
    }
    type Brand struct {
    	Name string
    	Address string
    }
    type TV struct { // TV同时继承了Goods和Brand
    	Goods
    	Brand
    }
    ```

## 接口

interface 类型可以定义一组方法，但是这些不需要实现。并且interface不能包含任何变量。到定义某个自定义类型要使用的时候，在根据具体情况把这些方法写出来

### 基本语法

```go
type 接口名 interface {
	method1(参数列表) 返回值类型
	method2(参数列表) 返回值类型
}
```

1. 接口里的所有方法都没有方法体，即接口的方法都是没有实现的方法，接口体现了程序设计的多态和高内聚低耦合的思想
2. Golang中的接口，不需要显式的实现。只需要一个变量，含有接口类型的所有方法，那么这个变量就实现这个接口

```go
package main
import "fmt"
type usb interface {
	start()
	stop()
}
type phone struct {}
type camera struct {}
func (p phone) start() {
	fmt.Println("手机插入USB了。。。")
}
func (p phone) stop() {
	fmt.Println("手机USB拔出来了。。。")
}
func (cam camera) start() {
	fmt.Println("手机插入USB了。。。")
}
func (cam camera) stop() {
	fmt.Println("手机USB拔出来了。。。")
}
type computer struct {}
func (c computer) working(u usb) {
	u.start()
	u.stop()
}
func main() {
	var computer1 computer
	var p1 phone
	var c1 camera
	computer1.working(p1)
	computer1.working(c1)
}
```

### 注意事项和细节

```go
type A interface {
	say()
}
type B intergace {
    hello()
}
```

1. 接口本身不能创建实例，但是可以指向一个实现了该接口的自定义类型的变量

    ```go
    type Stu struct {}
    func (stu Stu) say() {
    	fmt.Println("hello, stu")
    }
    func main() {
    	var b Stu
    	var a A = b
    	a.say()
    }
    ```

2. 接口中所有的方法都没有方法体，即都是没有实现的方法

3. 在Golang中 ，一个自定义类型需要将接口的所有方法都实现我们说这个自定义类型实现了该接口

4. 只要是自定义数据类型，就可以实现接口，不仅仅是结构体类型

    ```go
    type integer int
    func (i integer) say() {
    	fmt.Println("hello")
    }
    ```

5. 一个自定义类型可以实现多个接口

    ```go
    type monster struct {}
    func (m monster) say() {
        fmt.Println("monster say()")
    }
    func (m monster) hello() {
        fmt.Println("monster hello()")
    } 这样就实现了两个接口
    ```

6. Golang接口中不能有任何变量

7. 一个接口(A 接口)可以继承多个别的接口(B，C接口)，这时如果要实现A接口，也必须将B，C接口的方法也全部实现

    ```go
    type C interface {
    	A
    	B   // A B接口中不能有相同的方法，否则报错，报重复定义的错误
    	test()
    } // 如果要实现C接口那么就要将test和A B接口里面的全部方法都实现
    ```

8. interface类型默认是一个指针(引用类型)，如果没有对interface初始化，那么会输出nil

9. 空接口interface没有任何方法，所以所有类型都实现了空接口，即我们可以把任何类型的变量赋给空接口

    ```go
    type T interface {}
    func main() {
        var t1 T = stu
        fmt.Pritnln(t) // {}
        var t2 interface{} = stu
        var num1 float64 = 8.8
        t1 = num1 // t1 = 8.8
        t2 = num1 // t2 = 8.8
    }
    ```


### 接口最佳实践

```go
package main
import (
	"fmt"
	"sort"
)
type hero struct {
	Name string
	Age  int
}
type heroSlice []hero
func (hs heroSlice) Len() int {
	return len(hs)
}
// less 方法就是决定你使用什么标准进行排序
func (hs heroSlice) Less(i, j int) bool {
	return hs[i].Age < hs[j].Age // 大于是降序 小于是升序
}
// 进行换值的方法
func (hs heroSlice) Swap(i, j int) {
	hs[i], hs[j] = hs[j], hs[i]
}
func main() {
	var heros = heroSlice{
		{"zhangsan", 20},
		{"lisi", 17},
		{"zhaowu", 4},
		{"liliu", 47},
		{"qiqi", 23},
		{"luba", 45},
	}
	fmt.Println(heros)
	sort.Sort(heros)
	fmt.Println(heros)
}
```

### 实现接口和继承比较

```go
package main
import (
	"fmt"
)
type monkey struct {
	Name string
}
func (m *monkey) eat() {
	fmt.Println(m.Name, "吃香蕉")
}
type bird interface {
	fly()
}
type fish interface {
	swmming()
}
type monkeyChild struct {
	monkey
}
func (m *monkeyChild) fly() {
	fmt.Println(m.Name, "通过学习，会飞了")
}
func (m *monkeyChild) swmming() {
	fmt.Println(m.Name, "通过学习，会游泳了")
}
func main() {
	var m  = monkeyChild{ monkey{Name: "悟空"} }
	m.eat()
	m.fly()
	m.swmming()
}
```

1. 当A结构体继承了B结构体，那么A结构体就自动继承了B结构体的方法，并且可以直接使用
2. 当A结构体需要扩展功能，同时不希望去破坏继承关系，则可以去实现某个接口即可，因此我们可以认为：实现接口是对继承机制的补充

![image-20200627111515845](C:\Users\48356\Desktop\笔记\image\image-20200627111515845.png)

3. 接口和继承解决的问题不同
      1. **继承的价值**主要在于：解决代码的复用性和可维护性
      2. **接口的价值**主要在于：设计，设计好各种规范，让其他自定义类型去实现这些方法

4. 接口比继承更加灵活

    接口比继承更加灵活，继承是满足 is  -  a 的关系，而接口只需满足 like  -  a的关系

5. 接口在一定程度上实现解耦

### 多态

变量具有多种形态。面向对象的第三大特征，在Golang中，多态特征是通过接口实现的，可以安装统一的接口来调用不同的实现，这是接口变量就呈现不同的形态

#### 接口体现多态特征

1. **多态参数**

    在前面 Usb 接口案例， Usb usb，既可以接收手机变量，又可以接收相机变量，Usb 接口多态

2. **多态数组**

    ```go
    package main
    import "fmt"
    type usb interface {
    	start()
    	stop()
    }
    type phone struct {}
    type camera struct {}
    func (p phone) start() {
    	fmt.Println("手机插入USB了。。。")
    }
    func (p phone) stop() {
    	fmt.Println("手机USB拔出来了。。。")
    }
    func (cam camera) start() {
    	fmt.Println("相机插入USB了。。。")
    }
    func (cam camera) stop() {
    	fmt.Println("相机USB拔出来了。。。")
    }
    type computer struct {}
    func (c computer) working(u usb) {
    	u.start()
    	u.stop()
    }
    func main() {
    	var usbArr [3]usb
    	usbArr[0] = camera{}
    	usbArr[1] = phone{}
    	usbArr[2] = phone{}
    	fmt.Println(usbArr)
    	for _, val := range usbArr {
    		val.start()
    	}
    }
    ```

### 类型断言

```go
package main
import (
	"fmt"
)
type point struct {
	x int
	y int
}
func main() {
	var a interface{}
	var p point
	a = p
	var b point
	// 直接 b = a 会报错  
    b = a.(point)
    // b = a.(point) 就是类型断言，表示判断a是否指向point类型的变量，如果是就转成point类型并赋值给b变 	// 量,否则报错
	fmt.Println(b)
    var x interface{}
	var b2 float32 = 1.1
	x = b2 
	y, isOk := x.(float64) // 带检测的
	if isOk {
		fmt.Println("成功")
	} else {
		fmt.Println("失败")
	}
	fmt.Println(y)
}
```

类型断言，由于接口是一般类型，不知道具体类型，如果要转成具体类型，就需要使用类型断言

```go
package main
import "fmt"
type student struct {}
func typeJudge(item ...interface{}) {
	for i, v := range item {
		switch v.(type) {
		case bool :
			fmt.Printf("第%v个参数是 bool 类型，值是%v\n", i + 1, v)
		case int, int32, int64 :
			fmt.Printf("第%v个参数是 int 类型，值是%v\n", i + 1, v)
		case string :
			fmt.Printf("第%v个参数是 string 类型，值是%v\n", i + 1, v)
		case float64, float32 :
			fmt.Printf("第%v个参数是 float 类型，值是%v\n", i + 1, v)
		case byte :
			fmt.Printf("第%v个参数是 字符 类型，值是%c\n", i + 1, v)
		case student :
			fmt.Printf("第%v个参数是 student 类型，值是%c\n", i + 1, v)
		case *student :
			fmt.Printf("第%v个参数是 *student 类型，值是%c\n", i + 1, v)

		default :
			fmt.Println("其他类型")
		}
	}
}
func main() {
	var a = 10
	var f = 1.1
	var c byte = 'a'
	var s = "asjdlf"
	var stu student
	typeJudge(a, f, c, s, stu, &stu)
}
```

## 项目

项目1-家庭收支记账系统

```go
package main
import "fmt"
type homeMoney struct {
	Mold       string  // 收支 支出 或 收入
	TotalMoney float64 // 账户总额
	UseMoney   float64 // 收支金额
	Declare    string  // 说明
}
func (h *homeMoney) detail(sli *[]homeMoney) {
	fmt.Println("\t\t\t--------------------当前收支明细记录-----------------------")
	fmt.Println("\t\t\t收支\t\t账户金额\t收支金额\t说明")
	for _, val := range *sli {
		fmt.Printf("\t\t\t%s\t\t%v\t\t%v\t\t%s\n", val.Mold, val.TotalMoney, val.UseMoney, val.Declare)
	}
	fmt.Println()
}
func (h *homeMoney) income(sli *[]homeMoney) {
	var money float64
	var str string
	fmt.Print("\t\t\t\t\t\t本次收入金额: ")
	fmt.Scanln(&money)
	fmt.Print("\t\t\t\t\t\t本次收入说明: ")
	fmt.Scanln(&str)
	h.Mold = "收入"
	h.TotalMoney += money
	h.UseMoney = money
	h.Declare = str
	*sli = append(*sli, *h)
}
func (h *homeMoney) expend(sli *[]homeMoney) {
	var money float64
	var str string
	fmt.Print("\t\t\t\t\t\t本次支出金额: ")
	fmt.Scanln(&money)
	fmt.Print("\t\t\t\t\t\t本次支出说明: ")
	fmt.Scanln(&str)
	if money > h.TotalMoney {
		fmt.Println("\t\t\t\t\t\t你的余额不够这么多，只有", h.TotalMoney)
		return
	}
	h.Mold = "支出"
	h.TotalMoney -= money
	h.UseMoney = money
	h.Declare = str
	*sli = append(*sli, *h)
}
func mainPage() {
	fmt.Println("\n\t\t\t-----------------------------------------------------------")
	fmt.Println("\t\t\t---------------------家庭收支记账软件----------------------")
	fmt.Println()
	fmt.Println("\t\t\t\t\t\t1 收支明细")
	fmt.Println("\t\t\t\t\t\t2 登记收入")
	fmt.Println("\t\t\t\t\t\t3 登记支出")
	fmt.Println("\t\t\t\t\t\t4 退    出")
}

func main() {
	var sli []homeMoney
	var myHome = homeMoney{}
label1:
	for {
		mainPage()
		fmt.Print("\t\t\t\t\t\t请选择(1-4): ")
		var num int
		fmt.Scanln(&num)
		switch num {
		case 1:
			myHome.detail(&sli)
		case 2:
			myHome.income(&sli)
		case 3:
			myHome.expend(&sli)
		case 4:
			fmt.Println("\t\t\t\t\t你退出了家庭记账软件的使用")
			break label1
		default:
			fmt.Println("\t\t\t\t\t\t输入错误")
		}
	}
	fmt.Println()
}
```

项目2-客户信息管理系统

project02

## 文件操作

文件在程序中是以流的形式来操作的

流：数据在数据源(文件)和程序(内存)之间经历的路径

输入流：数据从数据源(文件)到程序(内存)的路径  （读文件）

输出流：数据从程序(内存)到数据源(文件)的路径（写文件）

Go中有os.File结构体操作文件

### 读取文件内容方式1

```go
// 读取文件并显示在终端
package main
import (
	"fmt"
	"os"
	"io"
	"bufio"
)
func main() {
	// 打开文件
	file是一个指针
	file, _ := os.Open("E:/学习/Go/src/Go_code/practise/bubbleSort/main.go")
	defer file.Close() // 及时关闭文件，防止内存泄露
	reader:= bufio.NewReader(file)
	// 循环读取文件的内容
	for {
		str, err := reader.ReadString('\n') // 读到一个换行就结束
		if err == io.EOF { // io.EOF 表示文件的末尾
			break
		}
		fmt.Print(str)
	}
	fmt.Println()
}
```

### 读取文件内容方式2不带缓冲的

读取文件的内容并显示在终端(使用ioutil一次将整个文件读入到内存中)，这种方式适用于文件不大的情况。相关方法和函数(ioutil.ReadFile)

```go
package main
import (
	"fmt"
	"io/ioutil"
)
func main() {
	file := "E:/学习/Go/src/Go_code/chapter09/demo01/main.go"
	content, _ := ioutil.ReadFile(file)
    // 把文件的打开和关闭操作写在了函数内部
	fmt.Println(string(content))
}
```

### 写文件操作

```go
package main
import (
	"bufio"
	"fmt"
	"os"
)
func main() {
	filePath := "E:\\学习\\Go\\src\\Go_code\\public\\abc.txt"
	file, err := os.OpenFile(filePath, os.O_WRONLY|os.O_CREATE, 0666)
	if err != nil {
		fmt.Printf("open file err = %v", err)
		return
	}
	// 及时关闭文件
	defer file.Close()
	str := "Hello,Gardon\n"
	// 写入时，使用带缓存的*writer
	writer := bufio.NewWriter(file)
	for i := 0; i < 5; i++ {
		writer.WriteString(str)
	}
	// 因为writer是带缓存的，因此在调用writeString方法时，内容是先写入缓存的，所以需要调用Flush方法
	// 将带缓存的数据真正写入到文件中，否则文件会没有数据
	writer.Flush()
	fmt.Println()
}
```

将一个文件的内容读出来写入另外一个文件，两个文件都已存在

```go
package main
import (
	"fmt"
	"io/ioutil"
)
func main() {
	filePath1 := "E:\\学习\\Go\\src\\Go_code\\public\\abc.txt"
	filePath2 := "E:\\学习\\Go\\src\\Go_code\\public\\kkk.txt"
	content, err := ioutil.ReadFile(filePath1)
	if err != nil {
		fmt.Println("read file err =", err)
		return 
	}
	ioutil.WriteFile(filePath2, content, 0777)
}
```

判断文件是否存在 os.Stat() 如果存在返回文件信息

### 拷贝文件

```go
package main
import (
	"bufio"
	"fmt"
	"io"
	"os"
)
func main() {
	filePath1 := "E:\\学习\\Go\\src\\Go_code\\public\\2.jpg"
	filePath2 := "E:\\学习\\Go\\src\\Go_code\\public\\abc.jpg"
	file1, _ := os.OpenFile(filePath1, os.O_RDWR, 0666)
	file2, _ := os.OpenFile(filePath2, os.O_RDWR|os.O_CREATE, 0666)
	defer file1.Close()
	defer file2.Close()
	reader := bufio.NewReader(file1)
	writer := bufio.NewWriter(file2)
	written, err := io.Copy(writer, reader)
	writer.Flush()
	if err != nil {
		fmt.Println("file copy err =", err)
		return
	}
	fmt.Println(written)
}
```

### 命令行参数的基本使用

```go
fmt.Println("命令行的参数有", len(os.Args))
// 遍历就可以获得命令行的所有输入参数
for _, val := range os.Args {
	fmt.Println(val)
}
```

### flag包解析命令行参数

```go
package main
import (
	"fmt"
	"flag"
)
func main() {
	var user string
	var pwd string
	var host string
	var port string
    &user 就是接受用户命令行中输入的-u后面的参数值
    "u" 就是 -u 指定参数
    "" 默认值
    "用户名默认为空" 说明
	flag.StringVar(&user, "u", "", "用户名默认为空")
	flag.StringVar(&pwd, "p", "", "密码默认为空")
	flag.StringVar(&host, "h", "localhost", "主机名，默认是localhost")
	flag.StringVar(&port, "port", "3306", "默认端口号为3306")
	flag.Parse()
	fmt.Printf("user=%v, pwd=%v, host=%v, port=%v", user, pwd, host, port)
}
```

### json序列化和反序列化操作

#### 序列化操作Marshal

```go
package main
import (
	"encoding/json"
	"fmt"
)
type monster struct {
	Name     string `json:"name"`
	Age      int    `json:"age"`
	Birthday string `json:"birthday"`
	Sal      int    `json:"sal"`
	Skill    string `json:"skill"`
}
func main() {
	var sli = []int{1, 2, 3, 4, 5}
	jsonSli, err := json.Marshal(sli)
	if err != nil {
		fmt.Println("filed err =", err)
		return
	}
	fmt.Println(jsonSli)
	var person = map[string]interface{}{"name": "红孩儿", "age" : 20, "address": "洪崖洞"}
	jsonPer, err := json.Marshal(person)
	if err != nil {
		fmt.Println("err =", err)
		return
	}
	fmt.Printf("%s\n", jsonPer)
	var cow = monster{"牛魔王", 2000, "100-100", 8000, "牛魔拳"}
	jsonCow, err := json.Marshal(cow)
	if err != nil {
		fmt.Println("err =", err)
		return
	}
	fmt.Printf("%s", jsonCow)
	fmt.Println()
}
```

结构体和map都是转换成JavaScript对象格式，map切片转换成对象数组，普通数据格式就还是转换成普通数据格式，转换普通数据格式没有意义，结构体字段必须大写

#### 反序列化操作Unmarshal

```go
package main
import (
	"fmt"
	"encoding/json"
)
type monster struct {
	Name     string `json:"monster_name"`
	Age      int    `json:"monster_age"`
	Birthday string `json:"monster_birthday"`
	Sal      int    `json:"monster_sal"`
	Skill    string `json:"monster_skill"`
}
func main() {
	str := `{"monster_name":"牛魔王","monster_age":2000,
	"monster_birthday":"100-100","monster_sal":8000,"monster_skill":"牛魔拳"}`
	var monster1 monster
	err := json.Unmarshal([]byte(str), &monster1)
	if err != nil {
		fmt.Println("err =", err)
		return
	}
	fmt.Println(monster1)
}
```

在反序列化一个json字符串时，要确保反序列化后的数据类型和原来的序列化前后的数据类型一致

## 单元测试

Go语言自带有一个轻量级的测试框架testing和自带的go test命令来实现单元测试和性能测试，testing测试框架和其他语言中的测试框架类型，可以基于这个框架写针对相应函数的测试用例，也可以基于该框架写相应的压力测试用例。通过单元测试可以解决如下问题：

1. 确保每个函数是可运行的，并且运行结果是正确的
2. 确保写出来的代码性能是好的
3. 单元测试能及时的发现程序设计或实现的逻辑错误，使问题及早暴露，便于问题的定位解决，而性能测试的重点在于发现程序设计上的一些问题，让程序能够在高并发的情况下还能保持稳定

原理是testing框架，会把xxx_test.go的文件引入，main里面调用TestXxx函数，必须是Test开头

### 入门总结

1. 测试用例文件名必须以 _test.go 结尾，比如cal_test.go，不是固定的

2. 测试用例的函数必须以Test开头，一般来说就是Test+被测试的函数名，比如TestAddUpper

3. TestAddUpper(t *testing.T) 的形参类型必须是 *testing.T

4. 一个测试用例文件中可以有多个测试用例函数，比如TestAddUpper, TestSub

5. 运行测试用例指令

    1. cmd > go test 如果运行正确，无日志，错误时，会输出日志。
    2. cmd > go test -v 运行正确或是错误时，都会输出日志

6. 当出现错误时，可以使用t.Fatalf来格式化输出错误信息，并退出程序

7. t.Logf 方法可以输出相应的日志

8. 测试用例函数，并没有放在main函数中，也执行了，这就是测试用例的方便之处

9. PASS 表示测试用例运行成功，FALL 表示测试用例运行失败

10. 测试单个文件，一定要带上被测试的原文件

    go test -v cal_test.go

11. 测试单个方法

    go test -v -run TestAddUpper

## goroutine和channel

### 进程和线程的说明

1. 进程就是程序在操作系统中的一次执行过程，是系统进行资源分配和调度的基本单位
2. 线程是进程的一个执行实例，是程序执行的最小单元，它是比进程更小的能独立运行的基本单位
3. 一个进程可以创建和销毁多个线程，同一个进程中的多个线程可以并发执行
4. 一个程序至少有一个进程，一个进程至少有一个线程

### 并发和并行

1. 多线程程序在单核上运行，就是并发
2. 多线程程序在多核上运行，就是并行

#### 并发

​	并发：因为是一个在一个CPU上，比如有10个线程，每个线程执行10毫秒(进行轮询操作)，从人的角度来看，好像这10个线程都在运行，但是从微观上看，在某一个时间点看，其实只有一个线程在执行，这就是并发

#### 并行

​	并行：因为是在多个CPU上(比如有10个CPU)，比如有10个线程，每个线程执行10毫秒(各自在不同CPU上执行)，从人的角度来看，这10个线程都在执行，但是从微观上看，在某一个时间点上，也**同时**有10个线程在执行，这就是并行

### Go协程和Go主线程

1. Go主线程(有程序员直接称为线程/也可以理解成进程)，一个Go线程上，可以有多个协程，可以这样理解，协程就是轻量级的线程
2. **Go协程的特点**
    1. 有独立的栈空间
    2. 共享程序堆空间
    3. 调度由用户控制
    4. 协程是轻量级的线程

```go
package main
import (
	"fmt"
	"time"
)
func test() {
	for i := 0; i < 10; i++ {
		fmt.Println("Hello, World", i)
		time.Sleep(time.Second)
	}
}
func main() {
	go test() // 开启协程
	for i := 0; i < 10; i++ {
		fmt.Println("Hello, Golang", i)
		time.Sleep(time.Second)
	}
}
```

### 快速入门小结

1. 主线程是一个物理线程，直接作用在CPU上的。是重量级的，非常耗费CPU资源。
2. 协程从主线程开启的，是轻量级的线程，是逻辑态。对资源消耗相对小
3. Golang的协程机制是重要的特点，可以轻松的开启上万个协程。其他编程语言的并发机制是一般基于线程，开启过多的线程，资源耗费大，这里就突显Golang在并发上的优势了

### MPG模式

1. M：操作系统的主线程(是物理线程)
2. P：协程执行需要的上下文
3. G：协程

### 设置Golang运行的CPU数

```go
package main
import (
	"fmt"
	"runtime"
)
func main() {
	cpuNum := runtime.NumCPU()
	fmt.Println("cpuNum =", cpuNum)
	runtime.GOMAXPROCS()  // 1.8以后的版本都用不上
}
```

## channel管道 

### 解决不同goroutine之间的通信

1. 全部变量的互斥锁

    ```go
    package main
    import (
    	"fmt"
    	"sync"
    	"time"
    )
    var (
    	myMap = make(map[int]uint64)
    	// 声明一个全局的互斥锁
    	lock sync.Mutex
    )
    func test(n int) {
    	lock.Lock()
    	var sum uint64 = 1
    	for i := 1; i <= n; i++ {
    		sum *= uint64(i)
    	}
    	myMap[n] = sum
    	lock.Unlock()
    }
    func main() {
    	for i := 1; i <= 30; i++ {
    		go test(i)
    	}
    	time.Sleep(time.Second * 5)
    	lock.Lock()
    	for i, v := range myMap {
    		fmt.Printf("myMap[%d] = %d\n", i, v)
    	}
    	lock.Unlock()
    }
    ```

2. 使用管道channel

### channel介绍

1. channel本质就是一个数据结构-队列
2. 数据是先进先出[FIFO： first in first out]
3. 线程安全，多goroutine访问时，不需要加锁，就是说channel本身就是线程安全的
4. channel是有类型的，一个string的channel只能存放string类型数据

### 定义/声明channel

var 变量名 chan 数据类型

1. channel是引用类型
2. channel必须初始化才能写入数据，即make后才能使用
3. 管道是有类型的，intChan只能写入 int类型

```go
package main
import (
	"fmt"
)
func main() {
	var intChan chan int
	intChan = make(chan int, 3)
	fmt.Printf("intChan 的值 = %v, intChan 本身的地址 = %v\n", intChan, &intChan)
	// 向管道写入数据
	intChan <- 10
	num := 211
	intChan <- num
	intChan <- 20
	// 读数据
	var n2 int
	n2 = <- intChan 
    <- intChan  // 可以不使用变量接收 直接丢了
	fmt.Println(n2)
}
```

### channel使用注意细节

1. channel中只能存放指定的数据类型
2. channel的数据放满后，就不能再放入了
3. 如果从channel取出数据后，可以继续放入
4. 在没有使用协程情况下，如果channel数据取完了，再取，就会报deadlock

```go
package main
import "fmt"
type cat struct {
	Name string
	Age int
}
func main() {
	var allChan chan interface{}
	allChan = make(chan interface{}, 10)
	cat1 := cat{"tom", 18}	
	cat2 := cat{"tom~", 18}
	allChan <- cat1
	allChan <- cat2
	allChan <- 10
	allChan <- "jack"
	cat11 := (<- allChan).(cat) // 这里需要使用类型断言
	fmt.Printf("cat11 的类型是 %T, cat11.Name = %v", cat11, cat11.Name)
}
```

### channel的关闭

使用内置函数close可以关闭channel，当channel关闭后，就不能再向channel写数据了，但是仍然可以从该channel取数据

### channel的遍历

channel支持for-range的方式进行遍历，注意这两个细节

1. 在遍历时，如果channel没有关闭，则会出现deadlock的错误
2. 在遍历时，如果channel已经关闭，则会正常遍历数据，遍历完后就会退出遍历

### goroutine和channel结合

```go
package main
import (
	"fmt"
)
func putNum(intChan chan int) {
	for i := 1; i <= 20000; i++ {
		intChan <- i
	}
	close(intChan)
}
func primeNum(intChan chan int, resChan chan int, exitChan chan bool) {
	for {
		v, ok := <-intChan
		if !ok {
			break
		}
		flag := true
		for i := 2; i <= v/2; i++ {
			if v%i == 0 {
				flag = false
			}
		}
		if flag {
			resChan <- v
		}
	}
	exitChan <- true
}
func main() {
	intChan := make(chan int, 2000)
	resChan := make(chan int, 10000)
	exitChan := make(chan bool, 4)
	go putNum(intChan)
	for i := 0; i < 4; i++ {
		go primeNum(intChan, resChan, exitChan)
	}
	go func() {
		for i := 0; i < 4; i++ {
			<-exitChan
		}
		close(resChan)
	}()
	for v := range resChan {
		fmt.Printf("%d\t", v)
	}
}
```

### channel使用细节和注意事项

1. channel可以声明为只读或者只写性质
    1. 在开启协程传递管道参数的时候可以设置，保护数据

```go
package main
import (
	"fmt"
)
func main() {
	// 声明可读可写的管道
	var chan1 chan int

	// 声明只写的管道
	var chan2 chan<- int
	chan2 = make(chan int, 2)
	chan2 <- 2
	// num := <-chan2 只写不能读会报错

	// 声明只读的管道
	var chan3 <-chan int
	chan3 = make(chan int, 2)
	// chan3 <- 2 只读不能写
	fmt.Println(chan1, chan2, chan3)
}
```

2. 使用select可以解决从管道取数据的阻塞问题

```go
package main
import (
	"fmt"
)
func main() {
	intChan := make(chan int, 10)
	for i := 0; i < 10; i++ {
		intChan <- i
	}
	strChan := make(chan string, 5)
	for i := 0; i < 5; i++ {
		strChan <- "hello" + fmt.Sprintf("%d", i)
	}
	for {
		select {
		case v := <-intChan:
			fmt.Printf("从intChan取到的数据%d\n", v)
		case v := <-strChan:
			fmt.Printf("从strChan取到数据%s\n", v)
		default:
			fmt.Printf("取不到数据了，不玩了\n")
			return
		}
	}
}
```

3. goroutine中使用recover，解决协程中出现panic，导致程序崩溃

```go
package main
import (
	"fmt"
	"time"
)
func sayHello() {
	for i := 0; i < 10; i++ {
		time.Sleep(time.Second)
		fmt.Println("hello", i)
	}
}
func test() {
    // 这里的map没有make所以会报错，没有加错误处理的话整个程序都会因为这个协程错误退出，
    // 加了之后其他协程不会有影响
	defer func() {
		if err := recover(); err != nil {
			fmt.Println("test() 发生错误", err) 
            // test() 发生错误 assignment to entry in nil map
		}
	}()
	var myMap map[int]string
	myMap[0] = "hello"
}
func main() {
	go sayHello()
	go test()
	time.Sleep(time.Second * 11)
}
```

## 反射

### 基本介绍

1. 反射可以在运行时动态获取变量的各种信息，比如变量的类型(type)，类别(kind)
2. 如果是结构体变量，还可以获取到结构体本身的信息（包括结构体的字段，方法）
3. 通过反射，可以修改变量的值，可以调用关联的方法
4. 使用反射，需要import("reflect")

### 反射重要的函数和概念

1. reflect.TypeOf(变量名)，获取变量的类型，返回reflect.Type类型
2. reflect.ValueOf(变量名)，获取变量的值，返回reflect.Value类型，reflect.Value是一个结构体类型
3. 变量、interface{} 和 reflect.Value是可以相互转换的，这点在实际开发中，会经常使用到

### 反射注意事项和细节说明

1. reflect.Value.Kind获取变量的类别，返回的是一个常量
2. Type是类型，Kind的类别，Type和Kind可能是相同的，也可能是不同的
3. 使用反射的方式获取变量的值(并返回对应的类型)，要求数据类型匹配，比如x是int，那么就应该使用reflect.Value(x).Int()，而不能使用其他的，否则报panic
4. 通过反射来修改变量，注意当使用SetXxx方法来设置需要通过对应的指针类型来完成，这样才能改变传入的变量的值，同时需要使用到reflect.Value.Elem()方法

### 最佳实践

```go
package main
import (
	"fmt"
	"reflect"
)
type monster struct {
	Name  string `json:"name"`
	Age   int    `json:"age"`
	Score float32
	Sex   string
}
func (m monster) Print() {
	fmt.Println("------- start -------")
	fmt.Println(m)
	fmt.Println("-------- end --------")
}
func (m monster) GetSum(n1, n2 int) int {
	return n1 + n2
}
func (m monster) Set(name string, age int, score float32, sex string) {
	m.Name = name
	m.Age = age
	m.Score = score
	m.Sex = sex
}
func testStruc(a interface{}) {
	typ := reflect.TypeOf(a)
	rVal := reflect.ValueOf(a)
	kd := rVal.Kind()
	if kd != reflect.Struct {
		fmt.Println("expect struct")
		return
	}
	// 获取字段总数，用于遍历字段
	num := rVal.NumField()
	fmt.Printf("this struct has %d fields\n", num)
	// 遍历字段
	for i := 0; i < num; i++ {
		fmt.Printf("field %d: 值为=%v\n", i, rVal.Field(i))
		// 获取struct标签，需要通过reflect.Type来获取标签的值
		tagVal := typ.Field(i).Tag.Get("json")
		if tagVal != "" {
			fmt.Printf("field %d: tag为=%v\n", i, tagVal)
		}
	}
	numOfMethod := rVal.NumMethod()
	fmt.Printf("struct has %d method\n", numOfMethod)
	// 方法的排序默认是按照函数名的排序(ASCII)
	rVal.Method(1).Call(nil)

	var params []reflect.Value
	params = append(params, reflect.ValueOf(10))
	params = append(params, reflect.ValueOf(20))
	res := rVal.Method(0).Call(params)
	fmt.Println(res[0].Int())
}
func main() {
	var a = monster{
		Name:  "黄鼠狼",
		Age:   20,
		Score: 30.8,
	}
	testStruc(a)
}
```

## TCP网络编程

### 网络编程的基本介绍

Golang的主要设计目标之一就是面向大规模后端服务程序，网络通信这块是服务端程序必不可少也是至关重要的

网络编程有两种

1. TCP socket编程：是网路编程的主流。之所以叫TCP socket编程，是因为底层是基于tcp/ip协议的
2. b/s结构的http编程：我们使用浏览器去访问服务器时，使用的就是http协议，而http底层依旧是用tcp socket实现的

![image-20200811150133360](C:\Users\48356\Desktop\笔记\image\image-20200811150133360.png)

qq相互通信案例

![image-20200811152310216](C:\Users\48356\Desktop\笔记\image\image-20200811152310216.png)

#### 端口

我们这里指的端口不是物理意义上的端口，而是特指tcp/ip协议中的端口，是逻辑意义上的端口。端口就是通过端口号来标记的，端口号只有整数，范围是从0-65535

1. 0号是保留端口

2. 1-1024是固定端口，又叫有名端口，即被某些程序固定使用，一般程序员不使用

    22：SSH远程登录协议	23：telnet使用	21：ftp使用

    25：smtp服务使用	80：iis使用	7：echo服务

3. 1025 - 65535是动态端口，这些端口程序员可以使用

### tcp socket编程的快速入门

#### 服务端处理流程

1. 监听端口
2. 接受客户端的tcp连接，建立客户端和服务端的链接
3. 创建goroutine，处理该链接的请求（通常客户端通过链接发送请求包）

#### 客户端处理流程

1. 建立与服务端的链接
2. 发送请求数据[终端]，接收服务器返回的结果数据
3. 关闭链接

## Redis

### 基本介绍

1. Redis 是 NoSQL 数据库，不是传统的关系型数据库
2. Redis：REmote Dictionary Server(远程字典服务器)，Redis性能非常高，单机能够达到15w qbs，通常适合做缓存，也可以持久化
3. 是完全开源免费的，高性能的(key/value)分布式内存数据库，基于内存运行并支持持久化的NoSQL数据库，是最热门的NoSQL数据库之一，也称为数据结构服务器
4. 下载地址https://github.com/tporadowski/redis/releases
5. 占用6379端口

5. Redis的启动：双击redis-server.exe

6. 命令文档[redisdoc.com]()

### 基本使用

说明：Redis安装好后，默认有16个数据库，初始默认使用0号库，编号是0...15

1. 添加key-val [set]

    set key value [expiration EX seconds|PX milliseconds] [NX|XX]

2. 查看当前Redis的 所有key [key *]

3. 获取key对应的值 [get key]

    get key

4. 切换Redis数据库 [select index]

5. 查看当前数据库的key-val数量 [dbsize]

6. 清空当前数据库的key-val和清空所有数据库的key-val [flushdb flushall]

### redis的五大数据类型和crud

redis的五大数据类型是：String(字符串)、Hash(哈希)、List(列表)、Set(集合)、zset(sorted set: 有序集合)

#### 字符串

string是redis最基本的类型，一个key对应一个value

string类型是二进制安全的。除普通的字符串外，也可以存放图片等数据

redis中字符串value最大是512M

##### 字符串-crud

**set** set key value 如果存在就相当于修改，不存在则是添加

**get** get key 查找

**del** 删除

**setex** key seconds value 设置key超时，就是在seconds之后消失

**mset** 一次设置一个或多个key-value

**mget** 一次查找一个或多个key

#### Hash(哈希表)

redis Hash 是一个键值对集合，

redis Hash 是一个string类型的field和value的映射表，Hash特别适合用于存储对象

**hset**  hset key field value 如果存在修改，不存在则添加

​	hset user name zhangsan

​	hset user age 30

**hget**  hget key field 查找

**hgetall** hgetall key 查找key的所有字段信息

**hdel** hdel key field 删除key的指定field

**hmset/hmget** 一次设置或获取多个字段

​	hmset key field1 value1 field2 value2 

​	hmget key field1 field2

**hlen** hlen key 返回存储在key中的哈希中包含的字段数

**hexists** hexists key field  查看哈希表key中，给定field是否存在

#### List(列表)

列表是简单的字符串列表，按照插入顺序排序。可以添加一个元素到列表的头部(左边)或尾部(右边)

List本质是个链表，List的元素是有序的，元素的值可以重复

**lpush** lpush key value1 value2 ... 从列表的头部插入数据

**rpush** rpush key value1 value2 ... 从列表的尾部插入数据

**lrange** lrange key start end 0 是第一个， -1 是最后一个 遍历

**lpop** lpop key 从列表头部取走一个元素

**rpop** rpop key 从列表尾部取走一个元素

**lindex** lindex key index 按照索引下标获得元素(从左到右，索引号从0开始)

**llen** llen key 返回列表key的长度，如果key不存在，则key被解释为一个空列表，返回0

如果值全部移除，对应的键也就消失了

#### Set(集合)

redis的Set是string类型的无序集合

底层是HashTable数据结构，Set也是存放很多字符串元素，字符串元素是无序的，而且元素的值不能重复

**sadd** sadd key member1 member2 ... 向集合 key 中添加成员member，如果集合不存在则创建

**smembers** smembers key 取出集合 key 中的所有成员

**sismember** smember key member 判断值是否是集合 key 中的成员 存在返回1 不存在返回0

**srem** srem key member ... 删除集合 key 中的指定成员

### redis连接池

说明：通过Golang 对 redis 操作，还可以通过Redis连接池，流程如下：

1. 实现初始化一定的连接，放入到连接池

2. 当Go需要操作redis时，直接从redis连接池取出连接即可

3. 这样可以节省临时获取redis连接的时间，从而提升效率

4. 核心代码

    ```
    var pool *redis.Pool
    pool = &redis.Pool{
    	MaxIdle: 8, // 最大空闲连接数
    	MaxActive: 0, // 表示和数据库的最大连接数，0表示没有限制
    	IdleTimeout:100, // 最大空闲时间
    	Dial: func() (redis.Conn, error) { // 初始化连接的代码，连接哪个ip的redis
    		return redis.Dial("tcp", "localhost:6379")
    	},
    }
    conn := pool.Get() // 从连接池中取出一个连接
    conn.Close() // 关闭连接池，一旦关闭连接池，就不能从连接池再取出连接
    ```

    

## 经典项目-海量用户即时通讯系统

### 开发流程

需求分析 -> 设计阶段 -> 编码实现 -> 测试阶段 -> 实施

### 需求分析

1. 用户注册
2. 用户登录
3. 显示在线用户列表
4. 群聊(广播)
5. 点对点聊天
6. 离线留言

## 数据结构与算法

### 数据结构的介绍

1. 数据结构是一门研究算法的学科，自从有了编程语言也就有了数据结构，学好数据结构可以编写出更加漂亮，更加有效率的代码
2. 要学好数据结构就要多多考虑如何将生活中遇到的问题，用程序去实现解决
3. 程序 = 数据结构 + 算法

### 稀疏数组sparsearray

#### 五子棋问题

当一个数组中大部分元素为0，或者为同一个值的数组中，可以使用稀疏数组来保存该数组。

稀疏数组的处理方法是：

1. 记录数组一共有几行几列，有多少个不同的值
2. 把具有不同值的元素的行列及值记录在一个小规模的数组中，从而缩小程序的规模

![image-20200905204259393](C:\Users\48356\Desktop\笔记\image\image-20200905204259393.png)

（加总行和总列是多少，默认值是多少）

#### 应用实例

1. 使用稀疏数组，来保存类似前面二位数组（棋盘、地图等等）
2. 把稀疏数组存盘，并且可以重新恢复原来的二位数组