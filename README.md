# lkl_study
study the LKL(linux kernel library)   https://github.com/lkl/linux

Only apply to 64Bit Linux with ipv4 network.

## Rinetd version(with LKL and raw socket backend)
### Compile

1. compile static library liblkl.a

https://github.com/linhua55/linux/tree/rinetd_bpf

refer to https://github.com/lkl/linux

Linux(LKL)'s kernel configuration file is the `.config` file in this repository, it need to be placed at the root directory of the LKL repository.

2. compile rinetd(with lkl)

https://github.com/linhua55/rinetd

refer to https://github.com/linhua55/rinetd/blob/lkl_raw/make.sh

replace `/home/vagrant/lkl/linux/tools/lkl/liblkl.a ` and `/home/vagrant/lkl/linux/tools/lkl/include` with your actual LKL path.


### Release

rinetd(lkl) with bbr powered congestion control

    wget "https://github.com/linhua55/lkl_study/releases/download/v1.2/rinetd_bbr_powered" -O /usr/bin/rinetd

rinetd(lkl) with bbr congestion control

    wget "https://github.com/linhua55/lkl_study/releases/download/v1.2/rinetd_bbr" -O /usr/bin/rinetd

rinetd(lkl) with pcc congestion control

    wget "https://github.com/linhua55/lkl_study/releases/download/v1.2/rinetd_pcc" -O /usr/bin/rinetd

For usage, refer to:

https://gist.github.com/codexss/1d5a834c479bb1532b9f82b23ee2f3fa

https://github.com/mixool/rinetd

https://www.v2ex.com/t/353778#r_4311799

### One-key script

Thanks to @phuslu for his one-key script

Usage：

      curl https://raw.githubusercontent.com/linhua55/lkl_study/master/get-rinetd.sh | bash
      
The configuration file generated by one-key script is `/etc/rinetd-bbr.conf`. By default, it only proxy(speed up) port `443`and`80`, modify the port number as needed.

### Determine if function

Use `top` command， view process `rinetd`'s  CPU usage. The faster of network speed, the bigger of CPU usage.

### Caution：

1. Dependency: iptables, grep, cut, xargs. Usual linux have these tools，But some linux use firewalld instead of iptables, it need install iptables
2. For KVM VPS, need to change `venet0:0` to the name of the network interface which have KVM's public IP, normally it is `eth0`

### Some technical details
https://linhua55.github.io/2017/04/24/LKL(Linux%20Kernel%20Library)/
jjj
