##### 一、在任意位置执行 `ssh-keygen`

​	更改文件名，输入密码可以直接为空

​	在C盘用户名的目录下多处一个`.ssh`的文件夹，里面就是生成的公钥和私钥

##### 二、打开代码托管平台，设置->部署公钥，把生成的公钥`id_rsa.pub`这个文件里的内容赋值上去

##### 三、配置本地config  （这不是一个dot file  可以通过 touch config 来新建）

```javascript
Host git.dev.tencent.com
IdentityFile C:\Users\18081\.ssh\\id_rsa_coding
PreferredAuthentications publickey
User XDLRanger
```

​	host  user得自己做一个修改，如果要配置多个平台，从第一步开始重新执行一次，然后再config里新增一条配置



Mac查看上查看 git 安装的位置

```bash
$ which git
```



Mac 上查看软件安装位置, 在terminal.app中使用which指令，格式为

```bash
$ which softwareName
```

### git bash 常用指令
pwd  打印当前完整路径
/   根目录
~  家目录
clear 清楚控制台
ls  列出当前路径下所有文件（夹）
ls -a  列出当前路径下所有文件（夹），包括隐藏文件（夹）
ls -al  列出当前路径下所有文件的（夹）详细信息（包括隐藏文件）
cd  切换目录
cd ../  进入上一级目录
cd test/  进入test目录
mkdir test  新建test目录
touch a.html  新建a.html文件
mv a.html b.html  a.html文件重命名为b.html
rm a.html  删除a.html文件
rm -r test  删除test目录
rm -rf test  删除test目录（强制删除）
vim a.html  用vim编辑a.html文件（如果没有a.html文件则自动创建）
i  切换vim到编辑模式（windows下貌似很多按键都可以）
:w  保存vim编辑器的内容
:q  退出vim编辑器
:wq  保存并退出
:q!  强制退出（不提示未保存等）
gg  定位到文件开头
G   定位到文件尾
y  复制
yy  复制整行（nyy或yny  复制n行，n为数字）
d  剪切
dd  剪切整行（ndd或dnd  剪切n行，n为数字
p  粘贴到光标后（复制整行则在光标下一行）
P  粘贴到光标前（复制整行则在光标上一行）
ctrl+f  下翻整页（ctrl+d 下翻半页）
ctrl+b  上翻整页（ctrl+u 上翻半页）
/string  查找string
u  撤销

