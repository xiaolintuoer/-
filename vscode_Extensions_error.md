### 关于扩展(Extensions)的"提取扩展时出错.XHR failed"的解决方案

在自己的HP笔记本上新装了vscode后，出现了扩展连不上网打不开的情况。

#### 1. 先查明问题的原因

首先电脑联网正常，然后开了代理和不开结果都一样，应该不是电脑网络的问题。

#### 2. 解决过程

先ping一下vscode扩展的网址，看能不能ping通，打开cmd输入以下

```bash
ping marketplace.visualstudio.com
```

结果如下，总之是能ping通的

![ping](/image/extension_1.png)

这里也查询出了ip地址`13.107.42.18`，不放心的可以在站长工具(https://ip.tool.chinaz.com/)查询下真实地址。

然后就可以修改`hosts`文件。hosts是一个系统文件，用于将一些常用的网址域名与对应的IP地址关联。当用户需要登录网址时，系统首先`hosts`文件中寻找对应的IP。如果找到对应的IP地址，系统直接连接对应网址；如果没有找到，则将网址提交给DNS解析。

window系统中到目录`C:\Windows\System32\drivers\etc\`下找到`hosts`文件`，先修改文件的权限，右键“属性”点击“安全”，一般来说当前使用的是"User"账号，则把"User"的权限修改即可。

![hosts](/image/extension_2.png)

然后用记事本打开hosts，添加如下一行记录，并保存

![hosts2](/image/extension_3.png)

到这里已经处理好问题，重进一下vscode就可以发现能正常使用扩展了。