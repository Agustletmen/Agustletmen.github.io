---
title: npm&yarn
date: 2022-05-03 12:03:35
categories: 前端开发
tags: nodejs
---
## Npm

📃[NPM 使用介绍（菜鸟教程）](https://www.runoob.com/nodejs/nodejs-npm.html)

📃[npm 中文文档](https://www.npmrc.cn/)



### 配置镜像

由于国内直接使用 npm 的官方镜像是非常慢的，这里推荐使用淘宝 NPM 镜像。

> npm.taobao.org 和 http://registry.npm.taobao.org 在 2022.06.30 号正式下线和停止 DNS 解析。
>
> 淘宝npm镜像站全新上线，Web界面地址：npmmirror.com；npm 客户端使用地址：registry.npmmirror.com

```sh
#查看正在使用的镜像地址
npm config get registry 

#设置淘宝镜像地址
npm config set registry  https://registry.npmmirror.com
```



### 使用cnpm

你可以使用淘宝定制的 cnpm 命令行工具代替默认的 npm

```sh
# 安装cnpm
npm install -g cnpm --registry= https://registry.npmmirror.com

# 这样就可以使用 cnpm 命令来安装模块了，cnpm其他命令同npm
cnpm install 模块名

# 解决Error: getaddrinfo EAI_AGAIN http://registry.npmmirror.com的问题
cnpm config set strict-ssl false
```



### 初始化项目

初始化项目，填写项目相关信息，会生成一个 **package.json**

```sh
npm init -y #-y yes
```

这个**package.json**主要是用来记录这个项目的详细信息的，我们在项目开发中所要用到的包，以及项目的详细信息等都将记录在这里。

![image-20221215175607259-16722782268441](https://agust.oss-cn-guangzhou.aliyuncs.com/images/202301012303845.png)





### 安装模块

npm 的包安装分为本地安装（local）、全局安装（global）两种

**1️⃣本地安装**

1. 将安装包放在 **node_modules** 下

2. 可以通过 `require()` 来引入本地安装的包。



**2️⃣全局安装**

1. 将安装包放在 **/usr/local** 下或者你 node 的安装目录。

2. 可以直接在命令行里使用。

```sh
# 切换到项目目录
cd project_dir

# 安装当前项目所需的所有依赖
npm install xxx       			# 本地安装
npm install -g xxx     			# 全局安装


-P,  --save-prod， --save  # 表示将模块添加到配置文件中的运行依赖中，不指定-D或-O时，默认使用此项
-D,  --save-dev	 	# 表示将模块添加到配置文件中的开发依赖，在项目最后是不需要使用这些模块的

-P, --save-prod           dependencies 依赖项安装，不指定-D或-O时，默认使用此项
-D, --save-dev            devDependencies 开发依赖项安装
-O, --save-optional     optionalDependencies 可选依赖项安装
-g, --global                 全局安装
-B, --save-bundle       bundleDependencies 依赖项安装
-E, --save-exact         明确版本号安装，不使用^符号进行默认安装。
-w, --workspace          install 命令也是支持多工作区安装的
-ws, --workspaces      设置为false时，禁用workspaces
```



[几类npm依赖包管理](https://blog.csdn.net/hujinyuan357/article/details/99621542)

1. dependencies
2. devDependencies
3. optionalDependencies
4. bundleDependencies



### 查看模块

你可以使用以下命令来查看所有全局安装的模块：

```sh
npm list -g #全局查看

npm list #查看当前项目

npm list <包名>  # 查看具体某个模块的安装信息
```





### 卸载模块

我们可以使用以下命令来卸载 Node.js 模块：

```sh
npm uninstall <模块名> 
```

卸载后，你可以到 /node_modules/ 目录下查看包是否还存在，或者使用以下命令查看：`npm ls`



### 更新模块

我们可以使用以下命令更新模块：`npm update xxx`

> [https://www.npmrc.cn/commands/npm-update.html#%E6%A6%82%E8%A6%81](https://www.npmrc.cn/commands/npm-update.html#概要)

使用以下来搜索模块：`npm search xxx`



### 清除缓存

如果你遇到了使用 npm 安 装 node_modules 总是提示报错：报错: npm resource busy or locked.....

可以先删除以前安装的 node_modules:

```sh
npm cache clean  # 清空缓存
npm install		 # 重新安装
```





### 部署项目

```sh
npm run build:stage  	# 构建测试环境
npm run build:prod  	# 构建生产环境
npm run dev  			# 开发
```

`npm run xxx`的时候，首先会去项目的`package.json`文件里找 **scripts** 里找对应的xxx，然后执行xxx的命令

![](https://agust.oss-cn-guangzhou.aliyuncs.com/images/202301012217576.png)



## Yarn

Yarn是由Facebook、Google、Exponent 和 Tilde 联合推出了一个新的 JS 包管理工具 ，正如官方文档中写的，Yarn 是为了弥补 npm 的一些缺陷而出现的。

在npm5.0之前，yarn的优势特别明显。但是在 npm5 之后，其在速度和使用上确实有了很大提升，值得尝试，不过还没有超过yarn。

https://zhuanlan.zhihu.com/p/300730415



### 配置yarn

安装yarn：

```sh
npm install -g yarn
```



如果想要升级yarn，可以先从网上查询yarn最新版本号，只要使用指定版本号的命令即可升级：

```sh
npm install yarn[@version] -g
```





### 常用命令

[yarn用法](https://www.yarnpkg.cn/getting-started/usage)

```sh
yarn help # 显示命令列表

yarn init # 初始化一个新项目

yarn、yarn add # 安装所有依赖项

# 添加依赖项
yarn add [package]
yarn add [package]@[version] 
yarn add [package]@[tag]

# 将依赖项添加到不同的依赖类别中
yarn add [package] --dev  # dev dependencies 
yarn add [package] --peer # peer dependencies

# 更新依赖项
yarn up [package]
yarn up [package]@[version]
yarn up [package]@[tag]

# 列出所有包和它们的依赖
yarn list [--depth] [--pattern] 

# 运行脚本
yarn run [script] [<args>]

# 删除依赖项
yarn remove [package]

# 更新 Yarn 本体
yarn set version latest yarn set version from sources
```



### 配置镜像

```sh
yarn config get registry  #查看镜像

yarn config set registry https://registry.npmmirror.com  # 使用淘宝镜像
```
