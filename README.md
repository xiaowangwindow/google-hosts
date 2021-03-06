google-hosts
============

### 为什么有这个项目

因为我每天都要访问Google, 以及我的朋友们也会访问Google.<br/>
然而朋友们对其他更复杂的代理未做深入研究, 最简单方法便是帮他们修改 hosts.<br/>
于人于己方便, 便弄了这个项目. 包含了大部分Google服务, G+, Drive, Gmail, Hangouts, Calendar等<br/>
域名参考了[smarthosts][smarthosts], [ipv6-hosts][ipv6-hosts].<br/>

IP不总是可用的, 因素可能是GFW封锁或Google IP变动. <br/>
同一个IP, A省能连上, B省就可能连不上(网络封锁). 上一个小时能连上, 这一个小时连不上(间歇性阻断)<br/>
另外Google的好多服务都已经不挂在北京的IP上了<br/>
**你可以用此脚本去寻找最适合你的稳定IP.**

### 脚本如何使用

`find.sh`查询某段IP详细信息,可接受一个或多个参数(这个可检测IP是否被封锁, 443端口是否被封锁)

```
$ cd google-hosts/scripts

# 查询 192.168.1.x
$ ./find.sh 192.168.1

# 查询 192.168.x.x
$ ./find.sh 192.168

# 查询 192.168.x.x, 192.169.x.x, 192.170.1.x
$ ./find.sh 192.168 192.169 192.170.1
```

`filter.sh`从output目录(由find.sh生成)过滤域名

```
$ cd google-hosts/scripts

# 过滤可用于*.google.com的域名
$ ./filter.sh *.google.com

# 过滤可用于mail.google.com的域名
$ ./filter.sh mail.google.com
```

`use.sh`使用过滤出的某个IP并更新hosts.all文件

```
$ cd google-hosts/scripts

# 使用可用于*.google.com 的IP 192.168.1.1
$ ./use.sh *.google.com 192.168.1.1

# 使用可用于mail.google.com 的IP 192.168.1.1
$ ./use.sh mail.google.com 192.168.1.1
```

`select.sh`结合了filter.sh, use.sh,自动选择最佳IP写入hosts.all文件, 并做了些特殊域名处理

```
$ cd google-hosts/scripts
$ ./select.sh
```

`apply.sh`使用hosts.all文件更新../hosts文件

```
$ cd google-hosts/scripts
$ ./apply.sh
```

`auto.sh`结合了find.sh, select.sh, apply.sh自动查询后选择最佳IP写入../hosts文件

```
$ cd google-hosts/scripts

# 查询192.168.x.x,192.169.1.x, 并在查询完后自动选择最佳IP更新../hosts文件
$ ./auto.sh 192.168 192.169.1
```

输出的四个字段含义

| IP | LOSS | TIME | SSL |
| --- | --- | --- | --- |
| 此IP | 丢包率| PING值 | 可用ssl域名 |

另外获取Google IP段可供参考

```
$ nslookup -q=TXT _netblocks.google.com 8.8.4.4
```

### 最新hosts

\>\> [hosts][hosts] \<\< `UPDATE: Tue Jun 24 10:14:07 UTC 2014` <br/>
**注意**: 如果此hosts文件内的IP失效, 就需要你自己用上面提到的脚本查询了<br/>
下面的两个程序是用来将项目内hosts文件更新你系统hosts. 尤其对不懂程序的Windows朋友很方便<br/>

#### Windows 用户

* 下载[fuckGFW-64.exe][fuckGFW-64.exe](64位)或[fuckGFW-32.exe][fuckGFW-32.exe](32位)
* 双击运行一下即可. 更新也是双击运行一下
* 此程序不会覆盖你原有的 hosts

#### \*nix/OSX 用户

* 下载此脚本 [updateHosts.py][updateHosts.py]
* 执行 `$ sudo python /PATH/TO/updateHosts.py`, 更新也一样
* 此程序不会覆盖你原有的 hosts

[hosts]: http://tx.txthinking.com/hosts
[fuckGFW-64.exe]: http://tx.txthinking.com/fuckGFW-64.exe
[fuckGFW-32.exe]: http://tx.txthinking.com/fuckGFW-32.exe
[smarthosts]: https://code.google.com/p/smarthosts/
[ipv6-hosts]: https://code.google.com/p/ipv6-hosts/
[updateHosts.py]: https://github.com/txthinking/google-hosts/tree/master/scripts/updateHosts.py


