---
layout: post
title: �й�git����
category: ��������
tags: [git]
---

�Լ���С�ڱ�������...��ʼ��ʵ���ҵĵ��Ըɻ������Ҫ�ύ����һ������Ĵ��룬�����git�����ù��̼�¼�����������Ժ�鿴��

1. Install the git client downloaded from [here](http://git-scm.com/download/) ;
2. Right click the "Git Bash" from startup menu, click property, flag the "quick edit";
3. echo `ssh-keygen -t rsa -C "email"`;
4. copy the content of id_rsa.pub to ssh settings;
5. echo `ssh -T git@github.com` to verify the id;
6. echo `git config --global user.name "username"` and `git config --global user.email "email"`;

���ˣ�git���þ�over�ˡ���`git add .`, `git commit -a -m 'xxxxx'`, `git push -u origin master`����������ɲ�Ӧ������~��