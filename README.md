# hexo-douban-list

[![GitHub license](https://img.shields.io/github/license/mythsman/hexo-douban.svg)](https://github.com/mythsman/hexo-douban/blob/master/LICENSE)

基于HEXO豆瓣插件 [hexo-douban](https://github.com/mythsman/hexo-douban) 的二次开发插，强烈建议先试用原插件，如果您觉得以下特性更能满足您的需要，那么再使用本插件。

主要特性：

- [原项目](https://github.com/mythsman/hexo-douban)固有特性；
- 重构模板页面，支持移动适配；
- 补全列表影评内容，支持短评和长影评（核心）；
- 支持生成指定长度的列表（对于观影数量较多的用户）；
- 样式inline化，允许直接嵌入同源其他页面；
  ``` html
  <div id="dbcontent"></div>
  <script>$('#dbcontent').load('./movies/index.html .hexo-douban-item:nth-child(1)');</script>
  ```

**注意：本插件构建的页面完全不保证兼容IE等上古浏览器，推广使用现代浏览器，人人有责。**

 
## 第一步：安装

``` bash
# 如果您使用过原插件请先卸载之
$ npm uninstall --save hexo-douban
$ npm install --save hexo-douban-list
```

## 第二步：配置

将下面的配置写入站点的配置文件 `_config.yml` 里(不是主题的配置文件).

``` yaml
douban:
  user: ID（数字或字幕|无需引号）
  builtin: true
  movie:
    title: '生成页面的标题'
    quote: '生成页面的内容的导语'
    length: 2
    valine_id: WbLE88qfAcz4hSI5
    valine_key: ycqjmtEfUxuxD
  timeout: 10000 
```

**注意：以上内容中务必确定 USER ID 的正确性！**

- **user**: 你的豆瓣ID.打开豆瓣，登入账户，然后在右上角点击 "个人主页" ，这时候地址栏的URL大概是这样："https://www.douban.com/people/xxxxxx/" ，其中的"xxxxxx"就是你的个人ID了。
- **builtin**: 是否将生成页面的功能嵌入`hexo s`和`hexo g`中，默认嵌入（TRUE）即npm安装后无需任何操作按原命令部署博客即可生效。
- **title**: 该页面的标题。
- **quote**: 写在页面开头的一段话,支持html语法。
- **length**: 默认值为2，非页数，可以自由尝试（建议取值:2-4）。
- **timeout**: 爬取数据的超时时间，默认是 10000ms ,如果在使用时发现报了超时的错(ETIMEOUT)可以把这个数据设置的大一点。

对于 `valine_id` 和 `valine_key`，主要针对的是**Volantis**主题（以及其他默认渲染评论区域的主题），如果您在测试时页面没有评论区域，则可以忽略这两项，如果出现以下显示则需要填写此两项。（这两项是什么？请移步[Valine官方介绍](https://valine.js.org/quickstart.html#%E8%8E%B7%E5%8F%96APP-ID-%E5%92%8C-APP-Key)）

![](https://cdn.jsdelivr.net/gh/TianZonglin/tuchuang/img/20200922010453.png)


## 使用


**注意**，通常大家都喜欢用`hexo d`来作为`hexo deploy`命令的简化，但是当安装了`hexo douban`之后，就不能用`hexo d`了，因为`hexo douban`跟`hexo deploy`的前缀都是`hexo d`。

## 升级

使用 `npm install hexo-douban-list --update --save` 直接更新。

## 测试

执行 `hexo clean && hexo generate && hexo server`，之后访问 `localhost:4000/movies` 即可访问生成的影评页面。

## 删除（可补回来）的内容


相比较于原项目，取消或删除了以下内容：

- 去掉了书籍和音乐，单纯针对电影
- 去掉了影评页跳转的菜单按钮
- 去掉了以上项目涉及的配置开关



## 异常

如果构建页面为空或404，且日志输出为 `INFO  0 movies have been loaded in xx ms`，这时怀疑您的IP由于多次请求豆瓣的页面而被豆瓣封禁了，一般第二天会解禁，使用代理或更改IP即可解决。
 
## 示例

https://www.cz5h.com/movies