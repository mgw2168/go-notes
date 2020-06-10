# go-notes
go 语言学习笔记--备忘！

### 1.安装

#### Mac:

[下载地址](https://dl.google.com/go/go1.14.4.darwin-amd64.pkg)  双击，一路下一步，安装成功！！

#### 在`.bash_profile` 中配置环境变量

```go
export GOROOT=$HOME/go  
export GOPATH=$HOME/mydata/mygo
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```

### 2.GOPATH与工作空间：

​	`$GOPATH`  约定有三个子目录：

* src 存放源代码
* pkg 存放编译后生成的文件(如: .a)
* bin 存放编译后生成的可执行文件

#### 编译安装

2种方式:

* 代码完成后在任意的目录执行 `go install ${package_name}` 
* 进入对应包的目录，进行 `go install` 

```go
➜  src go install quant //执行此命令
➜  src tree ../
../
├── bin
├── pkg
│   └── darwin_amd64
│       └── quant.a
└── src
    ├── quant
    │   └── quant.go
    └── hello
        └── main.go
```

可以看到生成了 .a 结尾的应用包

#### 编译

在对应目录，执行 `go build` 

```
➜  hello ls
main.go hello
```

生成了可执行文件, 然后 ./sqrt 即可输出结果

- 如果是普通包，就像上面编写的 `quant` 包那样，当执行`go build`之后，它不会产生任何文件。如果需要在`$GOPATH/pkg`下生成相应的文件，那就得执行`go install`。
- 如果是`main`包，当你执行`go build`之后，它就会在当前目录下生成一个可执行文件。如果你需要在`$GOPATH/bin`下生成相应的文件，需要执行`go install`，或者使用`go build -o 路径/a.exe`。
- 如果某个项目文件夹下有多个文件，而你只想编译某个文件，就可在`go build`之后加上文件名，例如`go build a.go`；`go build`命令默认会编译当前目录下的所有go文件。
- 你也可以指定编译输出的文件名。例如上面的`quant`应用，我们可以指定`go build -o quant.exe`，默认情况是你的package名(非main包)，或者是第一个源文件的文件名(main包)。

#### 安装

```go
➜  sqrt go install  // 会在bin目录下生成sqrt的可执行文件
➜  sqrt tree ../../
../../
├── bin
│   └── quant
├── pkg
│   └── darwin_amd64
│       └── quant.a
└── src
    ├── quant
    │   └── quant.go
    └── hello
        └── main.go
```

### 3.go 常用命令

* go build

见上面

* go install 

>  这个命令在内部实际上分成了两步操作：第一步是生成结果文件(可执行文件或者.a包)，第二步会把编译好的结果移到`$GOPATH/pkg`或者`$GOPATH/bin`。

* go clean 

用来移除当前源码包和关联源码包里编译生成的文件

可以用来清除编译文件，然后使用git提交源码文件

* go fmt 格式化代码

`go fmt <filename>.go`  更多参考 [gofmt](https://docs.huihoo.com/go/golang.org/cmd/gofmt/index.html) 

* go get

该命令用来动态获取远程代码包，支持的有BitBucket、GitHub、Google Code和Launchpad。主要分两步：

1. 下载源码
2. 执行go install

* go test

执行测试文件，自动读取源码目录下 *_test.go 文件，生成并运行测试用的可执行文件

* go tool
  * `go tool fix .` 用来升级旧代码到新版本的，如 go1之前的版本升级到go1
  * `go tool vet directory|files` 用来分析当前的代码是否有错误

* 其他命令

```go
go version 查看go当前的版本
go env 查看当前go的环境变量
go list 列出当前全部安装的package
go run 编译并运行Go程序
```



