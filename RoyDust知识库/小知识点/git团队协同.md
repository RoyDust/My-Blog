# git团队协同

```
git clone 	仓库地址  https://e.coding.net/xzlt/jishuqianduanxuexixiaozu/taskWarehouse.git
```

在项目里拉取分支

```
git pull origin main
```

```
git add .
```

```
git commit -m "熊维···"
```

```
git push origin mai
```

Git的使用,以码云为例:

码云是开源中国的代码托管平台，中文操作界面，使用十分方便。并且他使用的就是Git的技术，操作命令等和Git一模一样，客户端也是使用的同一个。

一.在码云上创建项目:

新建项目即可,会展示在项目下:

![img](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/20181116170444237.png)

二.本地需要安装Git,这里不再多说

三.上传本地代码到码云:

1.在自己的项目文件夹上右键-Git Bash Here,会弹出Git操作框

![img](https://img-blog.csdnimg.cn/20181116170858188.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3poYW5nbGVpNTAwMDM4,size_16,color_FFFFFF,t_70)

2.git身份设置，让git知道你是谁，填入你的账号和关联的邮箱

```
git config --global user.name "xxx"

git config --global user.email "xxx@qq.com"
```

3.生成公钥，填你的邮箱

```
ssh-keygen -t rsa -C "xxx@qq.com"
```

并按回车3下（为什么按三下，是因为有提示你是否需要设置密码，如果设置了每次使用Git都会用到密码，一般都是直接不写为空，直接回车就好了）

生成成功：

![img](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/20181122143840284.png)

生成之后，新项目再上传就不需要再次生成了。


4.初始化普通项目为git项目，填Git上的项目地址

```
git init 
git remote add origin "https://gitee.com/xxx/xxx.git"
```

5.提交项目

```
git pull origin master
git add .
git commit -m "第一次提交"
git push origin master
```

四.idea上使用git

1.项目上传码云后使用idea打开,通常已经与码云建立了联系

此时修改代码文件就会变成蓝色

2.将修改的文件上传

在文件上点右键-Git-Commit Directory,填写备注上传即可

![img](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/20181116171730377.png)

3.此时打开码云,发现并没有收到上传的代码

是因为刚刚走的过程中，其实还是没有走完，只是将Idea上的代码提交到了Git本地仓库，并没有将Git仓库中的代码提交到GitHub网站上

所以，还是需要将Git上的代码提交到GitHub上！

 ![img](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/978388-20180116143536646-1914535589.png)

也可以一步到位，代码提交的时候选择commit and push：

![img](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/20190327174101699.png)

4.push报错:Push rejected: Push to origin/master was rejected

基本上是因为你的项目中有和和历史不符的东西，比如新增了类 
Push rejected: Push to origin/master was rejected 
推拒绝：推送到起源/主人被拒绝 
解决办法：直接在项目的文件夹上鼠标右键git Bash Here，打开Git操作框，然后直接下面两行命令解决问题，按要求输入账号密码就行

```
git pull origin master –allow-unrelated-histories 
git push -u origin master -f
```





![logo_](https://s2.loli.net/2022/02/13/iGUyOProcKFjTIa.png)

![logo](https://s2.loli.net/2022/02/13/iSrqVfyQNvTD7kR.png)
