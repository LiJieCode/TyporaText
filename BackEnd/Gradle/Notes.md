# Notes











## Gradle 入门



### Gradle 的基本命令







### Gradle 的第一个项目



- Wrapper 包装器  

```shell
# 只是版本号修改了，还未下载
gardle wrapper --gradle-version=7.1.1

# 下载
gradlew.bat classes
# ..........10%......
```

> 下载存放目录：
>
> ```properties
> # 解压文件目录（和下载文件是一个目录）
> # GRADLE_USER_HOME是环境变量中配置的
> distributionBase=GRADLE_USER_HOME
> distributionPath=wrapper/dists
> distributionUrl=https\://services.gradle.org/distributions/gradle-7.1-bin.zip
> # 下载文件目录
> zipStoreBase=GRADLE_USER_HOME
> zipStorePath=wrapper/dists
> ```





## Gradle 与 Idea 整合





