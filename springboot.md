# spring boot webapplication to weblogic

pom.xml添加
打包方式war

```Xml
    <packaging>war</packaging><!--<packaging>jar</packaging>-->
```

添加依赖

```Xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-tomcat</artifactId>
        <scope>provided</scope>
    </dependency>
```

修改入口application

```Java
@SpringBootApplication
public class WebshellApplication  extends SpringBootServletInitializer implements WebApplicationInitializer {

    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
        return application.sources(WebshellApplication.class);
    }

    public static void main(String[] args) {
        SpringApplication.run(WebshellApplication.class, args);
    }

}
```

打包

```Shell
mvn package
```

添加weblogic.xml到war包的WEB-INF文件夹下

```Xml
<?xml version="1.0" encoding="UTF-8"?>
<wls:weblogic-web-app
    xmlns:wls="http://xmlns.oracle.com/weblogic/weblogic-web-app"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
        http://java.sun.com/xml/ns/javaee/ejb-jar_3_0.xsd
        http://xmlns.oracle.com/weblogic/weblogic-web-app
        http://xmlns.oracle.com/weblogic/weblogic-web-app/1.4/weblogic-web-app.xsd">
    <wls:container-descriptor>
        <wls:prefer-application-packages>
            <wls:package-name>org.slf4j</wls:package-name>
        </wls:prefer-application-packages>
    </wls:container-descriptor>
     <wls:context-root>/</wls:context-root>
</wls:weblogic-web-app>
```