## idea下配置springboot热加载

#### 1.添加pom依赖

```xml
       <!-- SpringBoot自带热加载开发工具 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
        </dependency>
```

#### 2. 添加配置

打开 File --> Settings --> Build-Execution-Deployment --> Compiler`，将 `Build project automatically.勾上。

![post-idea-setting-1](..\img\post-idea-setting-1.png)

#### 3 . 

快捷键 ctrl + alt + shift + / 打开 Maintenance 找到 `Registry...`，将 其中的 `compiler.automake.allow.when.app.running`勾上。

![post-idea-setting-2](..\img\post-idea-setting-2.png)



![post-idea-setting-3](..\img\post-idea-setting-3.png)

