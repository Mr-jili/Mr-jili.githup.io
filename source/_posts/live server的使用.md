---
title: live server的具体作用
date: 2018-09-04 9:40
tags: node
categories: Diary
keywords: [node]
---
live server的作用：
>live-server可以帮助我们前端人员搭建临时的http服务器。它不需要安装任何插件，使用起来比较便捷。它可以自动打开项目；修改本地文件后，浏览器能够立即同步，自动加载，自动刷新。
>在package中增加代码
```
"scripts": {
    "server": "live-server ./ --port=8081"
}
```

live server的参数
```
live-server --port=8083  //更改端口号
* `--port=NUMBER`     - 选择要使用的端口，默认值：PORT env var或8080 
* `--host=ADDRESS`    - 选择要绑定的主机地址，默认值：IP env var或0.0.0.0（“任意地址”）
* `--no-browser`      - 禁止自动Web浏览器启动 
* `--browser=BROWSER` - 指定浏览器使用，而不是系统默认 
* `--quiet | -q`      - 禁止记录 
* `--verbose | -V`    - 更多日志记录（记录所有请求，显示所有侦听的IPv4接口等） 
* `--open=PATH`       - 启动浏览器到PATH而不是服务器根目录 
* `--watch=PATH`      - 用逗号分隔的路径来专门监视更改（默认值：观看所有内容）
* `--ignore=PATH`     - 要忽略的逗号分隔的路径字符串（[anymatch](https://github.com/es128/anymatch) -compatible definition） 
* `--ignorePattern=RGXP`-文件的正则表达式忽略（即`.*\.jade`）（**不推荐使用**赞成`--ignore`） 
* `--middleware=PATH` - 导出.js文件的路径导出中间件功能添加; 可以是一个没有路径的名字，也不是引用`middleware`文件夹中捆绑的中间件的扩展名 
* `--entry-file=PATH` - 提供这个文件（服务器的根相对），以取代丢失的文件（对单页面应用程序有用） 
* `--mount=ROUTE:PATH` - 在定义的路线下提供路径内容（可能有多个定义） 
* `--spa`             - 将请求从/ abc转换为/＃/ abc（适用于单页面应用程序） 
* `--wait=MILLISECONDS` - （默认100ms）等待所有更改，然后重新加载 
* `--htpasswd=PATH`   - 启用期待位于PATH的htpasswd文件的http-auth 
* `--cors`            - 为任何来源启用CORS（反映请求源，支持凭证的请求） 
* `--https=PATH`      - 到HTTPS配置模块的路径 
* `--proxy=ROUTE:URL` - 代理ROUTE到URL的所有请求 
* `--help | -h`       - 显示简短的使用提示和退出 
* `--version | -v`    - 显示版本和退出
```

node中的使用
```
var liveServer = require("live-server");
 
var params = {
    port: 8181, // Set the server port. Defaults to 8080. 
    host: "0.0.0.0", // Set the address to bind to. Defaults to 0.0.0.0 or process.env.IP. 
    root: "/public", // Set root directory that's being served. Defaults to cwd. 
    open: false, // When false, it won't load your browser by default. 
    ignore: 'scss,my/templates', // comma-separated string for paths to ignore 
    file: "index.html", // When set, serve this file for every 404 (useful for single-page applications) 
    wait: 1000, // Waits for all changes, before reloading. Defaults to 0 sec. 
    mount: [['/components', './node_modules']], // Mount a directory to a route. 
    logLevel: 2, // 0 = errors only, 1 = some, 2 = lots 
    middleware: [function(req, res, next) { next(); }] // Takes an array of Connect-compatible middleware that are injected into the server middleware stack 
};
liveServer.start(params);

```
