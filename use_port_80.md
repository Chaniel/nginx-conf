# Linux下普通用户如何使用80端口启动程序(转载)
大家都知道默认情况下Linux的1024以下端口是只有root用户才有权限占用，于是我们的tomcat，apache，nginx等等程序如果想要用普通用户来占用80端口的话就会抛出permission denied的异常。

解决办法有两种：

1. 使用非80端口启动程序，然后再用iptables做一个端口转发。
2. 假设我们需要启动的程序是nginx，那么这么做也可以达到目的。

一开始我们查看nginx的权限描述：
```bash
-rwxr-xr-x 1 nginx dev 2408122 Sep  5 16:01 nginx
```
这个时候必然是无法正常启动的。

1. 首先修改文件所属用户为root  
`chown root nginx`  
这一步是必须的。否则即使u+s，也不管用。

2. 然后再加上s权限  
`chmod u+s nginx`  
说明：添加S位的目的是让程序以root权限起，即使你用的不是root帐号。它也会以root帐号名义起。这时候就绕开端口BIND权限的问题。

3. 再次查看权限描述的时候  
`-rwsr-xr-x 1 root root 2408122 Sep  5 16:01 nginx`  
这个时候切换到普通用户下再启动就没问题了。
