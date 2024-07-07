---
title: git建立SSH信任
tags:
  - git
categories:
  - git
  - SSH信任
cover: >-
  https://img1.baidu.com/it/u=3306102985,2313411151&fm=253&fmt=auto&app=138&f=PNG?w=2291&h=500
poster:
  topic: 用于代码仓库的托管与操作系统沟通的中间商
  headline: 利用git建立SSH信任
  caption: null
  color: black
abbrlink: b5cf5e6d
date: 2020-03-23 18:46:42
banner:
h1:
---
{% checkbox symbol:plus 在 macOS、Linux 或 Windows 上通过 SSH 连接到 Git 存储库，以使用 HTTPS 身份验证安全连接。 在 Windows 上，我们建议使用 Git 凭据管理器 或 个人访问令牌。 %}

{% u SSH URL 已更改，但旧的 SSH URL 将继续生效 。 如果已设置 SSH，则应将远程 URL 更新为新格式： %}


{% tabs active:1 align:center %}
<!-- tab 方法 -->
* 在本地生成公钥和密钥： <code>ssh-keygen -t rsa</code>
* 将本地生成的公钥发送到服务器上（建立信任关系）：<br>
* 测试ssh远程登陆是否成功：<code>ssh root@server_ip</code>
<!-- tab 代码 -->
```bash
ssh-keygen -t rsa
#注意这里UserName、root、server_ip 一定要看好
ssh-copy-id -i C:/Users/UserName/.ssh/id_rsa.pub root@server_ip
```
{% endtabs %}

{% tabs active:1 align:center %}
<!-- tab 建立密钥后error报错 -->
在建立密钥过程中如果出现的错误error: `sign_and_send_pubkey: signing failed: agent refused operation`
<!-- tab 解决方案 -->
```bash
ssh-agent -s
ssh-add
```
{% endtabs %}