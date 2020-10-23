#  VM

[Wikipedia](https://fr.wikipedia.org/wiki/Virtualisation)

## VirtualBox 

[VirtualBox](https://www.virtualbox.org/wiki/VirtualBox) is a general-purpose full virtualizer for x86 hardware, targeted at server, desktop and embedded use. 

### Installation

Binaries, extension and source code can be installed from the [wiki](https://www.virtualbox.org/wiki/Downloads).


A handy feature is the ability to run common commands for managing VM from the cli after installing the [extension pack](https://www.virtualbox.org/wiki/Downloads)

### Basic command for running VM

The extension pack cli entry point `VBoxManage` can be aliased as:
```bash
alias vbm=VBoxManage
```

List VM's:
```bash
vbm list vms
# List running vms
vbm list runningvms
```

Change the name of a VM:
```bash
vbm modifyvm "VirtualMachine provided for test purpose" --name "MyVM"
```

Start a VM in headless mode:
```bash
vbm startvm "MyVM" --type headless
```

Once started, a VM in headless mode can be controlled (pause/resume/poweroff):
```bash
vbm controlvm "MyVM" pause --type headless
vbm controlvm "MyVM" resume --type headless
vbm controlvm "MyVM" poweroff --type headless
```

View VM properties with `vboxmanage guestproperty` <badge-doc href='https://docs.oracle.com/en/virtualization/virtualbox/6.1/user/vboxmanage.html#vboxmanage-guestproperty' logo='VirtualBox'></badge-doc> 
```bash
# Enumerate all properties of the VM named MyVM
vbm guestproperty enumerate MyVM

# Get the IP address of the VM named Cloudera
vbm guestproperty get Cloudera /VirtualBox/GuestInfo/Net/0/V4/IP
```


## Vagrant 

### Installation on Debian based systems

deb package can be found at [download](https://www.vagrantup.com/downloads.html)

```
curl -LO https://releases.hashicorp.com/vagrant/2.2.9/vagrant_2.2.9_x86_64.deb
sudo apt install ./vagrant_2.2.9_x86_64.deb
# or dpkg -i 
```

[Customizing Vagrant VMware Fusion Virtual Machines with VMX Parameters](https://thornelabs.net/posts/customizing-vagrant-vmware-fusion-virtual-machines-with-vmx-parameters.html)

[How to create a Vagrant Box running Red Hat Enterprise Linux](https://medium.com/@severi/how-to-create-a-vagrant-box-running-red-hat-enterprise-linux-55410f8cfa7d)

### Troubleshooting on hosts with secure mode enabled  

UEFI[^1] Secure Boot[^2] (SB) is a verification mechanism for ensuring that
code launched by a computer's UEFI firmware is trusted. Unsigned drivers are
therefor not allowed to load.

2 kernels modules are compiled at installation time and must be loaded. If the
host provides the proper kernel headers and gcc, these two modules will be
built silently. The progress is logged into /tmp/vmware-root/vmware-PID.log[^3].

On error type like:

> Cannot open `/dev/vmmon`: No such file or directory. Please make sure that the kernel module `vmmon` is loaded

The modules must be signed and the keys added to a database recognised by the first stage of the bootloader, the **Machine Owner Key**


```console
# Modules must be signed by a CA (Certificate Authority), here self-signed  
openssl req -new -x509 -newkey rsa:2048 -keyout <MOK.priv> -outform DER -out <MOK.der> -nodes -days 36500 -subj "/CN=VMware/"
sudo /usr/src/linux-headers-``uname -r``/scripts/sign-file sha256 <MOK.priv> <MOK.der> $(modinfo -n vmmon)
sudo /usr/src/linux-headers-``uname -r``/scripts/sign-file sha256 <MOK.priv> <MOK.der> $(modinfo -n vmnet)

sudo mokutil --test-key <MOK.der>    
# cert should not be currently enrolled

sudo mokutil --import <MOK.der>
# mokutil should request pwd 

sudo mokutil --test-key <MOK.der>    
# cert should be enrolled now 

sudo mokutil --list-new    
# your cert should be displayed

reboot
```

## Links

[^1] Unified Extensible Firmware Interface - https://wiki.debian.org/UEFI  
[^2] [Debian secure boot documentation page](https://wiki.debian.org/SecureBoot)  
[^3] [VMware knowledge base](https://kb.vmware.com/s/article/2146460)
