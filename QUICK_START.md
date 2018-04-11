

快速开始
====

## 一个栗子：访问百度短链接REST接口

### 添加Maven依赖


```xml
    <!-- okhttp3 -->
    <dependency>
        <groupId>com.squareup.okhttp3</groupId>
        <artifactId>okhttp</artifactId>
        <version>3.4.1</version>
    </dependency>

    <!-- spring -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-beans</artifactId>
        <version>3.2.16.RELEASE</version>
        <scope>provided</scope>
    </dependency>

    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>3.2.16.RELEASE</version>
        <scope>provided</scope>
    </dependency>

    <!-- forest核心包 -->
    <dependency>
        <groupId>org.forest</groupId>
        <artifactId>forest-core</artifactId>
        <version>0.1.6</version>
    </dependency>

    <!-- forest spring扩展包 -->
    <dependency>
        <groupId>org.forest</groupId>
        <artifactId>forest-spring</artifactId>
        <version>0.1.6</version>
    </dependency>

```

### 创建一个Interface作为远程调用接口


```java

import org.forest.annotation.Request;
import org.forest.annotation.DataParam;

public interface MyClient {

    /**
     * 百度短链接API
     * @param url
     * @return
     */
    @Request(
        url = "http://dwz.cn/create.php",
        type = "post",
        dataType = "json"
    )
    Map getShortUrl(@DataParam("url") String url);


}


```


### 调用远程接口
```java

ForestConfiguration configuration = ForestConfiguration.configuration();
MyClient myClient = configuration.createInstance(MyClient.class);
Map result = myClient.getShortUrl("https://gitee.com/dt_flys/forest");
System.out.println(result);

```

#### 或者在Spring中调用

```java
@Autowired
MyClient myClient;

...

Map result = myClient.getShortUrl("https://gitee.com/dt_flys/forest");

```