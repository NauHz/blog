---
title: Hexo
date: '2022-5-23 20:53:14'
tags:
  - 笔记
categories: 博客笔记
cover: /img/Hexo.jpg
abbrlink: b314af1
top_img: "#0f4c81"
---

## 虚拟机搭建Hexo博客

下载[VMware Workstation](https://www.vmware.com/cn/products/workstation-pro/workstation-pro-evaluation.html)、[镜像操作系统](https://msdn.itellyou.cn/)、[Nodejs](http://nodejs.cn)、[Git](https://git-scm.com/)

**效验node：**`node -v`、**效验npm：**`npm -v`

**安装淘宝的cnpm 管理器：**👇

```POWERSHELL
`npm install -g cnpm --registry=http://registry.npm.taobao.org`
```

**效验cnpm：**`cnpm -v`

**安装hexo框架：**👇

成功会在目录中看到`.npminstall_tarball`文件

```POWERSHELL
`cnpm install -g hexo-cli`
```

**查看hexo版本：**`hexo -v`

**创建blog目录：**找个位置新建放blog的文件夹

**初始化博客：**在blog根目录右键点{% kbd Git Bash Here %}输入`hexo init `	

**生成网站静态文件：**`hexo s`	

**本地访问地址：**(http://localhost:4000/)

**下载butterfly主题到本地：**👇

```POWERSHELL
git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
```

**修改根目录的 _config.yml，把主题改为butterfly**👇

```YAML
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: butterfly
```

**根据butterfly博客根据自己需要装修博客：**[butterfly](https://butterfly.js.org/posts/21cfbf15/)

**在blog目录下安装git部署插件：**`cnpm install --save hexo-deployer-git `

**Github创建一个新的仓库：** `你的Github名字.github.io`

**Github用户名：**``git config --global user.name "xxx"``

**Github邮箱：**`git config --global user.email "xxx"`

>**配置_config.yml:**👇
```YAML
#Deployment
##Docs: https://hexo.io/docs/deployment.html
deploy:
type: git
repo: https://github.com/你的Github名字/你的Github名字.github.io.git
branch: master
```

**清除缓存：**`hexo clean`

**生成：**`hexo g`

**部署到Github仓库里：**`hexo d`

**访问地址即可查看博客：**(https://你的Github名字.github.io/)

**克隆仓库：**`git clone` 仓库地址、code 后在根目录安装依赖 `npm install`、在主题目录重新安装一次`hexo-theme-butterfly`

{% timeline 博客日志,blue %}

<!-- timeline 2022-05-23  -->

1. 购买[阿里云服务器ECS](https://www.aliyun.com/product/ecs?spm=5176.19720258.J_3207526240.46.70ad2c4as029Ht)

2. 重置实例密码

3. 终端输入`ssh root@服务器公网IP`

4. 输入重置的实例密码

5. [在线安装宝塔linux面板脚本](https://www.bt.cn/new/download.html)

6. 安装完成登录宝塔面板

7. 解决问题之后登陆宝塔界面，推荐安装套件选择默认LNMP极速安装

**浏览器输入地址后发现无法访问宝塔面板**
解决方案：在安全组中-快速添加-端口范围选中全部（1/65535）确定即可
<!-- endtimeline -->

{% endtimeline %}