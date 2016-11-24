Debug Vstack
===

### 下载代码
vStack: https://github.com/oncecloud/vStack.git
vStack: https://github.com/oncecloud/vStack-utility.git
vStack-dashboard: https://github.com/oncecloud/vStack-dashboard.git

> 将三份代码放到同一个目录下，本文档放于/home/xx/iscas

### 编译安装
1.下载tomcat
wget -c http://archive.apache.org/dist/tomcat/tomcat-7/v7.0.35/bin/apache-tomcat-7.0.35.zip

放入与三份代码相同的目录下（/home/xx/iscas）

2.编译代码
~~~
$ cd /home/xx/iscas
$ cd zstack-utility/zstackbuild
$ ant -Dzstack_build_root=/home/xx/iscas all-in-one
~~~

3.安装

~~~
$ cd /home/xx/iscas/zstack-utility/zstackbuild/target
$ sudo bash zstack-installer*.bin -a －D -R aliyun (公网环境)
$ sudo bash zstack-installer*.bin -o －D  (西大环境)
~~~

> 选项说明 -D :初始化数据库。 －a/-o 全部安装， －R 制定安装源


### 远程环境准备
* 关闭vStack
~~~
$ zstack-ctl stop
~~~
* 打开JPDA
~~~
$ cd /usr/local/zstack/apache-tomcat -7*/bin
$ ./catalina.sh jpda run
~~~
当最终出现start ** in xxms时，启动成功
* 运行Web UI
~~~
$ zstack-ctl start_ui
~~~


### 导入代码
* 将三分代码中的vStack以maven文件的形式导入eclipse中
* 在需要的地方打上断点
* 调试
eclipse->debug->debug configuration-> Remote java application
* 选中有断点的子项目，输入IP，端口默认8000，确定

### Debug

操作Web UI，触发断点
enjoy!







