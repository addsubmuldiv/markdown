# Protobuf

## 定义消息

```protobuf
/* SearchRequest represents a search query, with pagination options to
 * indicate which results to include in the response. */

message SearchRequest {
  required string query = 1;
  optional int32 page_number = 2;  // Which page number do we want?
  optional int32 result_per_page = 3;  // Number of results to return per page.
  repeated int32 aa = 4 [packed=true]; // repeated的后边加上方框里的东西，编码优化
}
```

数字表示在二进制文件中的索引，1~15俩字节，16开始4字节

## 保留字段

```protobuf
message Foo {
  reserved 2, 15, 9 to 11; // 要删掉字段，就直接reserved，避免以后更新出错
  reserved "foo", "bar";
}
```

## 编译后生成的是？

- 对于java，编译器生成一个 .java 文件，其中包含每个消息类型的类，以及用于创建消息类实例的特殊 Builder 类。
- 对于Python， 编译器生成一个模块，其中包含 .proto 中每种消息类型的静态描述符，然后与元类一起使用以在运行时创建必要的 Python 数据访问类。

## 消息默认值

```protobuf
optional int32 result_per_page = 3 [default = 10];
```

##　枚举

```protobuf
message SearchRequest {
  required string query = 1;
  optional int32 page_number = 2;
  optional int32 result_per_page = 3 [default = 10];
  enum Corpus {
    UNIVERSAL = 0;
    WEB = 1;
    IMAGES = 2;
    LOCAL = 3;
    NEWS = 4;
    PRODUCTS = 5;
    VIDEO = 6;
  }
  optional Corpus corpus = 4 [default = UNIVERSAL];
}
```

枚举还支持别名

## 套娃消息

```protobuf
message SearchResponse {
  repeated Result result = 1;
}

message Result {
  required string url = 1;
  optional string title = 2;
  repeated string snippets = 3;
}
```

被套娃的消息如果在别的文件，可以 **import** 进来

## 套娃定义消息

```protobuf
message Outer {       // Level 0
  message MiddleAA {  // Level 1
    message Inner {   // Level 2
      required int64 ival = 1;
      optional bool  booly = 2;
    }
  }
  message MiddleBB {  // Level 1
    message Inner {   // Level 2
      required int32 ival = 1;
      optional bool  booly = 2;
    }
  }
}
```

## 扩展一个已经在用的消息的原则

。。。

## 保留一些索引用于扩展

```protobuf
message Foo {
  // ...
  extensions 100 to 199;
}
```

## oneof

```protobuf
message SampleMessage {
  oneof test_oneof {
     string name = 4;
     SubMessage sub_message = 9;
  }
}
```

类似于C语言里面的 Union，**oneof** 不能是 **required, optional, repeated** 的

## 定义map

```protobuf
map<key_type, value_type> map_field = N;
```

- **map** 不能是 **required, optional, repeated** 的
- 顺序不一定

## package

使用package 来避免命名冲突

```protobuf
package foo.bar;
message Open { ... }
```

```protobuf
message Foo {
  ...
  required foo.bar.Open open = 1;
  ...
}
```

## 定义 **Service**

```protobuf
service SearchService {
  rpc Search(SearchRequest) returns (SearchResponse);
}
```

## Option

```protobuf
java_package // 用于生成java代码的时候，生成包名良好的JAVA代码
java_outer_classname // 设置生成的包装类名
java_multiple_files // 是否拆分成多个文件
optimize_for // 生成代码的三种级别，调低可以自己实现
deprecated // 表示新代码不应该再用了
java_generic_services // 表示生成服务，但是这不绑定到任何一个rpc系统
```

# 生成的 JAVA 代码解析

## package

如果没设定 **java_package**，就会按着 文件头的 来生成包

```protobuf
package foo.bar;	// 没设定就是这
option java_package = "com.example.foo.bar";  // 设定了就是这
```

