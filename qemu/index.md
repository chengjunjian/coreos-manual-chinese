---
layout: docs
slug: qemu
����: �ĵ�
---

# ��[QEMU][qemu-link]������CoreOS

[CoreOS](http://coreos.com) �����ھ޴�Ŀ����У����ұ������Ĳ���.

��Щ˵����ָ������QEMU������һ������CoreOSʵ��,
[QEMU](http://www.qemu.org)����С��ʿ�����������������CPU��������
�������Ҫ���ĸ��࣬�ɲο�[��������][qemunet]��[QEMU �ĵ�][qemuwiki] �� [�û��ֲ�][qemudoc].

�����ֱ�ӵ� [IRC ͨ��][irc] ���� [�ʼ��б�][coreos-dev]��ѯ.

[qemunet]: http://wiki.qemu.org/Documentation/Networking
[qemuwiki]: http://wiki.qemu.org/Manual
[qemudoc]: http://qemu.weilnetz.de/qemu-doc.html
[irc]:irc://irc.freenode.org:6667/#coreos
[coreos-dev]:https://groups.google.com/forum/#!forum/coreos-dev


## ��װ [QEMU][qemu-link]

QEMU��������������Linuxϵͳ������������Windows��OSX,�������������Linux��
���ҿ��������κ�Linux���а档

### [Debian][debian-link] ���� [Ubuntu][ubuntu-link]

[Debian�ĵ�][qemudeb] �и����ϸ�� ������ʼ�Ļ���ֻ��Ҫ��

    sudo apt-get install qemu-system-x86 qemu-utils

[qemudeb]: https://wiki.debian.org/QEMU

### Fedora ���� Red Hat

Fedora��ά������һ�� [����ָ��][qemufed] ���ǻ�����װ�ǳ��ļ�:

    sudo yum install qemu-system-x86 qemu-img

[qemufed]: https://fedoraproject.org/wiki/How_to_use_qemu

### Arch

�����㿪ʼ����Ҫ����:

    sudo pacman -S qemu

[Arch's QEMU ά��ҳ��][arch-qemu-wiki-link],���ܹ����ָ���ϸ��.
[arch-qemu-wiki-link]:https://wiki.archlinux.org/index.php/Qemu

### Gentoo

����������Ԥ�ڵ�������Gentoo���ܻḴ��Щ��
�����е�������ں�ѡ���USE��ʶ�������� [Gentoo
ά��][qemugen]. һ����˵���������㹻��:

    echo app-emulation/qemu qemu_softmmu_targets_x86_64 virtfs xattr >> /etc/portage/package.use
    emerge -av app-emulation/qemu

[qemugen]: http://wiki.gentoo.org/wiki/QEMU


## ����[CoreOS][coreos-link]

[QEMU][qemu-link]��װ��ɺ���������ز����������µ�CoreOS����.
��������Ҫ�����ļ�:  

1. ���̾�����qcow2�ĸ�ʽ�ṩ��  

2. ����[QEMU][qemu-link]��shell�ű� 

    mkdir coreos; cd coreos     
    wget http://storage.core-os.net/coreos/amd64-generic/dev-channel/coreos_production_qemu.sh  
    wget http://storage.core-os.net/coreos/amd64-generic/dev-channel/coreos_production_qemu_image.img.bz2  
    chmod +x coreos_production_qemu.sh 
    bunzip2 coreos_production_qemu_image.img.bz2
	
�����ܼ�:    
  
    ./coreos_production_qemu.sh -nographic

### SSH Keys

In order to log in to the virtual machine you will need to use ssh keys.
If you don't already have a ssh key pair you can generate one simply by
running the command `ssh-keygen`. The wrapper script will automatically
look for public keys in ssh-agent if available and at the default
locations `~/.ssh/id_dsa.pub` or `~/.ssh/id_rsa.pub`. If you need to
provide an alternate location use the -a option:

    ./coreos_production_qemu.sh -a ~/.ssh/authoized_keys -- -nographic

Note: Options such as -a for the wrapper script must be specified before
any options for QEMU. To make the separation between the two explicit
you can use -- but that isn't required. See
`./coreos_production_qemu.sh -h` for details.

Once the virtual machine has started you can log in via SSH:

    ssh -l core -p 2222 localhost

### SSH Config

To simplify this and avoid potential host key errors in the future add
the following to `~/.ssh/config`:

    Host coreos
    HostName localhost
    Port 2222
    User core
    StrictHostKeyChecking no
    UserKnownHostsFile /dev/null

Now you can log in to the virtual machine with:

    ssh coreos


## Using CoreOS

Now that you have a machine booted it is time to play around. Check out
the [Using CoreOS][using-coreos] guide.
[debian-link]:http://www.debian.org
[ubuntu-link]:http://www.ubuntu.com
[qemu-link]:http://www.qemu.org
[coreos-link]:http://coreos.com