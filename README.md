# document
nacos for windows

1.下载
nacos GitHub下载安装服务：https://github.com/alibaba/nacos/releases
assets 四个包  
  nacos-server-2.0.0-ALPHA.2.tar.gz 已编译Linux和macOS格式
  nacos-server-2.0.0-ALPHA.2.zip windows版本
  Source code（zip） windows版本源码
  Source code （tar.gz) Linux和macOS格式源码
  
  部署模式
Nacos支持三种部署模式
单机模式 - 用于测试和单机试用。
集群模式 - 用于生产环境，确保高可用。
多集群模式 - 用于多数据中心场景。
本文为单机试用

  1 nacos-server-2.0.3.zip  是已经编译过可以使用的包
  2 source code 是 源码
  
2 解压缩 nacos-server-2.0.3.zip
   bin里面是启动和关闭nacos命令文件；
   conf存储的nacos相关的配置文件；
   logs日志信息
   target里有一个springboot的jar包
注意 需要本地配置数据库，并修改配置文件之后，才能正常运行；

3.配置数据库
解压缩之后，在conf目录中会发现存在一个nacos-mysql.sql文件；
   3.1 我下载的 nacos 是 2.2.2 当前比较新的版本所以显示的用 muysql-schema.sql
   3.2 本地创建MYSQL数据库nacos，导入解压文件夹中的nacos-mysql.sql脚本。会创建 config 等配置文件信息
   
4.修改配置文件
   4.1 修改conf/路径下的配置文件application.properties
   4.2 将下图中的数据库配置注释放开，同时修改数据库账户和密码；
   4.3 此中的数据库nacos与步骤3中建立的数据库名保持一致；
    
5 启动服务
   5.1 在bin文件夹下执行命令：startup.cmd -m standalone
   5.2 其中**-m standalone指定为单机模式，否则以cluster集群模式启动**;
   5.3 如果没有安装java 环境 就会需要先安装java 8。0 以上的版本
   
6 安装 java jdk 8.6
  官网地址 https://www.oracle.com/java/technologies/downloads/#java8-windows
  6.1  安装java8 包括 jdk1.8 和 jre1.8 .双击已下载好的安装包即可
  6.2 修改安装路劲 自行修改
  6.3 jre 安装 ，建议和 jdk 安装在同一个路径下面
  
7 配置环境变量
   7.1 系统变量， 新建 JAVA_HOME 变量， 添加变量名 JAVA_HOME 变量值 当前 安装的 jdk 路径
   7.2  配置PATH 路径  找到系统变量中的PATH 编辑：%JAVA_HOME%\bin
   
8 测试JDK8 安装
   8.1  输入 cmd 后： java -version
   8.2 验证java编译命令是否可用： javac
   
9 测试nacos
  9.1 执行第五步运行命令 
  9.2 遇到报错  
      WARN Exception encountered during context initialization - cancelling refresh attempt: org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'memoryMonitor' defined in URL [jar:file:/D:/ProgramFiles/nacos/target/nacos-server.jar!/BOOT-INF/lib/nacos-config-2.2.2.jar!/com/alibaba/nacos/config/server/monitor/MemoryMonitor.class]: Unsatisfied dependency expressed through constructor parameter 0; nested exception is org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'asyncNotifyService': Unsatisfied dependency expressed through field 'dumpService'; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'externalDumpService': Invocation of init method failed; nested exception is ErrCode:500, ErrMsg:Nacos Server did not start because dumpservice bean construction failure :
    No DataSource set
  9.3  注意下nacos 配置文件  spring.datasource.platform=mysql 是否 注释 因为我使用的是mysql 8 的版本所以注释该地方
  
      
   
