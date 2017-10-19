---
layout: post
title: 我的win系统vagrant配置文件
---

我的win系统vagrant配置文件

### 我的win系统vagrant配置文件

```
Vagrant.configure(2) do |config|
  config.vm.box = "thdengops/ubuntu-14.04-dev"
  config.ssh.username = "vagrant"
  config.ssh.password = "vagrant"
  config.ssh.insert_key = false
  config.vm.network "private_network", ip: "172.28.128.7"
  config.vm.synced_folder ".", "/vagrant", type: "nfs", disabled: true
  config.vm.synced_folder "C:\\Users\\xzfz\\sun", "/sun", type: "nfs", mount_options: ["nolock", "vers=3", "udp", "noatime", "actimeo=1"]

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--nictype1", "virtio"]
    vb.gui = false
    vb.memory = "4096"
    vb.cpus = 2
  end
end
```
