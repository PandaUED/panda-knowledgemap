# UI命名规范

[TOC=2,3]


## 常用

- width 宽
- height 高
- pixel (px) 像素
- horizon (H) 水平
- vertical (V) 垂直
- background (bg) 背景
- border 描边
- outline 外边框
- padding 内边距
- margin 外面距
- shadow 阴影
- align 对齐
- column 列
- row 行
- flow 流
- flexible 弹性布局
- transition 转换，转场
- animation 动画


### Types 文件种类

- assets 资源
- audio 音频
- video 视频
- font 字体
- text 文本
- link 链接
- image（Img） 图片
- icon 图标
- logo 标志
- ad 广告
- document 文档
- template 模板
- kits 元件集
- mockup 模型（手机壳效果图一类）
- wireframe (low-fi) 低保真原型
- visual-flow (hi-fi) 高保真效果图


### Article 文章

- title 标题
- subtile 副标题
- content 内容
- note 注释
- comment 评论
- author 作者
- time 时间
- date 日期

### Pages 页面

- header 页头
- list 列表
- cell 表单
- menu 菜单
- screen 屏
- view 视图
- container 容器
- box 盒
- panel 面板
- card 卡片
- sheet 底部弹出菜单
- bar 栏
- footer 页脚
- splash 启动页
- home 首页
- discover 发现
- collect 收藏
- bookmark 收藏夹
- ranked 排名

### Profile 个人资料

- login 登录
- register 注册
- user 用户
- username 用户名
- nickname 昵称
- avatar 用户头像
- level (lvl) 等级
- sign 签名
- follow 关注

### Components 控件

- status-bar 状态栏
- nav-bar 导航栏
- tab-bar 标签栏
- tool-bar 工具栏
- progress-bar 进度条
- switch 切换开关
- slider 滑动器
- radio 单选框
- checkbox 复选框
- message (msg) 提示信息
- toast 轻弹窗
- dialog 对话框
- segment 分割
- mask 蒙版、遮罩

### Behavior 行为

- download 下载
- pop 弹出
- open 打开
- close 关闭
- back 返回
- input 输入
- delete 删除
- edit 编辑
- scroll 滚动
- touch 触摸
- click 点击
- press 按下
- drag 拖动
- slide 滑动
- switch 切换开关
- like 点赞

### Position 方位

- top 顶部
- middle (Mid) 中间
- bottom (Btm) 底部
- left 左
- center 中
- right 右
- first (1st) 第一
- second (2nd) 第二
- third (3rd) 第三
- forth (4th) 第三
- last 最后

### Status 状态

- default 默认
- normal 常用状态正常
- pressed 按下
- selected 选中
- disabled 禁用
- current 当前
- visited 已访问
- hover 悬停

### 常用数据类型

- arrary (a) 数组
- string (str,s) 字符串
- boolean (b) 布尔值
- function (fn) 方法
- x,y 坐标
- cx,cy 坐标差


## Components 组件

### Layout 布局

- flex 弹性布局
- wing-blank 两翼留白
- white-space 上下留白

### Navigation 导航

- drawer 抽屉
- menu 菜单
- nav-bar(Nav) 导航栏
- pagination 分页器
- popover 气泡
- segmented-control 分段器
- tabs 标签页
- tab-bar 标签栏

### DataEntry 数据输入

- button（btn） 按钮
- checkbox 复选框
- date-picker 日期选择
- image-picker 图片选择器
- input-item 文本输入
- picker-view 选择器
- picker 选择器
- radio 单选框
- range 区域选择
- switch 滑动开关
- search-bar 搜索栏
- slider 滑动输入条
- stepper 步进器
- textarea-item 多行输入

### DataDisplay 数据展示

- accordion 手风琴
- badge 徽标数
- card 卡片
- carousel 走马灯
- grid 九宫格
- icon 图标
- list 列表
- notice-bar 通告栏
- steps 步骤条
- table 表格
- tag 标签

### Feedback 反馈

- action-sheet 动作面板
- activity-indicator 活动指示器
- modal 对话框
- progress 进度条
- popup 弹出层
- toast 轻提示

### Gesture 手势

- refresh-control 下拉刷新
- swipe-action 滑动操作

### Combination 组合

- list-view 长列表
- result 结果页




## 命名法

### 中划线命名法 （前端命名法）

action-sheet

### UnderScoreCase 下划线命名法

action_sheet

### CamelCase 驼峰命名法

- 小驼峰法

除第一个单词之外，其他单词首字母大写:
actionSheet

- 大驼峰法 (帕斯卡命名法)

大驼峰法把第一个单词的首字母也大写了
ActionSheet



## BEM

BEM的意思就是块（Block）、元素（Element）、修饰符（Modifier）,是由Yandex团队提出的一种前端命名方法论。这种巧妙的命名方法让你的CSS类对其他开发者来说更加透明而且更有意义。BEM命名约定更加严格，而且包含更多的信息，它们用于一个团队开发一个耗时的大项目。


### Block，Element，Modifier

#### B： Block 

某一块展示/功能区域 比如： nav 

这个block并非inline-block里的block,而是将所有东西都划分为一个独立的模块,一个header是block,header里嵌套的搜索框是block,甚至一个icon一个logo也是block，block可以相互嵌套

#### E： Element

这块展示/功能区域里面的某个元素，比如: nav__item 

一个Block下的所有Element无论相互层级如何,都要摊开扁平的属于Block，所以 BEM 最多只有 B+E+M 三级,不可能出现 B+E+E+..+E+M 超长class名,也要求E不能同名

#### M：Modifier

某个元素或者某个块的状态，比如 nav--hide, nav__item--open 


```
B：search-bar //搜索栏
E：search-bar__icon //搜索栏图标
M：header-tabs__icon--grey //搜索栏图标灰色版
```


