# spring-boot-notice
记录spring boot 小知识点

## 典型的spring boot
spring-boot 简化了使用spring web web开发的开发配置, maven提供了spring-boot-maven-plugin，直接通过java -jar 直接启动
典型的pom如下:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.eglass</groupId>
    <artifactId>huifu_demo</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>war</packaging>

    <name>huifu_demo</name>
    <description>Demo project for Spring Boot</description>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.3.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <java.version>1.8</java.version>
        <spring-cloud.version>Finchley.SR1</spring-cloud.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!-- 依赖 tomcat -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
        <!--<dependency>-->
            <!--<groupId>org.springframework.cloud</groupId>-->
            <!--<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>-->
        <!--</dependency>-->

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <-- 本地jar -->
        <dependency>
            <groupId>commons-io</groupId>
            <artifactId>commons-io</artifactId>
            <version>1.3</version>
            <scope>system</scope>
            <systemPath>${project.basedir}/lib/commons-io-1.3.jar</systemPath>
        </dependency>
        <dependency>
            <groupId>ccryptokit.jni</groupId>
            <artifactId>cryptokit.jni</artifactId>
            <version>1.0</version>
            <scope>system</scope>
            <systemPath>${project.basedir}/lib/cryptokit.jni-1.0.jar</systemPath>
        </dependency>
        <dependency>
            <groupId>fastjson</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.9</version>
            <scope>system</scope>
            <systemPath>${project.basedir}/lib/fastjson-1.2.9.jar</systemPath>
        </dependency>
        <dependency>
            <groupId>huifu-module-common</groupId>
            <artifactId>huifu-module-common</artifactId>
            <version>1.0.10</version>
            <scope>system</scope>
            <systemPath>${project.basedir}/lib/huifu-module-common-1.0.10-20180730.060259-27.jar</systemPath>
        </dependency>
        <dependency>
            <groupId>cfca.common</groupId>
            <artifactId>SADK</artifactId>
            <version>3.2.0.8</version>
        </dependency>
        <dependency>
            <groupId>sansec.swxajce</groupId>
            <artifactId>sansec.swxajce</artifactId>
            <version>2.1.3</version>
            <scope>system</scope>
            <systemPath>${project.basedir}/lib/sansec.swxajce-2.1.3.jar</systemPath>
        </dependency>
        <dependency>
            <groupId>saturn-cfca</groupId>
            <artifactId>saturn-cfca</artifactId>
            <version>1.0.9</version>
            <scope>system</scope>
            <systemPath>${project.basedir}/lib/saturn-cfca-1.0.9.jar</systemPath>
        </dependency>
        <dependency>
            <groupId>slf4j-api</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.6.1</version>
            <scope>system</scope>
            <systemPath>${project.basedir}/lib/slf4j-api-1.6.1.jar</systemPath>
        </dependency>

    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <!-- 本地jar -->
                    <includeSystemScope>true</includeSystemScope>
                </configuration>
            </plugin>
        </plugins>
    </build>


</project>
```

主函数

```java
package com.eglass.huifu_demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class HuifuDemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(HuifuDemoApplication.class, args);
    }
}
```

## spring boot 打包war的配置
```xml
-    <packaging>jar</packaging>
+    <packaging>war</packaging>
+    <dependency>
+        <groupId>org.springframework.boot</groupId>
+        <artifactId>spring-boot-starter-tomcat</artifactId>
+        <scope>provided</scope>
+    </dependency>

```
主函数
```java
package com.eglass.huifu_demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.builder.SpringApplicationBuilder;
import org.springframework.boot.web.servlet.support.SpringBootServletInitializer;
//import org.springframework.cloud.netflix.eureka.EnableEurekaClient;

@SpringBootApplication
//@EnableEurekaClient
public class HuifuDemoApplication extends SpringBootServletInitializer {
    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
        return builder.sources(HuifuDemoApplication.class);
    }


    public static void main(String[] args) {
        SpringApplication.run(HuifuDemoApplication.class, args);
    }
}
```
