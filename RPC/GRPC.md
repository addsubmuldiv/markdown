# GRPC

## 对于 java

- 在maven中引入 protobuf 的依赖，包括代码生成插件
- 将 .proto 文件放在 main/src/proto 目录下
- 然后在maven中运行代码生成命令即可，有俩，分别对应 protobuf 和 grpc，一个是 compile, 一个是 compile-custom

### 在生成之后

- 主要是实现 xxxxGrpc 里面的方法





# maven索引更新

- 配置阿里云镜像，nexus的，或者直接`<mirrorof>*</mirrorof>`

- 然后直接在 idea 里面更新即可

