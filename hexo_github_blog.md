# Hexo + Github 搭建个人博客 

------

一直很项目那些有个人博客的人，于是决定自己也搞一个玩一玩。经过各种百度后最终选择使用Hexo + Github 搭建个人博客。主要优点在于简约方便（主要是免费，因为github本身给提供了300M的空间足够我们自己嗨）。下面我们开始搭建我们的博客。

> * 安装环境 （Node Npm Gitshell）
> * 下载Hexo文件
> * 初始化博客目录
> * 配置Hexo主题文件和更换主题
> * 测试本地博客并上传
> * 部署到Github
> * 访问Github主页地址（检查线上博客是否正确）
> * 博客站点的SEO优化


------

## 安装环境

### 1. 安装Node.js 

下载并安装 [Node.js](https://nodejs.org/en/)

### 2. 安装 GitHub for Windows

下载安装 [GitHub for Windows](https://desktop.github.com/)

### 3. 检测是否安装成功

```
$ node -v        // v6.3.1
$ npm -v         // 3.10.3
$ git --version  // git version 2.11.0.windows.3
```

---

## 下载Hexo文件

打开GitShell，输入命令`cd /`，进入C盘根目录，之后输入命令`npm install hexo-cli -g`

```
$ cd /
$ npm install hexo-cli -g

```
效果图如下：
![](http://img.blog.csdn.net/20160313101138688)

## 初始化博客目录

打开GitShell，命令`cd /`进入C盘根目录，命令`hexo init Hexo` **Hexo** 为文件名（可以自己随便命名）如下图：
![](http://img.blog.csdn.net/20160313101840894)

成功后显示如图：
![](http://img.blog.csdn.net/20160313101840894)

此时C盘已经有了Hexo文件夹以及一些文件资源
![](http://img.blog.csdn.net/20160313102932368)

接下来，在本地预览博客页面效果，在Hexo目录依次输入命令：

```
$ hexo generate
$ hexo server  
    
```
第二个命令输入后回车完成后系统会提示是否允许访问，点允许即可。如图：

![](http://img.blog.csdn.net/20160313103426275)

安装后的目录结构

```
.
├── .deploy       #需要部署的文件
├── node_modules  #Hexo插件
├── public        #生成的静态网页文件
├── scaffolds     #模板
├── source        #博客正文和其他源文件, 404 favicon CNAME 等都应该放在这里
|   ├── _drafts   #草稿
|   └── _posts    #文章
├── themes        #主题
├── _config.yml   #全局配置文件
└── package.json

```

如果上图最后一行提示，在浏览器中输入[http://localhost:4000/](http://localhost:4000/)

如果在浏览器中不能访问，可能是4000端口被占用（输入命令`hexo server -p 5000`即可）

`Ctrl + C`是停止该服务，停止后浏览器中该地址是打不开的。

博客页面效果如下：
![](http://img.blog.csdn.net/20160313103832755)

首次安装默认的主题（如果想换主题后面会提到）

## 部署到Github

打开GitShell输入命令`ssh -T git@github.com`

```

ssh -T git@github.com

// 如果出现successful字样这说明，github已经配置过了
// 如果出现 `Permission denied <publickey>`
// 需要配置 在本地配置rsa文件并保存在github的`SSH and GPG keys`
// 具体请参考文章[https://github.com/smileyby/helloWorld](https://github.com/smileyby/helloWorld)这里不再赘述


```

## 配置Hexo主题文件和更换主题

### 选择主题

主题从哪里找？官方就有一些[主题](https://hexo.io/themes/)，可以从中选择。官方提供的主题不少，可是并不一定有自己喜欢的或者有很难选择，这是个头疼的问题。之前我都是随便挑一个看着顺眼的就过去了。

但在使用过程中发现一些问题：

*   不会自动生成目录
*   不会自动获取摘要
*   有很多配置不太方便

通过多方搜索，最终在知乎上找到了答案[有哪些好看的 Hexo 主题？](https://www.zhihu.com/question/24422335),第一名的[next](https://github.com/iissnan/hexo-theme-next)主题简约，配置详细，能够解决上面所说的问题。

下面以更换next为例，开始更换主题：

### 安装主题

打开Gitshell，在前面创建的Hexo文件夹下输入命令`git clone https://github.com/iissnan/hexo-theme-next themes/next`

修改博客目录`C:\Hexo\_config.yml`中的theme属性，将其设置为`next`

```

theme: next

```

#### 配置菜单

在`C:\Hexo\themes\next\_config.yml`文件中找到menu选项，标签可以使用中文，需要配置语言为中文，下面是next默认给出的配置：

```

menu:
  home: /
  categories: /categories
  about: /about
  archives: /archives
  tags: /tags
  search: /search
  sitemap: /sitemap.xml
  commonweal: /404.html

```

#### 新建标签页和分类页

```

hexo new page tags
hexo new page categories

```

输入命令后，会在`C:\Hexo\source`目录下生成两个文件夹 `tags` `categories`,在这两个文件夹里面都会自动生成一个.md的文件。

修改里面的配置

* categories

```

title: 分类
date: 2017-03-19 14:33:00
type: "categories"

```

* tags

```

title: 分类
date: 2017-03-19 14:33:00
type: "tags"

```

#### 配置检索功能

在站点的根目录下执行以下命令：

```

npm install hexo-generator-search --save

npm install hexo-generator-searchdb --save

```

#### 启用检索功能

在根目录下的`_config.yml`文件任意位置，新增如下代码

```

search:
  path: search.xml
  field: post
  format: html
  limit: 10000

```

#### 添加友情链接

在根目录下的`C:\Hexo\themes\next\_config.yml` 

```

# Blog rolls
links_title: Links            // 友情链接的标题
#links_layout: block
#links_layout: inline
links:
  Title: http://example.com/  // 具体的链接

```

#### 开启打赏功能
在根目录下的`C:\Hexo\themes\next\_config.yml` 

```

reward_comment: 坚持原创技术分享，您的支持将鼓励我继续创作！
wechatpay: /path/to/wechat-reward-image
alipay: /path/to/alipay-reward-image

```

#### 侧边栏社交功能
在根目录下的`C:\Hexo\themes\next\_config.yml` 

```

# Social links
social:
  GitHub: https://github.com/your-user-name
  Twitter: https://twitter.com/your-user-name
  微博: http://weibo.com/your-user-name
  豆瓣: http://douban.com/people/your-user-name
  知乎: http://www.zhihu.com/people/your-user-name
  # 等等

```

##### 配置文章阅读量

[https://notes.wanghao.work/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html#%E9%85%8D%E7%BD%AELeanCloud](https://notes.wanghao.work/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html#%E9%85%8D%E7%BD%AELeanCloud)

更多配置信息详见[http://theme-next.iissnan.com/getting-started.html](http://theme-next.iissnan.com/getting-started.html)






## 测试本地博客并上传

配置完成后在博客文件夹根目录下`C:\Hexo`运行一下命令：

```

hexo clean        // 清除缓存
hexo generate     // 生成静态网页
hexo server       // 本地预览
hexo deploy       // 部署至github

```

## 访问Github主页地址（检查线上博客是否正确）

现在我们就可以访问，自己的博客啦。
https://github_userName.github.io

## 博客站点的SEO优化

SEO优化可以参考文章:

    [1]: http://blog.csdn.net/qq_23435721/article/details/50997275
    [2]: http://www.jianshu.com/p/86557c34b671
    [3]: http://blog.csdn.net/zaoan_wx/article/details/50859675
    [4]: http://www.07net01.com/2016/10/1692936.html
    [5]: http://www.arao.me/2015/hexo-next-theme-optimize-seo/

------
作者 [@smileyby]     
2017 年 03月 23日    

参考文档：

    [1]: https://segmentfault.com/a/1190000002632530
    [2]: http://www.jianshu.com/p/db7e64d86067
    [3]: http://blog.csdn.net/qq_23435721/article/details/50875579