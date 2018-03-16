---
layout: post
title: Subversion 使用经验
date: 2017-10-21 16:12:24.000000000 +08:00
tag: svn
---

将远程SVN版本库搬到本地  
--------------------------------------

此时如果可以将远程版本库整个同步到本地，然后所有操作都在本地的版本库上进行，好处就不用多说了。幸运的是SVN已经提供了相应的功能，具体操作步骤如下：
1）在本地建立一个新的版本库：
    svnadmin create D:\test
2）创建钩子文件pre-revprop-change：
windows环境里是D:\test\hooks\pre-revprop-change.bat,   文件中只需要一行内容即可
    exit 0
Linux 下是test/pre-revprop-change， 文件内容如下，
    #!/bin/sh
    exit 0
加上执行权限
    chmod +x test/pre-revprop-change
3）初始化同步操作：
    svnsync init file:///D:/test svn://10.250.32.10:88/client
svn://10.250.32.10:88/client 是远程SVN库的URL。如果需要用户名/密码，则按提示输入。成功后命令行将输出信息：复制版本 0 的属性
4）执行同步操作：
    svnsync sync file:///D:/test
   （如果需要用户名/密码，则按提示输入。如果远程SVN库数据较多，需要慢慢等待）
5）如果远程SVN库有了新的更新，只需重复执行步骤4即可。





git svn clone svn://10.250.32.10:88/client/Android_Palmplay/branch/PalmplayGradleProj --no-metadata --no-minimize-url --authors-file=authors PalmplayNew



authors: 

xushenlong=xushenlong <xushenlong@transsnet.com>
shikun=shikun <shikun@afmobilegroup.com>
hexiangyang=hexiangyang <hexiangyang@afmobilegroup.com>
hejianguo=hejianguo <hejianguo@afmobilegroup.com>



