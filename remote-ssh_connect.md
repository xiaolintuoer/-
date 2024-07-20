### VScode配置remote-ssh并连接远程服务器

> 教程先省略

### 远程服务器重装系统后的连接问题

**问题描述**：原来的电脑连接过远程服务器，然而当服务器重装系统后，电脑就连接不上了。具体报错信息为

```shell
> IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY! 
> Someone could be eavesdropping on you right now (man-in-the-middle attack)! 
> It is also possible that a host key has just been changed. 
> The fingerprint for the ED25519 key sent by the remote host is 
> SHA256:+EEKbk2wWZmGCr4QtictvQOuD5xC/FOrpmhyU7UYU5c. 
> Please contact your system administrator. 
> Add correct host key in C:\\Users\\EDY/.ssh/known_hosts to get rid of this message. 
> Offending ECDSA key in C:\\Users\\EDY/.ssh/known_hosts:6 
> Host key for 192.168.0.210 has changed and you have requested strict checking.
```

**原因**：服务器系统重装或重新安装SSH服务后，服务器的SSH密钥指纹发生更改，与本地`known_hosts`文件中存储的指纹不匹配。

**解决方式**：更新本地的`known_hosts`文件
* 路径为`C:\Users\EDY\.ssh\known_hosts`
* 根据报错的提示找到含`192.168.0.210`的行，删除或注释掉
* 保存`known_hosts`的更改
* 再次通过SSH连接远程服务器，此时SSH客户端会提示**接受新的密钥指纹**，选择确定，新指纹自动添加到`known_hosts`中。