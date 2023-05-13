# Notes

- 普通用户：lijzh
- 管理员用户：admin





## 启动DS

- 首先启动zk
- 一键部署

```shell
[/opt/software/ds/apache-dolphinscheduler-2.0.5-bin] ./install.sh
```

- 访问WebUI：l9z102:12345

> 改配置的话，要在安装目录里面改。在解压目录里面改没有用。







## 安全中心



- 租户管理

  DS的worker节点上的操作系统用户，因为最终提交

  租户对应的是 Linux 的用户，用于 worker 提交作业所使用的用户。  每个worker节点对应系统用户

  如果这个用户存在，就可以正常执行。

  如果这个用户不存在，就会报错；也可以修改某个参数，实现自动创建某个用户。





- 用户管理  

  DS的用户：

  管理员：有授权和用户管理等权限，没有创建项目和工作流定义的操作的权限。  

  普通用户：可以创建项目和对工作流定义的创建，编辑，执行等操作。  （没有安全中心）

  





- 环境管理

  管理一些环境变量

  可以指定一些环境组合，不用单独设计环境变量





- 令牌管理 







## 项目管理

定义一个工作流，可以包含多个任务

工作流执行一次，就会生成一个工作流实例，会生多个任务实例。











```
CREATE DATABASE dolphinscheduler DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;

CREATE USER 'dolphinscheduler'@'%' IDENTIFIED BY 'li123...';

GRANT ALL PRIVILEGES ON dolphinscheduler.* TO 'dolphinscheduler'@'%';

flush privileges;
```



```
cp /opt/software/mysql-connector-java-8.0.16.jar lib/

script/createdolphinscheduler.sh
```

