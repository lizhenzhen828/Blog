最近开始学习nodeJS，简单学习了一下之后开始搭建自己的第一个nodeJS程序，把整个流程梳理了一下。

首先编写package.json，或者用npm init 命令初始化

	$npm init

生成的pachage.json如下

	{
	  "name": "news project",
	  "version": "1.0.0",
	  "description": "nodejs Project module",
	  "main": "bin/www",
	  "scripts": {
	    "test": "echo \"Error: no test specified\" && exit 1"
	  },
	  "keywords": [
	  ],
	  "author": "cy",
	  "license": "ISC",
	  "dependencies": {
	    "body-parser": "^1.15.1",
	    "express": "^4.13.4"
	  }
	}

用命令npm install来安装node所需的各个模块

	$ npm install

如下是我的代码的目录结构

>![img](/img/first_nodeJS/mulu.png)

### 文件结构

/app下面有三个文件夹，分别是controllers、models以及routes。

>controllers提供了控制器，将各种业务对数据库的直接操作进行了封装。命名规范：function.controllers.server.js。

>models中初始化各个模块。命名规范：function.model.server.js。

>routes则在里面添加不同的路由，可以使代码更加清晰。命名规范：function.routes.server.js。

/bin下面的www文件是node程序的入口文件。

/config下面的env存放各种配置，其他的文件如(express.js、mongoose.js)提供了express等功能等接口，并进行初始化。

/node_modules存放了npm install下载的各个模块。

/app.js由www调用，初始化各个config中的功能模块。

<br><br>

每个模块通过module.exports给调用方提供接口，或者调用方可以直接require执行模块中的代码。

<br><br>


### 介绍一下整个流程。

前端发过来的请求，根据路由会在news.server.routes.js中做判断，app.route方法为后端代码添加支持不同的路由，根据不同路有掉用不同Controller代码进行数据库操作，进行数据的增删改查，然后将得到的信息或者结果通过res参数返回。整个http请求也就完成了。

我在路由代码中加入了‘／’的判断，在为根目录时返回index.html页面。调用require('fs').readFile读取html文件并将它写入到res中。一开始用require('fs').readFile直接将路径写成了'../../index.html'，后来才发现它的路径是根据程序运行的路径而不是当前文件的路径，用__dirname的到当前文件路径即可。

更新：后来改为了用ejs来渲染前端页面。

<br><br>

### 最后附上源代码[点击下载](/file/newsProject.zip)


