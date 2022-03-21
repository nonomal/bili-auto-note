# Bilibili 自动打轴助手

通过本工具可以将统一的时间轴自动转换到不同的录播笔记

首先，请准备好时间轴的 csv 文件和一个可用的 cookie 。之后按照示例准备一个配置文件

## 时间轴示例 (csv文件)

    1,开场,0
    10,这是一个简单的时间轴的示例,0
    11,用于时间轴的自动化上传测试,0
    20,第一列表示时间戳对应的时刻,1
    21,单位为秒，如这行表示第21秒,0
    22,文件中的时间戳基于开场时刻,0
    23,假设这个分p 的op的长10秒,0
    24,那么第 8行则会显示为第31秒,0
    30,第二列为时间戳对应显示内容,1
    40,第三列表示它是否为重要标记,1
    41,如果填充 0表示普通时间标记,0
    42,如果填充 1表示重要时间标记,0
    43,重要标记用红色加粗形式显示,1
    50,笔记测试结束了，大家晚安啦,0
    60,回马枪,0

## 获取 Cookie

* cookie 可使用 `F12` 开发人员工具从 Bilibili 网页端抓包
* 有了 cookie 能操作B站账号的大部分功能，切勿泄露或分享出去
* 请确保 cookie 中包含 `SESSDATA` 和 `bili_jct` 两项
* 为防广告，一些小号可能没有发布笔记的功能，请先在网页端进行发布笔记的测试
* 每人每天最多发布 5 篇笔记

接下来请按照如下形式准备配置文件

## 配置文件示例 (json文件)

    {
        "cookie": "SESSDATA=<SESSDATA>; bili_jct=<CSRF>",
        "bvid": "BV1FQ4y1R7nv",
        "timeline": "./data/timeline.csv",
        "offsets": [-10],
        "cover": "这是一个自动发布笔记的测试\n欢迎进入笔记打轴的自动化时代",
        "publish": false
    }

## 配置文件说明

`cookie`: 发送笔记用户的cookie，必须包含 `SESSDATA` 和 `bili_jct` 两项

`bvid`: 目标视频BV号

`timeline`: 时间轴文件路径

`offsets`: 目标视频每个分P开始时刻对应的统一时间轴时刻，单位为秒。注意，此处的值可能为负数（比如果统一时间轴以开场对齐，但视频中包含OP时）。
在offsets中也可以标记`auto`或`skip`，`auto`表示自动叠加上一p的累计时长，`skip`表示跳过这一p

`cover`: 视频转制通过时发送至评论区的文案

`publish`: 是否自动发布

## 使用

执行 `python bili_note.py <配置文件路径>` 即可。

## 更新计划

* 实现将文本轴转化到csv的功能
* 实现自动监测，当视频分p数量发生变化，或本地csv文件变化时自动上传笔记
* 实现时间轴转换
