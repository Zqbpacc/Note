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