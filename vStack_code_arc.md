代码结构
===

## zstack

| Name       | Description   |
| --------   | -----  |
|build|vStack的JAVA部分的MAVEN编译、打包、部署|
|compute|有关计算资源的操作，各类工作流。有放置、集群、主机、虚拟机、区域的相关操作。如虚拟机模块：提供具体的虚拟机在创建、管理过程中，需要做哪些步骤，垃圾如何回收等|
|conf|1.JAVA Bean的配置文件，2.数据库:数据库建立的SQL脚本、数据库安装搭建。3.持久化配置文件。4.spring的bean、servlet配置文件.5.service的配置文件……|
|configuration|模板管理。创建管理虚拟机模板、云盘模板、虚拟路由模板。同时可以配置全局属性|
|？console|疑似控制模块，用于控制消息的管理console angent|
|**core|核心模块。实现系统的核心功能。包括部署、数据库、消息总线、工作流实现等等方面。其他模块的实际操作都是调用此模块的代码|
|header|主要包含各类消息的具体封装类，java bean|
|identity|账户管理。用户的登入登出操作、sessionToken的获取等等|
|image|镜像的管理。处理镜像的消息，如镜像的添加、查询等等|
|network|网络管理，包含二层网络、三层网络的创建、管理等操作|
|plugin|插件模块。包含kvm/Xen agent，负载均衡、安全管理、虚拟路由等等，比较庞大|
|portal|消息总分发入口，包括ManageMent Node的管理、根据消息分发。在接受到消息体后，对消息中的信息进行验证，调用对应消息所需的消息预处理|
|search|查询操作处理模块。与数据库相关的操作|
|simulator|模拟器，应该是在做测试是模拟操作。此模块比较独立，其他模块没有调用这个模块的代码|
|storage|存储相关代码。包括管理主存、备份存储、快照、volume等的管理|
|tag|Tag系统，负责Tag的生成和管理|
|test|测试模块|
|tool|Doc生成类|
|utils|辅助工具类。包括json转化，ssh管理，序列化，iptable防火墙等等|





## zstack-utility


| Name       | Description   |
| --------   | -----  |
| agentcli |也是一个提供CLI服务的模块。根据描述，应该是用于agent测试用的，只识别写在文件中的命令，应该是用于执行测试命令脚本|
|apibinding|为zstackcli服务，对cli命令相关API转换提供服务，生成请求格式，往Tomcat发出REST请求|  
|appliancevm|开启HttpServer，监听7759端口。主要负责防火墙的规则设置|
|buildsystem|zstack系统的安装代码，负责系统的安装流程，安装后的服务启动| 
|cephbackupstorage||
|cephprimarystorage|| 
|consoleproxy|开启HttpServer，监听7758端口。守护进程，包含VNC连接。在ZStack运行的过程中会一直开启consoleproxy守护进程|
|fusionstorbackupstorage||
|fusionstorprimarystorage||
|imagestorebackupstorage||
|installation||
|iscsifilesystemagent||
|kvmagent|虚拟机的安装。在这个文件夹下面包含很多plugin，在虚拟机创建的时候会依次载入这些plugin。plugin包含。。。|
|puppets||
|setting||
|sftpbackupstorage||
|virtualrouter||
|zstackbuild|ZStack build目录。进入此目录后进行All-in-One包编译|
|zstackcli|zstackcli命令管理工具|
|zstackctl|zstackctl命令管理工具|
|zstacklib|提供运行中所需要的一些工具。守护进程、Http服务等|



## zstack-dashboard
| Name       | Description   |
| --------   | -----  |
|zstack_dashboard|web所有的文件|
|zstacl_dashboard/static|静态资源，包含页面的html文件以及js、image等文件|
|zstack_dashboard/web.py|后台文件，对消息的收发|
|zstack_dashboard.sh|部署脚本|


> Updating.........

