# ecplugin-version-gradle-plugin

本项目为 Gradle 插件，用于编辑与发布时自动根据 Git 推算版本号

## 使用方法

```
plugins {
    id 'com.ecplugin.gradle.plugin.version' version '<version>'
}
```

执行 `gradle build` 或者 `gradle release` 可见推算版本

``` bash
11:54:14: Executing 'build'...
reckon version: 0.0.3  ->  0.0.4-alpha
```

## 说明

插件已发布至 Gradle Plugin Portal ，如提示下载失败，请在`settings.gradle`增加配置

```
pluginManagement {
    repositories {
        gradlePluginPortal()
        ...
    }
}
...
```