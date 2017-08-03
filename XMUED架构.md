# 总体架构

![# test](http://ued.xiongmaojinku.com/img/site-logo.png)


>网址: <https://ued.xiongmaojinku.com>
>仓库: <https://coding.net/u/canisminor1990/p/newXMUED/git/tree/master>

## 目录

[TOC=2,3]

## 部署

### 常用命令

前端和数据是分离的，添加文档和UI仓库时不用整站编译

```bash
# 安装依赖
$ yarn

# 编译文档/UI仓库json 并部署,不会重新编译XMUED
# 前端和数据已分离增加内容时不用重新编译整站
$ yarn build-data

# 编译XMUED并部署
$ yarn build-all
```

压缩UI仓库：每次添加UI仓库时请跑一下此命令再`build-data`

>[warning] 可以去除颜色配置文件修复图片颜色不准的情况，同时可以大幅缩减图片体积

```bash
# 编译 UI仓库[--后放目标path]
# 请用最新的定制版Sketch插件导出，并放入data/library中
$ gulp library --2.2/xxx
```

>[warning] 如需增加版本号或者产品线需要修改 `data/nav/nav-library.json`

- `name`为文件夹名 (必须和library中的文件夹名保持一致)
- `title`为产品线名

```json
[  
  {
    "name": "3.0",
    "title": "熊猫金库"
  },
  {
    "name": "2.6",
    "title": "熊猫金库"
  },
  {
    "name": "2.4",
    "title": "熊猫金库"
  },
  ...
]
```

### 自动部署

>[info] 当`commit`内容为`autobuild`时，[xm-hook](ued/XMHOOK自动部署.md)将触发自动部署

```bash
# yarn build-xxx 类命令已自带commit
git commit -m "autobuild"
```

## 框架

共重构过三版分别为:

- `jekyll` : 基于ruby
- `hexo` : 基于nodejs
- `react` + `redux` : **当前**

### 网站框架

`react` + `redux` 部分用了阿里整套环境：

- [dva](https://github.com/dvajs/dva)
- [roadhog](https://github.com/sorrycc/roadhog)
- [ant design](https://ant.design/docs/react/introduce-cn) 阿里antd组件库

>[warning] 其中一些有深度定制: 有考虑取消，待原版支持定制功能

- [![](https://img.shields.io/npm/v/xm-cli.svg?style=flat)](https://www.npmjs.com/package/xm-cli)  **xm-cli**
- [![](https://img.shields.io/npm/v/xm-roadhog.svg?style=flat)](https://www.npmjs.com/package/xm-roadhog)  **xm-roadhog**


## UI仓库

### 添加仓库

1. 使用定制版sketch插件`XM Measure`导出json和资源文件
2. 将资源那文件，放于`data/library/*.*中` 
3. 执行`gulp library --*.*` 命令
4. 执行`yarn build-data`编译并部署到线上

### XM Measure

原插件: [Sketch Mearsure](https://github.com/utom/sketch-measure)

> 定制插件原理：
> 原插件是导出html格式仓库，每次导出都会重新生成js和css文件，体积庞大并不易于维护
> 现将js和css文件已写入xmued中，将插件改为只生成结构文件json, 从而减少体积和资源调用

### Sketch仓库

- 熊猫金库v1-2 sketch仓库

```
git@git.coding.net:canisminor1990/XmjkSketch.git
```

- 熊猫金库v3 sketch仓库

```
git@git.coding.net:xmjk-fe/xmSketch.git
```

- 智子 sketch仓库

```
git@git.coding.net:xmzhen/zhizi-sketch.git
```

## 首页信息流

UED首页信息流基于[BearyChat](https://bearychat.com/)

因为Bearychat并不开放api调用信息流，因此使用了一些hack方法，使用cookies注入了我的账号登录信息，直接调用Bearchat的接口

- Host: <https://xmzhen.bearychat.com>

### 获取团队信息 

~~~[api:bearychat]
get:/api/team
<<<
return
{
    "code": 0,
    "result": {
        "inactive": false,
        "description": "www.xiongmaojinku.com",
        "logo_url": null,
        "updated": "2016-07-06T05:26:13.000+0000",
        "name": "熊猫金库",
        "created": "2016-07-06T04:43:49.000+0000",
        "subdomain": "xmzhen",
        "preference": {
            "prior_name": "fullname"
        },
        "from": null,
        "id": "=bw8Fc",
        "email_domain": "xmzhen.com",
        "plan": "basic"
    }
}
~~~

### 登陆接口 

需要记录下 cookie 

~~~[api:bearychat]
post:/api/signin
*string:identity=yangyufan@xmzhen.com#用户名
*string:password=******#密码
*bool:remember_me=true#是否记住
<<<
return
{
    "code": 0,
    "result": {
        "user": {
            "inactive": false,
            "role": "owner",
            "features": [
                "dnd-mode"
            ],
            "email": "yangyufan@xmzhen.com",
            "authed": [
                "trello",
                "evernote",
                "teambition",
                "shimo"
            ],
            "presence": "online",
            "dnd": {
                "manual_enabled": true,
                "start": "22:00:00+0800",
                "end": "07:00:00+0800",
                "schedule_enabled": false
            },
            "updated": "2016-09-30T02:22:55.000+0000",
            "name": "canisminor",
            "type": "normal",
            "created": "2016-07-06T04:43:49.000+0000",
            "email_verified": true,
            "guides": {
                "tour": false,
                "fav": false,
                "search": false,
                "help": false,
                "files": false,
                "shortcuts": false
            },
            "mobile_verified": false,
            "preference": {
                "sound": true,
                "desktop_notification": "at",
                "self_typing_visibility": "visible",
                "notification": "all",
                "robot_notification": true,
                "theme": "light",
                "email_visibility": "visible",
                "mention": "half_hour",
                "language": "zh-CN",
                "mobile_visibility": "visible",
                "mobile_notification_mute": true,
                "desktop_robot_notification": true,
                "leftbar_mode": "default",
                "typing_visibility": "visible"
            },
            "id": "=bwHFw",
            "position": "UED",
            "avatars": {
                "small": "https://dn-bearychat.qbox.me/FtR5JrI0GdBtHrwNDiId23Tu-2Ud?imageView2/1/w/180/h/180",
                "medium": "https://dn-bearychat.qbox.me/FtR5JrI0GdBtHrwNDiId23Tu-2Ud?imageView2/1/w/360/h/360",
                "large": "https://dn-bearychat.qbox.me/FtR5JrI0GdBtHrwNDiId23Tu-2Ud?imageView2/1/w/720/h/720"
            },
            "team_id": "=bw8Fc",
            "full_name": "番薯哥哥",
            "mobile": "15305853008",
            "avatar_url": "https://dn-bearychat.qbox.me/FtR5JrI0GdBtHrwNDiId23Tu-2Ud"
        },
        "ws_host": "wss://rtm.bearychat.com/nimbus/ws:3a2f2acec43cc54bcdc892040a57c287",
        "tcp_path": "rtm01.bearychat.com:5222",
        "tcp": {
            "url": "rtm01.bearychat.com:5222",
            "key": "tcp:d725c239083e0f32234463b752fa0a93"
        },
        "web_version": "8634aec568fd594f9576cb32c15cd5c43f66d78a",
        "oauth": {
            "access_token": "15b200a8855dd505c35a9864ea79c4c1",
            "refresh_token": "66239dbaf1bdef711fc9d98d00c3c023",
            "expires_in": 7776000,
            "scope": "all",
            "token_type": "bearer"
        }
    }
}
~~~

值得研究的地方 

```bash
# websocket 
wss://bearychat.com/nimbus/ws:6c41a0eeec0696ce94f7707f83d6a88d
```

### 获取频道

>[info]
>请求头 `Cookie: bearychat_517=???`
>也可以带上 `bearychat=517; Cookie: bearychat=517; bearychat_517=xxx;`

```bash
curl -H 'Cookie: bearychat_517=xxx;'  https://xmzhen.bearychat.com/api/channels|json_pp
```

~~~[api:bearychat]
get:/api/channels
<<<
return
{
    "code": 0,
    "result": [
        {
            "inactive": false,
            "description": null,
            "read_ts": 1487140038702,
            "star_id": null,
            "private": false,
            "general": true,
            "latest_ts": 1501646313679,
            "pinyins": "suoyouren,syr",
            "ann_read_ts": 0,
            "updated": "2016-07-06T07:44:27.000+0000",
            "uid": "=bwHFw",
            "name": "所有人",
            "pinyin": [
                "suoyouren",
                "syr"
            ],
            "is_member": true,
            "index_symbol": "s",
            "type": "normal",
            "created": "2016-07-06T04:43:49.000+0000",
            "topic": "大厅",
            "member_count": 34,
            "vchannel_id": "=bwDmm",
            "id": "=bwDmm",
            "team_id": "=bw8Fc",
            "members": [...],
            "unread_count": 100,
            "mention_count": 0
        }
    ]
}
~~~


### 获取归档频道 
请求头 Cookie: bearychat_517=??? 
返回 同上 GET /api/channels

~~~[api:bearychat]
get:/api/channels/archived
<<<
return
返回 同上 GET /api/channels
~~~


### 获取成员 

获取成员 
请求头 Cookie: bearychat_517=??? 

~~~[api:bearychat]
get:/api/members
bool:all=true#获取全部
<<<
return
{
   "result" : [
		{
            "inactive": false,
            "role": "owner",
            "read_ts": 0,
            "email": "yangyufan@xmzhen.com",
            "star_id": null,
            "presence": "online",
            "latest_ts": 0,
            "pinyins": "canisminor,fanshugege,panshugege,fsgg,psgg",
            "dnd": {
                "manual_enabled": true,
                "start": "22:00:00+0800",
                "end": "07:00:00+0800",
                "schedule_enabled": false
            },
            "updated": "2016-09-30T02:22:55.000+0000",
            "name": "canisminor",
            "pinyin": [
                "canisminor",
                "fanshugege",
                "panshugege",
                "fsgg",
                "psgg"
            ],
            "index_symbol": "c",
            "met_before": true,
            "type": "normal",
            "created": "2016-07-06T04:43:49.000+0000",
            "vchannel_id": "=VmTbVypC",
            "email_verified": true,
            "mobile_verified": false,
            "hidden": true,
            "id": "=bwHFw",
            "position": "UED",
            "avatars": {
                "small": "https://dn-bearychat.qbox.me/FtR5JrI0GdBtHrwNDiId23Tu-2Ud?imageView2/1/w/180/h/180",
                "medium": "https://dn-bearychat.qbox.me/FtR5JrI0GdBtHrwNDiId23Tu-2Ud?imageView2/1/w/360/h/360",
                "large": "https://dn-bearychat.qbox.me/FtR5JrI0GdBtHrwNDiId23Tu-2Ud?imageView2/1/w/720/h/720"
            },
            "team_id": "=bw8Fc",
            "full_name": "番薯哥哥",
            "mobile": "15305853008",
            "unread_count": 0,
            "avatar_url": "https://dn-bearychat.qbox.me/FtR5JrI0GdBtHrwNDiId23Tu-2Ud",
            "conn": "disconnected"
        },
        ...
	]
}
~~~

### 获取机器人

~~~[api:bearychat]
get:/api/robots
bool:all=true#获取全部
<<<
return
{
   "result" : [
		{
                  "inactive": false,
                  "description": null,
                  "deleted": false,
                  "meta": {},
                  "pinyins": "trelloued",
                  "updated": "2017-02-13T09:09:59.000+0000",
                  "uid": "=bwHFw",
                  "name": "Trello-UED",
                  "pinyin": [
                      "trelloued"
                  ],
                  "type": "trello",
                  "created": "2017-01-11T09:38:19.000+0000",
                  "vchannel_id": "=bwDmm",
                  "channel_id": "=bwDmm",
                  "token": "77c23fbcfd0ddb1e25a0bdc4c37f7b90",
                  "status": "ok",
                  "id": "=bwE4x",
                  "target_vchannel_id": "=bwDmm",
                  "avatars": {
                      "small": "https://dn-bearychat.qbox.me/robot_trello.png?imageView2/1/w/180/h/180",
                      "medium": "https://dn-bearychat.qbox.me/robot_trello.png?imageView2/1/w/360/h/360",
                      "large": "https://dn-bearychat.qbox.me/robot_trello.png?imageView2/1/w/720/h/720"
                  },
                  "team_id": "=bw8Fc",
                  "thirdparty_url": "https://api.trello.com/1/webhooks/58a177854d39a83ee22a9544",
                  "avatar_url": "https://dn-bearychat.qbox.me/robot_trello.png"
		},
        ...
	]
}
~~~

### 获取某个频道下的消息

~~~[api:bearychat]
get:/api/vchannels/:channelId/messages
number:limit=50#获取全部
<<<
return
{
   "result" : [
		{
                  "inactive": false,
                  "description": null,
                  "deleted": false,
                  "meta": {},
                  "pinyins": "trelloued",
                  "updated": "2017-02-13T09:09:59.000+0000",
                  "uid": "=bwHFw",
                  "name": "Trello-UED",
                  "pinyin": [
                      "trelloued"
                  ],
                  "type": "trello",
                  "created": "2017-01-11T09:38:19.000+0000",
                  "vchannel_id": "=bwDmm",
                  "channel_id": "=bwDmm",
                  "token": "77c23fbcfd0ddb1e25a0bdc4c37f7b90",
                  "status": "ok",
                  "id": "=bwE4x",
                  "target_vchannel_id": "=bwDmm",
                  "avatars": {
                      "small": "https://dn-bearychat.qbox.me/robot_trello.png?imageView2/1/w/180/h/180",
                      "medium": "https://dn-bearychat.qbox.me/robot_trello.png?imageView2/1/w/360/h/360",
                      "large": "https://dn-bearychat.qbox.me/robot_trello.png?imageView2/1/w/720/h/720"
                  },
                  "team_id": "=bw8Fc",
                  "thirdparty_url": "https://api.trello.com/1/webhooks/58a177854d39a83ee22a9544",
                  "avatar_url": "https://dn-bearychat.qbox.me/robot_trello.png"
		},
        ...
	]
}
~~~

### 获取当前登录用户信息

可获取websocket 地址

~~~[api:bearychat]
get:/api/current_user
<<<
return
{
    "code": 0,
    "result": {
        "user": {
            "inactive": false,
            "role": "owner",
            "features": [
                "dnd-mode"
            ],
            "email": "yangyufan@xmzhen.com",
            "authed": [
                "trello",
                "evernote",
                "teambition",
                "shimo"
            ],
            "presence": "online",
            "dnd": {
                "manual_enabled": true,
                "start": "22:00:00+0800",
                "end": "07:00:00+0800",
                "schedule_enabled": false
            },
            "updated": "2016-09-30T02:22:55.000+0000",
            "name": "canisminor",
            "type": "normal",
            "created": "2016-07-06T04:43:49.000+0000",
            "email_verified": true,
            "guides": {
                "tour": false,
                "fav": false,
                "search": false,
                "help": false,
                "files": false,
                "shortcuts": false
            },
            "mobile_verified": false,
            "preference": {
                "sound": true,
                "desktop_notification": "at",
                "self_typing_visibility": "visible",
                "notification": "all",
                "robot_notification": true,
                "theme": "light",
                "email_visibility": "visible",
                "mention": "half_hour",
                "language": "zh-CN",
                "mobile_visibility": "visible",
                "mobile_notification_mute": true,
                "desktop_robot_notification": true,
                "leftbar_mode": "default",
                "typing_visibility": "visible"
            },
            "id": "=bwHFw",
            "position": "UED",
            "avatars": {
                "small": "https://dn-bearychat.qbox.me/FtR5JrI0GdBtHrwNDiId23Tu-2Ud?imageView2/1/w/180/h/180",
                "medium": "https://dn-bearychat.qbox.me/FtR5JrI0GdBtHrwNDiId23Tu-2Ud?imageView2/1/w/360/h/360",
                "large": "https://dn-bearychat.qbox.me/FtR5JrI0GdBtHrwNDiId23Tu-2Ud?imageView2/1/w/720/h/720"
            },
            "team_id": "=bw8Fc",
            "full_name": "番薯哥哥",
            "mobile": "15305853008",
            "avatar_url": "https://dn-bearychat.qbox.me/FtR5JrI0GdBtHrwNDiId23Tu-2Ud"
        },
        "ws_host": "wss://rtm.bearychat.com/nimbus/ws:8b832f0ddf7eac1b677ac7d53906ac09",
        "tcp_path": "rtm01.bearychat.com:5222",
        "tcp": {
            "url": "rtm01.bearychat.com:5222",
            "key": "tcp:18f83ae0244dbd2ab9cf904712b047b1"
        },
        "web_version": "8634aec568fd594f9576cb32c15cd5c43f66d78a"
    }
}
~~~

- 扩展阅读: <https://www.zybuluo.com/electricface/note/139048>

