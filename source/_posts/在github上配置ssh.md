---
title: 在github上配置ssh
cover: /images/pkqiu.webp
date: 2024-12-1
tags: 
    - configuration
    - github
    - git
categories: ["Problems"]
---

# 生成密钥
打开Git Bash，输入以下命令：
`$ ssh-keygen -t rsa -C "这里写你注册github时的邮箱"`
会弹出来一段话
`$ Enter file in which to save the key (/c/Users/86132/.ssh/id_rsa):`
按enter键，选择n
然后再输入以下命令查看公钥：
`$ cat ~/.ssh/id_rsa.pub`
复制得到的公钥

# 将密钥添加要github上
打开github，点击右上角头像，点击设置
点击ssh and gpg keys，点击new ssh key
标题随便取(自己知道什么意思就行)
将复制的公钥粘贴到key字段里
点击add ssh key
测试一下连通性，连接失败，嘻嘻

# 关键一步，配置config
回到Git Bash，输入以下命令，在vim编辑器中编辑config文件：
`$ vim ~/.ssh/config`
粘贴以下内容，记得改邮箱：
> Host github.com  
> User 这里写你注册github时的邮箱  
> Hostname ssh.github.com  
> PreferredAuthentications publickey  
> IdentityFile ~/.ssh/id_rsa  
> Port 443

然后按Esc键退出insert模式，（按i键就又回到插入模式），退出插入模式后输入以下命令
`:wq`
再按Enter，即可回到原来的界面
然后就可以来测试联通性啦，输入以下命令
`$ ssh -T git@github.com `
大功告成！

