[TOC]

# 入职环境

## 挂载NAS网盘

![](https://o4j4l4n7h.qnssl.com/2017-08-02-022652.jpg)

1. 打开 `Finder - 前往 - 链接服务器` 或 `commad + k`
2. 输入 smb://nas.xiongmaojinku.com
3. 选用游客登录
4. 将`Pandatown`文件夹拉入Finder左侧的个人收藏即可快速访问

>[info] NAS为金库内网网盘，只可在内网访问

## 安装工具

### 安装Adobe系

使用[Adobe Cloud](https://creative.adobe.com/zh-cn/products/download/creative-cloud)直接安装试用版，之后使用`Adobe Zii`统一激活

### 安装Sketch

[Sketch官网](https://www.sketchapp.com/updates/)

使用nas网盘安装: `nas/Pandatown/软件/Sketch 统一版/`，因为sketch不支持向下兼容，因此团队需使用统一版本，plugin中有团队定制插件，必须安装

### 安装Figma

[Figma官网](https://www.figma.com/)

交互稿协作和查询工具，统一账号密码问管理员


### 安装MarkEditor（可选）

[MarkEditor官网](http://markeditor.com/app/markeditor)

公众号及线上平台发文统一markdown编辑器, 文件夹位于`nas/Markdown/`, 与七牛自动同步

>[info] 激活地址: 激活码位于根目录md


## Git配置

### 注册coding.net账号

1. 在[此网站](https://coding.net)注册账号
2. 找管理员将你拉进UED项目组

### 配置SSH

[参考文档](https://coding.net/help/doc/account/ssh-key.html)

### 安装SourceTree

[SourceTree官网](https://www.sourcetreeapp.com/)

Git可视化工具，UED设计文件使用Git管理

需要[翻墙](ued/share/创建私有SSR.md)并配置`SSH`和`Coding`


## UED设计项目

### 熊猫金库v1-2 sketch仓库

```
git@git.coding.net:canisminor1990/XmjkSketch.git
```

### 熊猫金库v3 sketch仓库

```
git@git.coding.net:xmjk-fe/xmSketch.git
```

### 智子 sketch仓库

```
git@git.coding.net:xmzhen/zhizi-sketch.git
```

## UED工具站

### Trello

[Trello](https://trello.com/b/WDGfmQRs/ued) - UED项目管理

### XMUED

[XMUED](https://ued.xiongmaojinku.com) - 金库UED官网

### Redmine

[Redmine](https://redmine.xiongmaojinku.com) - 走查汇报bug

### iconfont.cn

[iconfont.cn](http://www.iconfont.cn/) - iconfont托管

### Ant Design

[Ant Design](https://mobile.ant.design/docs/react/introduce-cn) - 阿里组件库

### 花瓣素材库

[背景素材](http://huaban.com/boards/25545712/)

# 进阶环境

## 安装工具

### 安装iTerm

```bash
git clone git://git.coding.net/canisminor1990/myConfig.git
# 配置文件 /iTerm
```

### 安装WebStorm

```bash
# 配置文件 /webStorm
git clone git://git.coding.net/canisminor1990/myConfig.git
# 配置文件 /webstorm
```

>[info] 激活地址: <https://jetbrains.xiongmaojinku.com>

扩展阅读：[WebStorm常用技巧汇总](pd/前端/WebStorm常用技巧汇总)

## 配置环境

### 安装homebrew

官网[homebrew](https://brew.sh/)

```bash
ruby -e "$(curl -fsSL --insecure raw.githubusercontent.com/Homebrew/install/master/install)"
```

### 安装fishshell

官网[fishshell](http://www.fishshell.com/)

```bash
git clone git://git.coding.net/canisminor1990/myConfig.git
# 在fish文件夹中查看后续流程
```

### 安装nodejs

官网[nodejs](https://nodejs.org/en/)

选择Current版

### 安装yarn

官网[yarn](https://yarnpkg.com/en/)

包管理工具

```bash
npm install -g yarn
```

### 安装 git-lfs

```
brew install git-lfs
git lfs install
```

## UED设计管理项目


### XMUED | 线上版本

```
git@git.coding.net:canisminor1990/newXMUED.git
```

> ~~XMUED (旧 | 不再维护) - git@git.coding.net:canisminor1990/XMUED.git~~

### XMUI | 组件库

```
git@git.coding.net:xmjk-fe/xmui.git
```

### XMHOOK | 自动部署服务

```
git@git.coding.net:canisminor1990/xm-hook.git
```

### XMRM | Redmine定制

```
git@git.coding.net:xmjk/xmjkRedmine.git
```

### XMADM | Admin定制

```
git@git.coding.net:canisminor1990/xmjkAdmin.git
```