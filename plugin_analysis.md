plugin分析
===

### vm_plugin

#### 新建虚拟机
虚拟机的创建是通过调用vm_plugin.py -> VmPlugin -> start_vm()方法来实现的，最终通过vm_plugin.py -> Vm -> from_StartVmCmd()静态方法来构造虚拟机的XML对象，再通过调用libvirt的defineXML()来构造虚拟机。

#### 查询虚拟机
查询虚拟机是通过vm_plugin.py -> VmPlugin -> get_vm_by_uuid() or get_running_vm_uuids()方法来查询的，最终通过vm_plugin.py -> Vm -> from_virt_domain()静态方法转化成虚拟机的XML对象。

#### 适配Xen虚拟机
1、修改XML类型为Xen
    from_virt_domain() -> make_root() -> root.set('type', 'xen')
2、修改使用的QEMU路径
    from_virt_domain() -> make_devices() -> get_qemu_path()

#### 测试用例
测试用例可参考test\test_vm_plugin_start_vm.py，基本用法符合unittest，只是没有assert。

