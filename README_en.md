# ecplugin-version-gradle-plugin

**[中文](README.md) | [English](README_en.md)**

This project is a Gradle plugin, which is used to automatically calculate the version number from Git in time (following
the [semver](https://semver.org) specification)`build``release`

Please refer to [the online documentation](https://liuzhenghui.github.io/ecplugin-version-gradle-plugin/) for detailed
instructions

## Usage

```
plugins {
    id 'com.ecplugin.gradle.plugin.version' version '<version>'
}
```

Execute or Visible Extrapolated Version `gradle build` `gradle release`

```bash
11:54:14: Executing 'build'...
reckon version: 0.0.3  ->  0.0.4-alpha
```

## gradle.properties

```
# git
git@gitee.com=username:password@https://gitee.com/xxx/
git@github.com=username:password@https://github.com/xxx/
```

> 1. If the username or password contains or, add it first.
     As:`git@gitee.com=paul\\@gmail.com:pwd\\:111@https://gitee.com/xxx/`
> 2. Github needs to use the token method, the username is fixed, and the password is token.
     As:`PRIVATE-TOKEN``git@github.com=PRIVATE-TOKEN:your_token@https://github.com/xxx/`

## methods

| task       | description                                                                                                                                                           |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| build      | gradle build                                                                                                                                                          |
| release    | 发布新版本，示例:`gradle release -Pversion.scope=minor`。<br>可选参数: <br>1. version.scope: 指定递增范围，选项为 major、minor、patch(默认)   <br>2. version.version: 指定发布版本号，将忽略推算的版本号，如`1.2.0` |
| releaseGUI | 图形界面发布新版本，示例:`gradle releaseGUI`。   <br>![image](http://free.yunpng.top/tu/2024/08/03/66adbc59cc46a.png)                                                              |

## configuration

| parameter                | description         |
|--------------------------|---------------------|
| branches                 | Git分支与版本号Stage 对应关系 |
| branchesReleaseMergeInto | 发布时自动合并新内容的分支       |

default:

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

## others

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
