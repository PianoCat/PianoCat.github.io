---
layout: post
title: 有关git配置
category: 其他技术
tags: [git]
---

自己的小黑本本挂了...开始用实验室的电脑干活。想起来要提交备份一下最近的代码，这里把git的配置过程记录下来，方便以后查看。

1. Install the git client downloaded from [here](http://git-scm.com/download/) ;
2. Right click the "Git Bash" from startup menu, click property, flag the "quick edit";
3. echo `ssh-keygen -t rsa -C "email"`;
4. copy the content of id_rsa.pub to ssh settings;
5. echo `ssh -T git@github.com` to verify the id;
6. echo `git config --global user.name "username"` and `git config --global user.email "email"`;

到此，git配置就over了。像`git add .`, `git commit -a -m 'xxxxx'`, `git push -u origin master`这样的命令可不应该忘掉~。