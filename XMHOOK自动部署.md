# 总体架构

![](https://dn-coding-net-production-static.qbox.me/1d89f1e7-5ce9-42e0-8bc6-784d6fc695b2.png)

基于`nodejs` + `express`

>网址: <https://fanshu.xiongmaojinku.com>
>仓库: <https://coding.net/u/canisminor1990/p/xm-hook>

## 使用方法

```sh
# 安装forever 
$ npm install forever -g

# 使用forever常驻进程
$ forever start webhook.js

# 结束进程
$ forever stop webhook.js
```

> 接受到hook信息将会保存为`log.json`,显示于<https://fanshu.xiongmaojinku.com>

在`config.js`中可配置监听项目

```js
var projects = {
    "newXMUED"   : {
        coding: 'git@git.coding.net:canisminor1990/newXMUED.git',
        url   : 'ui',
    },
    "xmjkRedmine": {
        coding: 'git@git.coding.net:xmjk/xmjkRedmine.git',
        url   : 'redmine',
    },
    "xmjkAdmin"  : {
        coding: 'git@git.coding.net:xmjk/xmjkRedmine.git',
        url   : 'admin',
    },
    "xm-hook"    : {
        coding: 'git@git.coding.net:canisminor1990/xm-hook.git',
        url   : 'webhook',
    },
    "xmui"       : {
        coding: 'git@git.coding.net:xmjk-fe/xmui.git',
        url   : 'xmui'
    }
};
```


在`bash/*.sh`中可配置动作

>[info] 
> 1. 当`commit`内容为`autobuild`时，[xm-hook](XMHOOK自动部署.md)将触发动作
> 2. 文件名为webhook地址，如ued的webhook地址为 <https://fanshu.xiongmaojinku.com/ui>, 则会触发`ui.sh`

```bash
# bash/ui.sh
cd ~/../var/www/newXMUED/
git checkout .
git pull
```

## 获取日志

Host: http://fanshu.xiongmaojinku.com

~~~[api:xmhook]
get:/
<<<
success
[
    {
        "url": "/ui",
        "data": {
            "ref": "refs/heads/master",
            "before": "1bb93851c53d51c9957fa4a24847d4563cf98ab2",
            "commits": [
                {
                    "committer": {
                        "name": "deer012611",
                        "email": "deer012611@163.com"
                    },
                    "web_url": "https://coding.net/u/canisminor1990/p/newXMUED/git/commit/63aaa4d814111a9b228a5d9107cda4ea25968600",
                    "short_message": "autobuild\n",
                    "sha": "63aaa4d814111a9b228a5d9107cda4ea25968600"
                }
            ],
            "after": "63aaa4d814111a9b228a5d9107cda4ea25968600",
            "event": "push",
            "repository": {
                "owner": {
                    "path": "/u/canisminor1990",
                    "web_url": "https://coding.net/u/canisminor1990",
                    "global_key": "canisminor1990",
                    "name": "canisminor",
                    "avatar": "https://dn-coding-net-production-static.qbox.me/e11b070a-4533-41b2-90d3-91ab97ebd4bb.png?imageMogr2/auto-orient/format/png/crop/!800x800a0a0"
                },
                "https_url": "https://git.coding.net/canisminor1990/newXMUED.git",
                "web_url": "https://coding.net/u/canisminor1990/p/newXMUED",
                "project_id": "783406",
                "ssh_url": "git@git.coding.net:canisminor1990/newXMUED.git",
                "name": "newXMUED",
                "description": ""
            },
            "user": {
                "path": "/u/deer012611",
                "web_url": "https://coding.net/u/deer012611",
                "global_key": "deer012611",
                "name": "deer012611",
                "avatar": "https://dn-coding-net-production-static.qbox.me/92c60288-cb01-4a97-ae76-3612d18f24c5.jpg?imageMogr2/auto-orient/format/jpeg/crop/!524x524a10a42"
            }
        },
        "time": "2017-7-31 18:37:34"
    },
    ...
]
~~~
