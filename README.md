# GenshinUID / 原神UID查询

一个HoshinoBot插件，用于查询原神UID信息，用于查询树脂/探索派遣状态，推送树脂快满了，每日签到。

**一定要读更新记录和指令！！**

注意：本插件不包含本体，您应该配合[Mrs4s](https://github.com/Mrs4s) / [go-cqhttp](https://github.com/Mrs4s/go-cqhttp) 和 [HoshinoBot](https://github.com/Ice-Cirno/HoshinoBot) 使用，本插件的作用是利用米游社API查询指定原神UID信息（Cookies获取可前往[YuanShen_User_Info](https://github.com/Womsxd/YuanShen_User_Info)查看教程）

再次提醒：**Cookies是重要信息，请不要随意泄露！！！**

示例：	![1](https://raw.githubusercontent.com/KimigaiiWuyi/GenshinUID/main/readme/1.PNG)

- [安装（HoshinoBot）](#安装（HoshinoBot）)
- [更新记录](#更新记录)
- [指令](#指令)
- [相关仓库](#相关仓库)
- [其他](#其他)

## 安装（HoshinoBot）

​	基于[Mrs4s](https://github.com/Mrs4s) / [go-cqhttp](https://github.com/Mrs4s/go-cqhttp) 和 [HoshinoBot](https://github.com/Ice-Cirno/HoshinoBot) 的插件，请确保你知晓HoshinoBot的插件安装方法和go-cqhttp的使用方法。

1、在hoshino/modules目录下执行

```sh
$ git clone https://github.com/KimigaiiWuyi/GenshinUID.git
```

2、进入GenshinUID文件夹内，安装依赖库

```sh
$ pip3 install -r requirements.txt
```

3、在hoshino/config的`__bot__.py`文件中，添加GenshinUID

4、启动HoshinoBot后，私聊机器人，发送

```sh
添加 cookies
```

注意事项：可以添加多条，但一次只能添加一条，添加两个字的之后必须带有空格，cookies填入你自己的，**并且不要泄露给任何人**，~~如果添加了错误的cookies，会导致一系列问题，如果想删除错误的cookies，请操作sqlite数据库完成~~，目前已实现Cookies校验，如果校验失败，请检查Cookies是否按照格式输入。

5、进入机器人在的群聊，即可正常使用本插件。

## 更新记录

**（作者已经转用NoneBot2，Hoshino的更新可能未经测试，有bug及时提Issues！）**

#### 2021-12-04

修复：`查询词云`功能失效的问题。

修复：`查询`功能只能查到8个角色的问题（经测试应该BanIP概率极低，需要在配置文件中加入`genshinuid_use_new_get_chars_method=1`才可生效）。

修复：`校验全部Cookies`命令错误的问题（**由于API返回字段变化的缘故，旧版本使用该命令会清空所有Ck，旧版本请不要使用该命令**），该问题同时导致`添加`命令不可用，均已修复。

优化：查询时优先从数据库中调用主人的Cookies。

优化：错误Cookies将在`NewCookiesTable`中的`Extra`标记为`error`(失效)或者`limit30`(今天达到30人限制)，其中`limit30`将在每日零点清空。

#### 2021-11-21

新增：`查询词云`功能

优化：`命座\dxx`

修改：默认背景图

#### 2021-11-18

修复：最新的深渊查询返回数据

修复：wiki百科接口

调整：默认背景图

#### 2021-11-14

新增：NoneBot2分支（前往NoneBot分支查看）

新增：原神wiki功能（beta），特别感谢[minigg](https://www.minigg.cn/)提供的Api调用，使用方式查看[指令](#指令)。

#### 2021-10-24

修复：Cookies池中存在失效Cookies时可能导致自动签到不正常运作

新增：每月统计的命令（该功能需要Cookies），具体使用可以前往[指令](#指令)处查阅。

优化：添加了部分代码的注释

#### 2021-10-24

**重要：目前Cookies池又采用了新的方式（去除冗余），如果你是上个版本的使用者，请在更新后使用群聊命令：优化Cookies，无损迁移旧版本全部Cookies；（如果你是上上个版本的使用者，更新后使用命令：迁移Cookies）**

修复：可能会导致的添加cookies问题

新增：绑定Cookies后可以实现米游社签到，如果开启自动签到之后，可以每天0:30准时签到，具体使用可以前往[指令](#指令)处查阅。

#### 2021-10-17

**重要：目前Cookies池采用了新的方式，如果你是之前版本的使用者，请在更新后使用群聊命令：迁移Cookies，无损迁移旧版本全部Cookies**

新增：奇馈宝箱的支持，以及新UI的调整。

新增：绑定Cookies可以实现基于当前绑定uid信息的树脂查询，以及推送，具体使用可以前往[指令](#指令)处查阅。

新增：可以查询深渊总览信息（beta），具体使用可以前往[指令](#指令)处查阅。

新增：可以群内@某人查询（角色信息、深渊总览、深渊固定层数），具体使用可以前往[指令](#指令)处查阅。

优化：更换了背景图，更新了readme的指令表格。

优化：支持群内命令：校验全部Cookies，以此判断是否Cookies池有失效CK。

修复：在查询深渊时背景图片无法正确缩放的问题。

修复：极少数情况下，查询功能失效的实例（先uid查询后mys查询）。

#### 2021-9-27

​	新增：Cookies次数防浪费机制（查过的mysid/uid会锁定使用过的cookies，当天再查时会使用同样的cookies防止次数浪费，每日零点清空。）

​	优化：Cookies填入现在需要私聊bot，可以设置多条，并且不会随着git pull而需要重新设置。

​	优化：白色底图现在的透明度会更高。

​	修复：使用心海刷新深渊记录时，尝试查询深渊时无法输出正确的结果。

#### 2021-9-20

​	新增：米游社id查询（指令示例：mys123456789），该方法同样支持深渊查询，（指令示例：mys123456789深渊12）.

​	新增：支持绑定（指令示例：绑定uid123456789；指令示例：绑定mys123456789），二选一绑定或者都绑定也可，自动优先调用mys命令。

​	新增：绑定后可查询（指令示例：查询），同时支持深渊查询（指令示例：查询深渊12），该指令同时支持自定义图片，（指令示例：查询[此处应有图片]）

​	修复：修复图片拉伸比例不正确等问题。

​	优化：现在输出的图片质量默认为90%，优化发送速度。

​	优化：文件夹目录的bg文件夹可自由添加背景随机图库。

​	优化：优化代码结构

#### 2021-9-7

​	修改了米游社的salt值[@Azure](https://github.com/Azure99)，修复了米游社ds算法[@lulu666lululu](https://github.com/lulu666lulu)

​	更换了新ui+新背景画面。

​	添加了自动下载拼接头像、武器的程序，以后理论上游戏更新也通用。

​	uid命令现在可以根据角色数量自动设定长宽，并且自定义背景仍然适用！并且添加了角色当前携带的武器ui界面。

​	UID命令在uid命令的基础上删除了武器的ui界面。

​	添加了深渊查询，指令：uidxxxxxx深渊xx，例如uid123456789深渊12，只能查指定楼层（beta）

​	删除角色命令。

#### 2021-8-14

​	修复宵宫和早柚可能导致的输入错误bug。

​	增加了简易的cookies池，现在填写cookies的方法在函数cache_Cookie()中的cookie_list中，支持多个cookies共同使用。

​	增加了新功能（beta），使用uid+九位数字+角色的方式触发，获取全部角色+武器信息。

​	增加了新的默认随机图，简单修改了部分ui。

#### 2021-8-05

​	修复自定义图片时，竖屏图片可能造成黑边问题。

​	降低高斯模糊值。

#### 2021-8-01

​	添加自定义背景图。

#### 2021-7-29

​	优化排序算法。

#### 2021-7-28

​	添加排序算法。

#### 2021-7-26

​	完成主体。

#### 2021-7-18

​	本项目开坑。

## 指令

（**括号内为可选词缀**，以下所有可以输出图片的，**命令后跟图可自定义背景图片**）：

| 触发前缀               | 触发后缀/备注          | 效果                                   | 举例               | 备注                                     |
| :--------------------- | ---------------------- | -------------------------------------- | ------------------ | ---------------------------------------- |
| uid                    |                        | 获取角色信息一览（带武器信息）         | uid123456789       |                                          |
| uid                    | （上期）深渊           | 获取角色深渊总览（层数为最后一层）     | uid123456789深渊   |                                          |
| uid                    | （上期）深渊9/10/11/12 | 获取角色深渊某一层数据                 | uid123456789深渊12 |                                          |
| mys                    |                        | 角色信息（带武器信息，冒险等级）       | mys123456          | 米游社通行证                             |
| mys                    | （上期）深渊           | 获取角色深渊总览（层数为最后一层）     | mys123456深渊      | 米游社通行证                             |
| mys                    | （上期）深渊9/10/11/12 | 获取角色深渊某一层数据                 | mys123456深渊12    | 米游社通行证                             |
| UID                    |                        | 获取角色信息一览（不带武器信息）       | UID123456789       | 旧版本，比例更和谐                       |
| 绑定uid                |                        | 当前qq号关联绑定uid                    | 绑定uid123456789   | 查询前缀前置条件                         |
| 绑定mys                |                        | 当前qq号关联绑定米游社通行证           | 绑定mys12345678    | 查询前缀前置条件                         |
| 查询                   |                        | 查询当前绑定角色信息一览               | 查询               | **必须**绑定过mys/uid                    |
| 查询（上期）深渊       |                        | 查询当前绑定角色深渊总览               | 查询深渊           | **必须**绑定过mys/uid                    |
| 查询（上期）深渊\d     |                        | 查询当前绑定角色深渊某一层数据         | 查询深渊10         | **必须**绑定过mys/uid                    |
| 添加                   |                        | 向cookies池添加cookies                 | 添加 _ga=balabala  | **私聊**bot，注意空格                    |
| 查询 @人               |                        | 获取@的群友的角色信息一览              | 查询 @Wuyi         |                                          |
| 查询（上期）深渊 @人   |                        | 获取@的群友的深渊信息一览              | 查询深渊 @Wuyi     |                                          |
| 查询（上期）深渊\d @人 |                        | 获取@的群友的深渊某一层数据            | 查询深渊10 @Wuyi   |                                          |
| 当前状态               |                        | 获取树脂、每日委托、派遣等信息         | 当前状态           | **必须**绑定过CK和uid                    |
| 开启推送               |                        | 开启推送，超过140树脂提醒旅行者        | 开启推送           | 群聊/私聊都可<br />**必须**绑定过CK和uid |
| 关闭推送               |                        | 关闭树脂快满的提醒                     | 关闭推送           | 都可以                                   |
| 校验全部Cookies        |                        | 校验当前池内全部Cookies状态            | 校验全部Cookies    | **群聊**                                 |
| 迁移Cookies            |                        | 迁移旧版本（上上个版本）全部Cookies    | 迁移Cookies        | **群聊**                                 |
| 优化Cookies            |                        | 优化上个版本全部Cookies                | 优化Cookies        | **群聊**                                 |
| 签到                   |                        | 米游社签到                             | 签到               | **必须**绑定过CK和uid                    |
| 开启自动签到           |                        | 开启每日米游社签到                     | 开启自动签到       | 群聊/私聊都可<br />**必须**绑定过CK和uid |
| 关闭自动签到           |                        | 关闭每日米游社签到                     | 关闭自动签到       | 群聊/私聊都可<br />**必须**绑定过CK和uid |
| 每月统计               |                        | 查询当前绑定账号的每月/每日的原石/莫拉 |                    | 仅限群聊，**必须**绑定Cookies和uid       |
| 武器                   |                        | 查询武器信息                           | 武器天空之卷       |                                          |
| 命座\d                 |                        | 查询角色命座信息                       | 命座6可莉          |                                          |
| 角色                   |                        | 查询角色简略信息                       | 角色可莉           |                                          |
| 查询词云               |                        | 查询绑定角色的词云                     | 查询词云           | 必须绑定过UID/MYSID                      |

### 深渊查询：

![2](https://raw.githubusercontent.com/KimigaiiWuyi/GenshinUID/main/readme/2.png)

### 当前状态：

![3](https://raw.githubusercontent.com/KimigaiiWuyi/GenshinUID/main/readme/3.png)

### 签到：

![3](https://raw.githubusercontent.com/KimigaiiWuyi/GenshinUID/main/readme/4.PNG)

### 查询词云：

![3](https://raw.githubusercontent.com/KimigaiiWuyi/GenshinUID/main/readme/5.PNG)

## 相关仓库

- [PaimonBot](https://github.com/XiaoMiku01/PaimonBot) - 插件原始代码来自于它
- [YuanShen_User_Info](https://github.com/Womsxd/YuanShen_User_Info) - 米游社API来自于它

## 其他

​	代码写的很烂，勿喷，有问题可以发issues/Pull Requests~

​	顺便求个star~
