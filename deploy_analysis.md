部署运行机制分析
===

> 此文档处于持续更新中，结论均为探索中的结论，请以辩证角度阅读此文档

## 安装后环境说明

ZStack安装后，主要会使用两个路径，分别对这两个路径进行说明

### /usr/local/zstack 

 此路径是ZStack的主要安装路径(All-In-One安装路径)，为ManagementNode安装保存路径，即此路径会安装在ManagementNode上。此路径包含ZStack的Tomcat服务、Ansible服务、安装源码包、垃圾收集等等。

ManagementNode会不断轮询Agent，来收集Agent信息。当发现有服务down后，会自动重新部署安装Agent节点，替换代码。


【根据现在的分析，Agent端只负责接受消息请求，不主动发自身状态给ManagementNode，而是由ManagementNode主动轮询。这种方式在Agent很多的情况下，势必会造成网络内部的大量通信，不知道会不会影响性能。ZStack文档中所说的负载均衡应该不是运用在系统内部的，是负责用户请求的负载均衡。因此如何处理系统内部的消息通信，还需要进一步探究】


*目录文件分析*

| Name | Description|
| --------   | -----  |
|ansible|包含所有ZStack部署所需要的源代码、ansible部署文件。应该是ansible的source code目录|
|apache-tomcat-7.0.35/webapps/zstack|ZStack core的Web Server,接受处理请求，提供可靠保障机制所需的备份原始文件|


> Notice: 在ZStack中，自动维护部署任务应该是由Ansible负责。虽然在代码中有自动运维工具SaltStack和Puppet的影子，但是在验证安装中并没有发现安装了salt和puppet。因此认为在ZStack商业版中可能会用到这两个工具，社区版则只使用Ansible

### /var/lib/zstack

  此路径是zstack的Agent运行时环境，即此路径会安装在host节点。在virtualenv中包含console代理、virtualenv、KVM Agent等等。

KVM Agent使用cherrypy来提供http服务。即在Agent端提供Http server功能，接收来自ManagementNode的请求，如该agent的状态收集请求、控制请求等。


*/var/lib/zstack/virtualenv目录文件分析*

| Name | Description|
| --------   | -----  |
|consoleproxy|守护进程，负责VNC连接|
|kvm|客户端python代码。当此处代码发生修改，或在服务关闭，此处代码会被ManagementNode替换成备份代码，重启服务|
|sftpbackupstorage||
|zstackcli|zstackcli运行时代码|
|zstackctl|zstackctl运行时代码|
|zstack-dashboard|dashboard的运行部署|


## ZStack Agent

Agent由zstacklib.utils.http提供http服务

### ZStack Agent启动流程

1. 载入plugins并安装

 zstacklib.utils.plugin:Loading plugins from folder[/var/lib/zstack/virtualenv/kvm/lib/python2.7/site-packages/kvmagent/plugins
 Adding plugin[HostPlugin] to PluginRegistry

2. 为虚拟机启动进行准备
 [zstacklib.utils.http] function[reboot_vm] registered uri 注册过后的服务会以此执行，进行qume检查、重建ISO，初始化环境、启动虚拟机等等操作

3. 查看当前服务状态
  INFO:cherrypy.error:[30/Aug/2016:10:16:47] ENGINE Listening for SIGHUP. 会进行服务进程状态检测

4. 虚拟机启动请求




