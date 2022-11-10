## ssh config 

1. config 为了方便我们批量管理多个 ssh
2. config 存放在 ~/.ssh/config
3. config 配置语法

## ssh config 语法关键字

1. Host 别名
2. HostName 主机名（重要）
3. Port 端口（重要）
4. User 用户名
5. IdentityFile 秘钥文件的路径

eg：配置多台服务器时只需要重复配置如下的配置项

```
host "mogo"
	HostName 192.168.60.77
	User mogo
	Port 22
	IdentityFile ~/.ssh/id_rsa  # 这里是私钥的配置
	IdentitiesOnly yes
```

**使用**

当只配置如下配置项时：

```
host "ubuntu"
    HostName 10.211.55.3
    User blueberry
    Port 22
```

连接这台服务器时使用命令  `ssh ubuntu`  后输入密码即可连接。而以往的连接方式是 `ssh username@ip_addr` 后输入密码才可连接。



## ssh 免密登录

**ssh key**

1. ssh key 使用非对称加密方式生成公钥 和 私钥
2. 私钥存放在本地 `~/.ssh` 目录
3. 公钥可以对外公开，放在服务器的 `~/.ssh/authorized_keys`
4. 私钥放在本地，可通过 config 配置私钥的存放路径 `IdentityFile ~/.ssh/id_rsa`

**生成秘钥**

其中 `dsa` 和 `rsa` 是两种不同的加密算法，可以选其一

`ssh-keygen -t rsa`

`ssh-keygen -t dsa`









