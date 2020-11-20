1、package golang.org/x/net/html/...: unrecognized import path "golang.org/x/net/html": https fetch: Get "https://golang.org/x/net/html?go-get=1": dial tcp 216.239.37.1:443: i/o timeout



问题：golang由google公司开发，一些服务器域名被国内屏蔽

解决：1）vpn，设置代理google.golang.com

2)git clone && go install

这种方法适合Go语言版本在1.11以下，不支持Go module功能，可以通过如下方式github.com将对应项目克隆到本地$GOPATH/src目录下

  ```
cd %GOPATH/src
git clone https://github.com/grpc/grp-go.git google.golang.org/grpc

此外，还要克隆google.golang.com/grpc依赖的包
git clone https://github.com/golang/net.git golang.org/x/net
git clone https://github.com/golang/text.git golang.org/x/text
git clone https://github.com/google/go-genproto.git google.golang.org/genproto

接下来，通过如下命令安装Golang protobuf包
go get -u -v github.com/golang/protobuf/proto
go get -u -v github.com/golang/protobuf/protoc-gen-go

最后通过go install命令手动安装这个扩展包
go install google.golang.org/grpc
  ```

3）go module

对于go 1.11及以上版本，支持Go module功能，Go Module是一个新型的包管理工具，我们创建一个新项目，比如helloworld，并且在该项目下运行如下命令来初始化Go Module

```
go mod init helloworld
```

4）4、go module & GOPROXY

https://xueyuanjun.com/post/19887.html





















