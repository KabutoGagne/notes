# 数据结构

简单数据类型(值类型)

整型int

浮点型floor

字符串string

字符类型 byte&rune

布尔boolean

数组array

引用数据类型(栈类型)

切片slice

map类型

接口interface

结构体

### 整型

有符号整型按长度分为: int8 int16 int32 int64

无符号整型: unit8 unit16 uint32 uint64

int8     -2^7~2^7-1 (127) uint8 0~2^8-1 1字节

int16    -2^15~2^15-1 uint16 0~2^16-1 2字节

int32    -2^31~2^31-1 uint8 0~2^32-1 4字节

int64    -2^63~2^63-1 uint8 0~2^64-1 8字节

类型不同不能相加,需要进行转换 int64(a1) + a2

数字字面语法 %d 表示10进制输出 %b表示二进制 %o八进制

 

 

### 布尔类型

0，1无法转换为 false 和 true

 

 

### 字符串类型

转义字符 \r 回车 \n 换行符 \t 制表符 \' 单引号

 

len(Str)    // 获取该字符串的长度          

fmt.Sprintf("%v %v",Str1,Str2)    // 字符串拼接       

strings.Split(Str,"")    // 返回 字符串分割而成的数组     

strings.Join(Arr,"")    // 返回 数组用 连接而成的字符串 

strings.HasPrefix(Str1,Str2)    // 返回布尔,Str1开头是否包含Str2 

strings.HasSutfix(Str1,Str2)    

strings.Index(Str1,Str2)    // 返回数值,Str2在Str1第几

 

### 字符类型

byte类型,即unit8类型,转换为ASCII码, 单个字母

rune类型,代表了utf-8标准的字样,如 一个汉字或者假名

打印出来会被编译,所以要用格式化输出,%c来原样输出

 ``` go
a := "xorld"
byteA := []byte(a)   // 字符型切片
byteA[0] = 'w'
fmt.Printf("%c",byteA)    // [w o r l d]

b := "地界"
runeB := []rune(b)   // 字符型切片
runeB[0] = '世'
fmt.Printf("%c",runeB)    // [世 界]

// 字符 转字符串
fmt.Println(string(runeB))
 ```





### 数组

 ``` golang
// 初始化数组,定义和赋值    

var a = [3]int{1,2,3}    
var b = [...]int{1,2,3}     // 数组长度是动态的了
var c = [...]int{0:1,1:9,5:9}    // len(c) 6

 

var d [3]int   // 定义了数组的长度

// 二维数组        多维数组的表示
var arr = [3][2]string{
{"aaa","bbb"},
{"ccc","ddd"},
{"eee","fff"}
}

 

// 遍历数组
var sum int = 0
for i := 0; i < len(a); i++ {
 sum += a[i]
}
 ```



### 切片

 ``` go
slice := make([]int, 3, 5)

b := slice[:]    // 获取所有值
c ：= slice[1:3] // 获取第一位到第四位    切片的切片

// 扩容  对象 = append(对象,值) 元素往后加一，长度和容量都增加, x2
// 深拷贝    copy(对象切片, 新定义的空切片)
// 删除元素 对象 = append()
// a = append(a[:2], a[3:]...) 
// 获取前两项元素 和 第四项往后的元素,去掉第三个
 ```





### map类型

``` go
// 创建map类型

var userInfo = make(map[string]string)
/* var userInfo = map[string]string{
 \* "username" : "aaa",
 \* "userage" : "20",
 \* }
 */

userInfo["username"] = "aaa"
userInfo["userage"] = "20"

// curd操作 增删改查
// 增加 就是新定义一个，修改也是直接重赋值
// 查找
value,ok := userInfo["username"]   // "aaa",true
// 删除
delete(userInfo，"username")

// map类型的切片
userInfo := make([]map[string]string,3,3)
// 打印  map[age:20 name:aa]
```





### 接口

接口只是用来规范要定义的内容

 ``` go
type usber interface {
  start()
  stop()
  off()
}


type Person struct { ... }
func (p Person) start() { ... }

func main() {
  p := Person{
​    name:"kabuto",
  }
  var p1 usber    // 接口是个类型，再让他等于struct
  p1 = p
}

// 空接口,任何类型都可以接受
type A inerface{}
// 定义一个空接口的变量 可以赋值给任何类型的值， 多用于函数参数 interface{}
// 类型断言
v,ok := a.(string)
if ok {
  fmt.Printf("string类型，值%v",v)
} else {
  fmt.Printf("不是string类型，值%v",v)
}

switch a.(type) {
  case int:
​      fmt.Printf("int类型")
  case string:
​      fmt.Printf("string类型")
  case bool:
​      fmt.Printf("bool类型")
  default:
​      fmt.Printf("传入错误")
}
 ```





 

### 结构体struct

 ``` go
// 结构体 定义 & 创建
type Books struct {
  title string
  author string
  subject string
  book_id int
}

 
func main() {
  // 创建一个新的结构体
  fmt.Println(Books{"Go 语言", "wsds", "教程", 6495407})

  // 也可以使用 key => value 格式
   fmt.Println(Books{"Go 语言", "wsds", "教程", 6495407})

  // 忽略的字段为 0 或 空
  fmt.Println(Books{"Go 语言", "wsds", "教程", 6495407})

  // 创建一个实例体
  var Book1 Books
  Books1.title ="Go 语言"
  Book1.author = "wwwsassa"
  Book1.subject = "Go教程"
   Book1.book_id = 6495407

  // 第二种实例化的方法
  var p2 =new(Person)
  // 第三种
  p3 := &person{}
  // 第四种
  var p4 =person{
​    name:"kabuto",
​    age:18,
  }
}
 ```



# 函数

### 参数&返回值

``` go
/*
 \* 如果返回值有多个,可以用括号括起来
 \* 一个函数的定义不能在另一个函数中， 可以在另一个函数中调用执行
*/
func sumA(a int, b int) int {
 sum := a + b;
 return sum
}
func sumB(a ... int) int {
 for _,v = range a {
​    sum += v
 }
 return sum
}
```





 

 

 

 

### 语句 defer

延迟执行，该语句或者该函数会在return 后面执行

``` go
func CopyFile(dstName, srcName string) (written int64, err error) {
 src, err := os.Open(srcName)
 if err != nil {
 return
 }
 defer src.Close()
 dst, err := os.Create(dstName)
 if err != nil {
 return
 }
 defer dst.Close()
 return io.Copy(dst, src)
 }

// 当defer被声明时，其参数就会被实时解析

func a() {
 i := 0
 defer fmt.Println(i) //输出0，因为i此时就是0
 i++
 defer fmt.Println(i) //输出1，因为i此时就是1
 return
 }

// defer执行顺序为先进后出

func b() {
 for i := 0; i < 4; i++ {
  defer fmt.Print(i)
 }
}  // 3210
```



