# ecplugin-version-gradle-plugin

本项目为 Gradle 插件，用于`build`与`release`时自动根据 Git 推算版本号(遵循[semver](https://semver.org)规范)

详细说明请查看[在线文档](https://github.com/liuzhenghui/ecplugin-version-gradle-plugin)

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

## 方法

| task       | 说明                                                                                                                                                                     |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| build      | 构建                                                                                                                                                                     |
| release    | 发布新版本，示例: `gradle release -Pversion.scope=minor`。<br>可选参数: <br>1. version.scope: 指定递增范围，选项为 major、minor、patch(默认)   <br>2. version.version: 指定发布版本号，将忽略推算的版本号，如`1.2.0` |
| releaseGUI | 图形界面发布新版本，示例: `gradle releaseGUI`。   <br>![image](http://free.yunpng.top/tu/2024/08/03/66adbc59cc46a.png)                                                              |

## 配置参数

| 参数                       | 说明                  |
|--------------------------|---------------------|
| branches                 | Git分支与版本号Stage 对应关系 |
| branchesReleaseMergeInto | 发布时自动合并新内容的分支       |

默认配置:

```groovy
reckonVersion {
    // Git分支与版本号Stage 对应关系
    branches.empty()
            .branch(['main', 'master'], 'rc')
            .branch('test', 'beta', 'beta')
            .branch('release/**', 'rc')
            .branch('hotfix/**', 'rc')
            .branch('**', 'alpha', 'alpha')

    // 发布时自动合并新内容的分支
    branchesReleaseMergeInto = ['main', 'master', 'test', 'develop/**']
}
```

## 说明

1. 若插件不生效，检查`build.gradle`是否设置了`version`属性。将`version`移除或设置为`auto`

```
group = 'com.xxx.xxx'
version = 'auto'
```

2. 插件已发布至 Gradle Plugin Portal ，如提示下载失败，在`settings.gradle`增加配置如下:

```
pluginManagement {
    repositories {
        gradlePluginPortal()
        ...
    }
}
...
```
