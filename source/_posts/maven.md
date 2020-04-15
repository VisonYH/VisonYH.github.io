### maven

项目下没有包仓库，统一集中在计算机maven安装时设置的仓库位置。



#### maven安装

下载[maven](http://maven.apache.org/download.cgi)。
- windows
下载安装包，配置环境变量， 依赖JAVA_HOME。
- mac

编辑```~/.bash_profile```
```bash
export MAVEN_HOME=/usr/local/apache-maven-3.3.9
export PATH=${PATH}:${MAVEN_HOME}/bin
```

#### 仓库种类
- 本地仓库
默认在系统用户目录/.m2/repositive
可以在默认在系统用户目录/.m2/config.xml中配置更改本地仓库位置 ```<localReposity>/path/to/reposity</localReposity>```

- 远程仓库（私服）
    远程仓库没有找到仓库的时候，会继续到中央仓库寻找。

- 中央仓库
  社区维护的仓库，几乎所有开源包


#### maven项目标准目录结构

- src/main/java 核心代码目录
- src/main/resource 核心代码目录
- src/test/java 测试代码目录
- src/test/resource 测试代码目录
- src/main/webapp 页面资源 js、css图片等


#### maven常用命令
- mvn clean 清除编译好的内容
- mvn compile 编译
- mvn package 打包
- mvn install 在本地安装依赖
- mvn test-compile 编译测试代码
- mvn test 运行测试
- mvn tomcat:run 启动tomcat
- mvn deploy

#### maven生命周期
下方命令包含以上每个命令
- 编译 mvn compile
- 测试 mvn test
- 打包 mvn package
- 安装 mvn install
- 发布 mvn deploy


#### 一键构建功能