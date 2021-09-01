# Flink-Question-OnAir
all flink question and solution

## Q1. Flink SQL 创建Kafka表时，用IDE跑是正常，打包后用flink run报错
报错信息：
-  Cannot discover a connector using option: 'connector'='kafka'
-  Could not find any factory for identifier 'kafka' that implements 'org.apache.flink.table.factories.DynamicTableFactory' in the classpath.

> 原因：

> 解决方案：
> 
> 
> 
> 
> 
> 


## Q2. Flink SQl打包运行报错
报错信息：
org.codehaus.janino.CompilerFactory cannot be cast to org.codehaus.commons.compiler.ICompilerFactory

> 原因：在flink 1.10 之后，配置文件中 classloader.resolve-order 参数默认是 child-first

> 解决方案： 
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