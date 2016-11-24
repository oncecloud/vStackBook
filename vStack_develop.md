二次开发
===

This documentation is a guide for install and compile zstack from source code in single node model,and show you how to debug zstack core.

## Install from source code

#### Download
~~~
$ mkdir /root/zstack-repos
$ cd zstack-repos
$ git clone https://github.com/zstackorg/zstack.git
$ git clone https://github.com/zstackorg/zstack-utility.git
$ git clone https://github.com/zstackorg/zstack-dashboard.git
$ cd zstack/
$ mvn -DskipTests clean install
~~~

#### Compile
~~~
$ cd zstack-utility/zstackbuild
$ ant -Dzstack_build_root=/root/zstack-repos all-in-one
~~~

#### Install

~~~
$ cd /root/zstack-repos/zstack-utility/zstackbuild/target
$ sudo bash zstack-installer*.bin -a -R aliyun
~~~

> Notice: If the installation can not be success, check the log, maybe you need install the rpm packages manually as fllows:
* libvirt-daemon-1.2.17-13.el7_2.5.x86_64.rpm
* libvirt-client-1.2.17-13.el7.x86_64.rpm


## Install after modify
After modify the code, you do not need recompile the code to All_In_One again, just recompile the project which you modified.

### zstack-dashboard

After modify the web UI:

~~~
$ cd zstack-dashboard/
$ python setup.py sdist
$ cp zstack-dashboard/dist/zstack_dashboard-*.tar.gz /usr/local/zstack/apache-tomcat-7.0.35/webapps/zstack/WEB-INF/classes/tools/
$ /etc/init.d/zstack-dashboard stop 
$ zstack-ctl install_ui
$ /etc/init.d/zstack-dashboard start
~~~ 

### zstack-utility
If you wanna develop a new agent,please add your xml to zstack.xml at [vStack_JAVA]/conf/springconf/zstack.xml
#### Kvm agent

After modified, just compress the source code with the same file name as :

~~~
$ /usr/local/zstack/apache-tomcat-7.0.35/webapps/zstack/WEB-INF/classes/ansible/kvm/kvmagent-1.6.tar.gz
~~~

#### Aliyun agent

Do compile first, compile process will create a tar.gz file in agent's dist/ sub-dir.

~~~
$ . /var/lib/zstack/virtualenv/aliyun/bin/activate #activate python virtualenv
$ cd [vStack-utility]/aliyunagent/dist
$ pip install --upgrade aliyunagent-1.6.tar.gz
~~~

#### Run aliyun agent in virtualenv

Run aliyun agent for test without all-in-one installation.

~~~
$ . /var/lib/zstack/virtualenv/aliyun/bin/activate #activate python virtualenv
$ cd /var/lib/zstack/virtualenv/aliyun/lib/python2.7/site-packages/aliyunagent
$ python -c "from aliyunagent import kdaemon; kdaemon.main()" start
$ cat /var/log/zstack/zstack-aliyunagent.log
~~~

### zstack



## How to debug zstack

Remote debug is needed. Just do as follow:

### Open Tomcat debug mode 

~~~
$ cd /usr/local/zstack/apache-tomcate-7*/bin
$ sudo ./catalina.sh jpda run
~~~

### Eclipse remote debug

* import the packge which you wanna debug
* insert break point in code
* Eclipse Debug configurations -> Remote Java Application -> set Name, Project, Port(8000) -> click "Debug"
* Do your operation and get the debug information 




> Updating.......





