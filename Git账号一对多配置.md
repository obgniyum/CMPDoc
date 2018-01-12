# 同一台电脑，同一邮箱（帐号）与多个git仓库关联

> 制作背景：
> 之所以制作此文档是因为 github 协作开发需要获取写作者的公钥，并且一个公钥只能被一个项目或者账号占用，解决办法就是“同一台电脑，同一邮箱（帐号）与多个git仓库关联”。



### 一、制作第一把密钥
###### 1.1 切换到用户主目录下

	cd ~/
	
###### 1.2 生成密钥（一路默认）

	ssh-keygen -t rsa -C "yourEmail"
	
###### 1.3 修改生成的密钥对文件名称（建议私钥、公钥对应修改，修改是为了后续账号不覆盖之前的密钥）

> 修改后的文件名称如：id\_rsa\_aaa,  id\_rsa\_aaa.pub
	
###### 1.4 添加到SSH agent中(后续如果对之前的文件进行修改依然需要执行此步骤)

	ssh-add id_rsa_aaa
	
### 1.5 配置config文件

#### 1.5.1 查看当前 .ssh 目录下是否有 config 文件
	
	ls
	 
#### 1.5.2 如果没有创建一个(如果有，略过此步骤)
	
	touch config
	
#### 1.5.3 编辑 config 文件

	vim config
	
#### 1.5.4 示例如下：
>
	Host aaa
	HostName github.com
	User git
	IdentityFile ～/.ssh/id_rsa_aaa
	

#### 1.5.5 查看生成的公钥给对应代码托管者
	
	cat id\_rsa\_aaa.pub
	
## 二、制作第 N 把密钥

### 2.1 重复步骤一

## 三、使用

### 3.1 克隆
#### 3.1.1 原克隆代码需要操作如下：
 
	git clone git@github.com:<githubname>/<repositoryName>.git
	
#### 3.1.2 现克隆代码需要操作如下：
 
	git clone aaa:<githubname>/<repositoryName>.git
