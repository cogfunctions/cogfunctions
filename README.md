// pom.xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.jasmine</groupId>
    <artifactId>cogFunctions</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>

    <name>cogFunctions</name>
    <description>Jungian Cognitive Function Test Website</description>

    <properties>
        <java.version>17</java.version>
        <spring.boot.version>3.2.5</spring.boot.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>

// src/main/java/com/jasmine/cogfunctions/JungTestApp.java
package com.jasmine.cogfunctions;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class JungTestApp {
    public static void main(String[] args) {
        SpringApplication.run(JungTestApp.class, args);
    }
}

// src/main/java/com/jasmine/cogfunctions/controller/TestController.java
package com.jasmine.cogfunctions.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class TestController {

    @GetMapping("/")
    public String index() {
        return "index";
    }

    @GetMapping("/question/{id}")
    public String question(@PathVariable int id, Model model) {
        // TODO: 加载题目和选项
        return "question";
    }

    @PostMapping("/answer")
    public String submitAnswer(@RequestParam Map<String, String> params) {
        // TODO: 保存答案并跳转下一题
        return "redirect:/question/2";
    }

    @GetMapping("/result")
    public String result(Model model) {
        // TODO: 计算得分并展示
        return "result";
    }
} 

