# 模块

## time

``` go
  time.Unix() // 两个参数

  // 时间戳 与 格林威治时间 的转化
  unixTime := 1587894706
  timeO := time.Unix(int64(unixTime), 0)
  var str = timeO.Format("2006-01-02 03:04:05")
  t2 := "2019-01-08 ß13:50:30"
  timeTemplate := "2006-01-02 15:04:05"
  stamp,_ =time.ParseInLocation(timeTemplate,t2,time.Local)
  // stamp     "2020-04-26 15:38:04 +0800 CST"
  // stamp.Unix()  1546926630

  
  // 时间间隔 time中自己定义的常量
  time.Millisecond    // 1ms
  time.Second      // 1s
  time.Minute
  time.Hour

  // 时间操作函数  时间倒退 & 时间前进
  // add & sub 关键字
  now := time.Now()
  // time.Now().Unix()
  fature := now.Add(time.Hour)    // 前进一小时

  // 定时器
  ticker := time.NewTicker(time.Second)
```

## fmt

%v    打印变量值

%T    打印类型

%t    打印布尔值

%d    打印整数

%b    打印二进制

%c    打印asicII 码

%s    打印字符串

 

 

## math

// 开二次方，参数为被开方数

Math.Sqrt(9)       

 

 

## math/rand    随机数

// 返回 0-100的随机整数

rand.Intn(100)

 

// 返回 0-1.0的浮点数

Rand.Float64()

 

//要让伪随机数生成器有确定性，可以给它一个明确的种子

s1 := rand.NewSource(42)
 r1 := rand.New(s1)

 

 

## strconv

 

 

## runtime

num := runtime.NumCPU()    // 获取电脑的cpu个数

runtime.GOMAXPROCSS( num - 1) // 设置使用几个cpu

 

## robotgo

```go
// go get github.com/go-vgo/robotgo
import "github.com/go-vgo/robotgo"


// 监控键盘按键
ok := robotgo.AddEvents("q",)
if ok {
  fmt.Println("you press…","q")
}
mleft := robotgo.AddEvents("mleft",)
if mleft {
  fmt.Println("you press…","mouse left button")
}

// 操作键盘按键
robotgo.KeyTap("a")
robotgo.KeyTap("a")

robotgo.MoveMouse(100,100)
robotgo.MouseClick("left", false)  // 不传参默认左键
x,y := robotgo.GetMousePos()    // 鼠标坐标
```

# 服务器

```go
// 服务器请求  http_request
package main
import (
    "fmt"
    "net/http"
        "io/ioutil"
)
func get() {
    res, err := http.Get("http://httpbin.org/get")
    if err != nil {
       panic(err)
    }
    defer res.Body.Close()
    content,err := ioutil.ReadAll(res.Body)
    if err != nil {
       panic(err)
   }
   // string(content)    将其转换为字符串
   fmt.Printf("%s",content)
}
// 第二个参数必须加上，第三个
func post() {
    res,err := http.post("http://httpbin.org/post","application/x-www-formurlencoded",nil)
    if err != nil {
       panic(err)
    }
    defer res.Body.Close()
    content,error := ioutil.ReadAll(res.Body)
    if error != nil {
        panic(error)
    }
    fmt.Printf(string(content))
}
func main() {
     get()
     post()
}

// 关于put del 请求 ====================
func put() {
   request,err :=http.NewRequest(http.MethodPut,"http://httpbin.org/put",nil)
   if err != nil {
      panic(err)
   }
}

// 代码封装
// 设置请求参数 ==========================
func requestByParams() {
  request, err := http.NewRequest(http.MethodGet,"http://httpbin.org/get",nil)
  if err != nil {
    panic(err)
  }
  params := make(url.Values)
  params.Add("name","Gagne")
  params.Add("age","23")
  request.URL.RawQuery = params.Encode()
  r,err := http.DefaultClient.Do(request)
  if err != nil {
    panic(err)
  }
  printBody(r)
}
 
// 设置请求头 ===================
func requstByHead() {
  request, err := http.NewRequest(http.MethodGet,"http://httpbin.org/get",nil)
  if err != nil {
    panic(err)
  }
  request.Header.Add("user-agent","chrome")
  r, err := http.DefaultClient.Do(request)
  if err != nil{
    panic(err)
  }
  printBody(r)
}

```



