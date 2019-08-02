Eclipse:

Eclipse 高级版本自带Git，不需要安装插件。（如使用低级版本，请自己百度安装Git插件。）

将本地项目上传到Git,

流程：需要先通过Commit 传到本地仓库，然后再从本地仓库push到Git。

实例：

1. Open Eclipse， 新建项目demo

2. 项目右键， Team -> Share Project





3. 选择Git， 随后配置GIT， Configure Git Repository



在此目录下会生成一个.git 的文件夹， 此时Eclipse中文件显示？号。

4. 为新建的文件添加Index， 右键项目-＞Team->Add to Index, 这里将所有文件会带个+号， 对于不需要提交的文件，可以通过右键->Team->Remove from Index 移除。

5. 首先提交代码到本地仓库

右键项目->Team->Commit,  add commit message, 如果遇到下面这种情况，先去Window->Preference->Team->Git->Committing, 将第一个默认勾选去掉。





以下面作为参考提交，



 

注意，代码只需要提交图片中标识的文件即可。也可以通过编辑.gitignore将不需要提交的文件筛除。

例如，

使用Notepad输入需要忽略的文件或文件名，如下所示：

 

##ignore this file##
/target/

 

.classpath
.project
.settings

 

 

这时，可以看到文件带有圆柱形标志，

 



6. 从本地代码提交到Git

项目右键，Team->Remote->Push, 输入Git地址，以及登陆凭证



 

点击Next，Source ref和Destination ref下拉框中选择master，点击Add Spec



点击Next。

7. 项目提交到Git成功



8. 打开Git， 查看是否项目是否上传成功。


