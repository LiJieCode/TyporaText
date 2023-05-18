# JDBC Notes

## Remark

1、Mysql连接的配置文件区别（*.properties）

```properties
# 使用时，注意配置文件的内容：数据库，用户名，密码等是否正确
# mysql 5.7  
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/db_jdbc
username=root
password=li123...
initialSize=10
maxActive=20
maxWait=10000

# mysql 8.0
driverClassName=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/db_jdbc?useSSL=false&serverTimezone=UTC
username=root
password=li123...
initialSize=10
maxActive=20
maxWait=10000
```

2、导入项区别

```java
import com.mysql.jdbc.Driver;     // mysql57  用于注册驱动
import com.mysql.cj.jdbc.Driver;  // mysql80  用于注册驱动
```

3、获得当前类路径的方法

```java
// 第一种：获取类加载的根路径
File f = new File(this.getClass().getResource("/").getPath());
System.out.println(f);
 
// 获取当前类的所在工程路径; 如果不加“/”  获取当前类的加载目录  D:\git\daotie\daotie\target\classes\my
File f2 = new File(this.getClass().getResource("").getPath());
System.out.println(f2);
 
// 第二种：获取项目路径    D:\git\daotie\daotie
File directory = new File("");// 参数为空
String courseFile = directory.getCanonicalPath();
System.out.println(courseFile);
 
 
// 第三种：  file:/D:/git/daotie/daotie/target/classes/
URL xmlpath = this.getClass().getClassLoader().getResource("");
System.out.println(xmlpath);
 
 
// 第四种： D:\git\daotie\daotie
System.out.println(System.getProperty("user.dir"));
/*
 * 结果： C:\Documents and Settings\Administrator\workspace\projectName
 * 获取当前工程路径
 */
 
// 第五种：  获取所有的类路径 包括jar包的路径
System.out.println(System.getProperty("java.class.path"));
```



## JDBC 快速入门

###  JDBC程序编写步骤  

- 注册驱动，加载Driver类
- 获取连接，得到Connection
- 执行增删改查，发送SQL给mysql执行
- 释放资源，关闭相关连接

### JDBC的五种连接方式

- 第一种方式

```java
// 1.注册驱动
Driver driver = new Driver();

// 2.得到链接
//(1) jdbc:mysql:// 规定好表示协议，通过jdbc的方式连接mysql
//(2) localhost 主机，可以是ip地址
//(3) 3306 表示mysql监听的端口
//(4) db_jdbc 连接到mysql dbms 的哪个数据库
//(5) mysql的连接本质就是前面学过的socket连接
// String url = "jdbc:mysql://localhost:3306/db_jdbc?characterEncoding=utf8&useSSL=false&serverTimezone=UTC&rewriteBatchedStatements=true";
String url = "jdbc:mysql://localhost:3306/db_jdbc?useSSL=false&serverTimezone=UTC";
Properties properties = new Properties();
properties.setProperty("user", "root");
properties.setProperty("password", "li123...");
Connection connect = driver.connect(url, properties);

// 3.执行sql语句
// String sql = "insert into actor values(null, '张学友', '男', '1970-01-02', '111')";
String sql = "update actor set name = '周星驰1' where id = 1";
Statement statement = connect.createStatement();
int row = statement.executeUpdate(sql);
System.out.println(row > 0 ? "成功" : "失败");

// 4.关闭连接资源
statement.close();
connect.close();
```

- 第二种方式

```java
// 1.注册驱动
// 使用反射加载Driver类，动态加载，更加灵活，减少依赖性
Class<?> aClass = Class.forName("com.mysql.cj.jdbc.Driver");
Driver driver = (Driver)aClass.newInstance();

// 2 - 4:同第一种方式
// 2.得到链接
// 3.执行sql语句
// 4.关闭连接资源

```

- 第三种方式

```java
// 使用 DriverManager 代替 Driver 进行统一管理

// 1.注册驱动
Class<?> aClass = Class.forName("com.mysql.cj.jdbc.Driver");
Driver driver = (Driver)aClass.newInstance();

// 2.获得连接
//创建url 和 user 和 password
String url = "jdbc:mysql://localhost:3306/db_jdbc?useSSL=false&serverTimezone=UTC";
String user = "root";
String password = "li123...";
DriverManager.registerDriver(driver);      //利用 Driver 注册DriverManager
Connection connect = DriverManager.getConnection(url, user, password);

// 3 - 4:同前两种方式
// 3.执行sql语句
// 4.关闭连接资源

```

- 第四种方式

```java
// 使用Class.forName 自动完成注册驱动，简化代码
// 这种方式获取连接是使用的最多，推荐使用
// 使用反射加载了 Driver类
// 在加载 Driver类时，完成注册
/*
源码: 1. 静态代码块，在类加载时执行，并且只执行一次
2. DriverManager.registerDriver(new Driver());
3. 因此注册driver的工作已经完成
static {
    try {
        DriverManager.registerDriver(new Driver());  //  注册driver的工作已经完成
    } catch (SQLException var1) {
        throw new RuntimeException("Can't register driver!");
    }
}
*/

// 1.使用反射加载 Driver类时，静态代码块自动完成注册Driver驱动
Class.forName("com.mysql.cj.jdbc.Driver");

// 2.获得连接
String url = "jdbc:mysql://localhost:3306/db_jdbc?useSSL=false&serverTimezone=UTC";
String user = "root";
String password = "li123...";
Connection connect = DriverManager.getConnection(url, user, password);

// 3 - 4:同前两种方式
// 3.执行sql语句
// 4.关闭连接资源

```

- 第五种方式

```java
// 配置文件内容 pro.properties 文件
driver=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/db_jdbc?useSSL=false&serverTimezone=UTC
username=root
password=li123...



Properties properties = new Properties();
properties.load(new FileInputStream("D:\\DeskTop\\Java\\JDBCStudy\\chapter01\\src\\edu\\lzu\\f1\\pro.properties"));
String username = properties.getProperty("username");
String password = properties.getProperty("password");
String driver = properties.getProperty("driver");
String url = properties.getProperty("url");

Class.forName(driver);   //建议写上

Connection connect = DriverManager.getConnection(url, username, password);
```



# JDBC - 康师傅

## 























