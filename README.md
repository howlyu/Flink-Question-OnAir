# Flink-Question-OnAir
all flink question and solution

## Q1. Flink SQL 创建Kafka表时，用IDE跑是正常，打包后用flink run报错
报错信息：
-  Cannot discover a connector using option: 'connector'='kafka'
-  Could not find any factory for identifier 'kafka' that implements 'org.apache.flink.table.factories.DynamicTableFactory' in the classpath.

> **原因**：因为Flink 加载 table Factory 使用的时SPI机制，而正常的flink jar包是不包含META-INF.services 路径的，需要自己去添加

> **解决方案**
> 链接：[Could-not-find-any-factory-for-identifier-kafka-td5414](http://apache-flink.147419.n8.nabble.com/Could-not-find-any-factory-for-identifier-kafka-td5414.html)
> ![resources增加META-INF.servers](https://img2020.cnblogs.com/blog/1892627/202103/1892627-20210303120841195-1010498336.png)
> 


## Q2. Flink SQl打包运行报错
报错信息：
org.codehaus.janino.CompilerFactory cannot be cast to org.codehaus.commons.compiler.ICompilerFactory

> **原因**：在flink 1.10 之后，配置文件中 classloader.resolve-order 参数默认是 child-first

> **解决方案**： 
> 方案1： 把 flink-conf.yaml 文件中 设置classloader.resolve-order： parent-first
> 
> 方案2： pom文件中设置 scope = provided,然后把flink-table-planner-blink 的jar包拷贝的 FLINK_HOME/lib目录中
> ```
> <dependency> 
>   <groupId>org.apache.flink</groupId>
>   <artifactId>flink-table-planner-blink_2.11</artifactId>
>   <version>${flink.version}</version>
>   <scope>provided</scope>
> </dependency>
> ```
> 
> 