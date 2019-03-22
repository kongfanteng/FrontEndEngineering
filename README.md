# git操作
>`https://github.com`：git仓库网址，提供代码管理的公共平台，组件/类库/插件/框架，开源平台
>
> git作用
> - 创建仓库，管理自己的项目文件
> - 代码推送指定的仓库
> - 静态web页面的发布
>
> 国内git：coding，资源较少
> 
> 基于github创建仓库
# git 基础知识
> git 是一个“分布式”代码版本管理控制系统
> - 记录当前产品的所有版本信息，回退某一个版本
> 团队协作开发，解决冲突，合并代码
> 
1. 集中式：
    -  中央服务器（版本信息，最新代码管理）
    - 本地开发的文件未提交前拉取svn，本地修改会被覆盖
    - 随时查看历史版本，必须联网操作；
2. 分布式：
    - 每个开发者本地都是一个git仓库
    - 本地可以生成历史版本
    - 集中服务器（一般github）,同步到中央服务器
    - 可以断网操作

> ps: CDN加速：地域式服务器分布管理
> `svn`：“集中式”管理
> mac安装git 1.下载Xode 2. 下载http://brew.sh brew install git
#### git的工作管理和基础操作
>初次使用，本地设置基础信息
>`git config -l`
>`git config --global user.name XXX`
>`git config --global user.email XXX`
>`git init` 
1. `git init`：  创建.git文件
2. '.gitignore'
>在当前目录创建一个 '.gitignore'文件
>编辑器创建
>集成了linux的docs命令
#### Git基础管理
>.gitignore内容`node_modules`
>交换数据
> 1.新建第三方变量 2. [g,h] = [h,g] 3.相加相减
#### GIT工作原理
> 每个git仓库三个区域
>  - 工作区，编辑代码
>  - 暂存区，临时存储版本代码
>  - 历史区，生成的历史版本代码
>  操作
>  - `git status`：查看状态，红色工作区，绿色暂存区
>  - '.git add .gitignore' :添加到暂存区
>  - `$ git add . / $ git add -A`：工作区所有文件提交到暂存区
>  - `git commit` ：提交，i 操作 :wq 保存退出
> - `git commit -m '操作'`:提交
> - `git diff`：工作区vs暂存区
> - `git log`： 记录
> - `git diff master` 工作区vs历史区
> - `git diff --cached` 暂存区vs历史区
