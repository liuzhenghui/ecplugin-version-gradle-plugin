# ecplugin-version-gradle-plugin

本项目为 Gradle 插件，用于编辑与发布时自动根据 Git 推算版本号

## 使用方法

```
plugins {
    id 'com.ecplugin.gradle.plugin.version' version '<version>'
}
```

build

```
./gradlew build
```

release

```
./gradlew release
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