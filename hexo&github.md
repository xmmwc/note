---
HEXO+Github
---

### 配置环境

安装Node（必须）

*略过。*

安装Git（必须）

*略过。*

申请GitHub（必须）

*略过。*

### 正式安装Hexo

Node和Git都安装好后,首先创建一个文件夹,如blog,用户存放hexo的配置文件,然后进入blog里安装Hexo。

执行如下命令安装Hexo：

```bash 
    $ sudo npm install -g hexo
```

初始化然后，执行init命令初始化hexo,命令：

```bash 
    $ hexo init
```

好啦，至此，全部安装工作已经完成！blog就是你的博客根目录，所有的操作都在里面进行。

生成静态页面

```bash 
    $hexo generate
```
    
（hexo g也可以）

本地启动

启动本地服务，进行文章预览调试，命令：

```bash
    $hexo server
```

浏览器输入http://localhost:4000

### 配置Github

建立Repository

建立与你用户名对应的仓库，仓库名必须为**your_user_name.github.io**，固定写法。


现在我们需要_config.yml文件，来建立关联，

翻到最下面，改成这样子的

```yml
    deploy:
        type: git
        repo: https://github.com/XXX/XXX.github.io.git
        branch: master
```


然后执行命令：

```bash
    $ npm install hexo-deployer-git --save
```


然后，执行配置命令：

```bash
    $ hexo deploy
```

然后再浏览器中输入 http://XXX.github.io/ 就行了

### 部署步骤

每次部署的步骤，可按以下三步来进行。

``` bash
	$ hexo clean
```

``` bash
	$ hexo generate
```

``` bash
	$ hexo deploy
```

一些常用命令：

```bash 
    $ hexo new "postName" #新建文章
```

```bash 
    $ hexo new page "pageName" #新建页面
```

```bash 
    $ hexo generate #生成静态页面至public目录
```

```bash 
    $ hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
```

```bash 
    $ hexo deploy #将.deploy目录部署到GitHub
```

```bash 
    $ hexo version #查看Hexo的版本
```



>文／潘柏信（简书作者）
>原文链接：http://www.jianshu.com/p/465830080ea9
