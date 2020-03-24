# Get-URLs-on-WeChat-Accounts--people.cn
获取人民日报公众号推文标题和链接


## 工具
### Anyproxy
![](https://i.imgur.com/tyuccy6.png)

### MUMU模拟器
![](https://i.imgur.com/J5LntK1.png)

### bejson
http://www.bejson.com/
“格式化校验”按钮一键处理格式

## 原理
* 环境：windows
* npm: 6.13.4
* node: 12.16.1
* anyproxy: 4.1.2

1. npm安装AnyProxy
```
npm install -g anyproxy
```

2. CMD运行AnyProxy
```
anyproxy -i
```

3. MUMU WIFI设置代理到本机IP（如192.168.1.xxx），端口8001
![](https://i.imgur.com/m4b6gmG.png)

4. 本机打开http://localhost:8002/ 监听

5. MUMU上下载并登陆微信，随便打开一篇推文，在AnyProxy界面可以看到一条对应的get，可以通过筛选“s?_”得到。打开response搜索“uin”可以找到对应该公众号的编号，比如人民日报的是“MjM5MjAxNDM4MA”。

6. 在微信里打开如下链接：
```
https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=[***]==&scene=123#wechat_redirect
```
其中[***]处是公众号的编号。于是打开了旧版的公众号推文历史记录界面。（新版的用AnyProxy会看到不一样的现象，所以不能直接看公众号历史记录）。

7. 在历史记录里面不停翻页，则可以在AnyProxy里面通过筛选“action=getmsg”找到翻页后刷新的新推文，AnyProxy里面每条记录会对应10篇因为一次刷新会get10篇文章。（建议找个物理外挂办法滑动滚轮，或者模拟滚轮事件，不然很费手指头）

8. 从每条记录-response-preview里面可以看到json，复制到http://www.bejson.com/里面“格式化校验”，然后处理里面的list就行了。
