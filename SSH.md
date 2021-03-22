http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html


SSH主要用于远程登录。假定你要以用户名user，登录远程主机host，只要一条简单命令就可以了。

　　$ ssh user@host

如果本地用户名与远程用户名一致，登录时可以省略用户名。

　　$ ssh host

SSH的默认端口是22，也就是说，你的登录请求会送进远程主机的22端口。使用p参数，可以修改这个端口。

　　$ ssh -p 2222 user@host

上面这条命令表示，ssh直接连接远程主机的2222端口。



当远程主机的公钥被接受以后，它就会被保存在文件$HOME/.ssh/known_hosts之中。下次再连接这台主机，系统就会认出它的公钥已经保存在本地了，从而跳过警告部分，直接提示输入密码。

每个SSH用户都有自己的known_hosts文件，此外系统也有一个这样的文件，通常是/etc/ssh/ssh_known_hosts，保存一些对所有用户都可信赖的远程主机的公钥。



### 公钥登录

就是用户将自己的公钥储存在远程主机上。登录的时候，远程主机会向用户发送一段随机字符串，用户用自己的私钥加密后，再发回来。远程主机用事先储存的公钥进行解密，如果成功，就证明用户是可信的，直接允许登录shell，不再要求密码。

这种方法要求用户必须提供自己的公钥。如果没有现成的，可以直接用ssh-keygen生成一个：

　　$ ssh-keygen


重启远程主机的ssh服务。

　　// ubuntu系统
　　service ssh restart

　　// debian系统
　　/etc/init.d/ssh restart





































