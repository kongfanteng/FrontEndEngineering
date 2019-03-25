1. npm下载的资源都是在https://www.npmjs.com/中下载
`npm install xxx` ： 把资源下载的当前目录下
`npm install xxx -g` : 下载到全局

> 基于npm安装的一些细节点：
> - 需要联网
> - node_modules文件夹
> 源码+压缩版本


2. 解决下载慢的问题
`基于nrm切换到国内下载一个`：
安装nrm
> npm install nrm -g
> - nrm ls 查看当前可用源
> - nrm use xxx 使用某个源
> 切完源还是使用npm 安装

`yarn 安装管理`
> npm install yarn -g
> yarn add xxx
> yarn remove xxx
> yarn 只能安装到本地，不能安装到全局
> 

 `基于cnpm淘宝镜像`
 
 `npm uninstall xxx / npm uninstall xxx -g `：从本地或者全局卸载
 
 3. 解决安装版本问题
> 首先查看当前模块的历史版本信息
> `npm view jquery jquery.version.json` ： 把当前模块的历史信息输出到具体的某个文件中

bower 从github下载

1.安装less / babel-cli

 