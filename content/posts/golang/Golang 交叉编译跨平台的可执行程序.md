Golang是编译形语言，但是对比c在跨平台角度来讲并不需要代码级的判断，因为Go 语言源代码的 [`src/cmd/compile/internal`](https://github.com/golang/go/tree/master/src/cmd/compile/internal) 目录中包含了很多机器码生成相关的包，不同类型的 CPU 分别使用了不同的包生成机器码。

通过支持交叉编译，你可以在大部分主流机器上开发，然后编译生成其他平台或cpu架构下的可执行程序。

## 交叉编译依赖下面几个环境变量

### $GOOS

 要运行的目标平台操作系统

1. mac：`GOOS="darwin"`
2. linux：GOOS="linux"
3. windows：`GOOS="windows"`

### $GOARCH

要运行的目标平台处理器架构

1. 386：`GOARCH="386"`

2. amd64：`GOARCH="amd64"`

3. arm：`GOARCH="arm64"`

   

## 跨平台编译步骤

1. 确定当前go环境的 GOARCH 和 GOOS

   ```shell
   $ go env | grep  -E 'GOOS|GOARCH'
   GOARCH="arm64"
   GOOS="darwin"
   ```

2. 确定当前编译环境的处理器架构，Linux mac 都可以用uname -a 来查看

3. 编译对应平台下的执行文件

   Mac 下编译 Linux 和 Windows 64位可执行程序

   ```shell
   CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build main.go
   CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build main.go
   ```