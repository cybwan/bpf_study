[Kubernetes使用eBPF替换iptables - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/137960916)

https://blog.csdn.net/alex_yangchuansheng/article/details/124008328

[bpftools/kube-bpf: (e)BPF primitives for Kubernetes (github.com)](https://github.com/bpftools/kube-bpf)

[bpftools/linux-observability-with-bpf: Code snippets from the O'Reilly book (github.com)](https://github.com/bpftools/linux-observability-with-bpf)

[eBPF - Introduction, Tutorials & Community Resources](https://ebpf.io/zh-cn/)

[Welcome to Cilium’s documentation! — Cilium 1.11.5 documentation](https://docs.cilium.io/en/v1.11/)

[Cilium · GitHub](https://github.com/cilium)

[基于 Ubuntu 21.04 BPF 开发环境全攻略 | 深入浅出 eBPF](https://www.ebpf.top/post/ubuntu_2104_bpf_env/)

[Linux超能力BPF技术介绍及学习资料.doc-原创力文档 (book118.com)](https://max.book118.com/html/2021/0328/5214032221003204.shtm)

[最Cool Kubernetes网络方案Cilium入门教程 - 云+社区 - 腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1626943)


[开启 eBPF，代替 iptables，加速 Istio](https://baijiahao.baidu.com/s?id=1726604684964173717&wfr=spider&for=pc)

# 重点阅读
[[译] 利用 ebpf sockmap/redirection 提升 socket 性能（2020）](https://arthurchiao.art/blog/socket-acceleration-with-ebpf-zh/)

[ARTHURCHIAO'S BLOG](https://arthurchiao.art/articles-zh/)

https://github.com/ArthurChiao/socket-acceleration-with-ebpf

https://github.com/cyralinc/os-eBPF

[Mimic - a eBPF virtual machine and emulator which runs in userspace](https://golangrepo.com/repo/dylandreimerink-mimic)

[开源项目 Merbridge 深度剖析](https://zhuanlan.zhihu.com/p/506625295)

[Use eBPF instead of iptables
to accelerate the Istio
dataplane](https://events.istio.io/istiocon-2022/slides/b6-ebpf-iptables.pdf)

[从0到0.5:eBPF加速ServiceMesh实践](http://elssm.top/2022/02/28/%E4%BB%8E0%E5%88%B00-5-eBPF%E5%8A%A0%E9%80%9FServiceMesh%E5%AE%9E%E8%B7%B5/)

[基于 Ubuntu 21.04 BPF 开发环境全攻略 | 深入浅出 eBPF](https://www.ebpf.top/post/ubuntu_2104_bpf_env/)

## eBPF&tc

[Understanding tc “direct action” mode for BPF](https://arthurchiao.art/blog/understanding-tc-da-mode-zh/)

[Ubuntu 21.10 编写 eBPF tc 程序](https://alenliu.blog.csdn.net/article/details/125754880)

[Advanced: XDP interacting with TC](https://github.com/xdp-project/xdp-tutorial/blob/master/advanced01-xdp-tc-interact/README.org)

[你的第一个TC BPF 程序](https://cloud.tencent.com/developer/article/1626377)

[eBPF: Traffic Control Subsystem](https://blog.51cto.com/u_15703183/5464446)

[Exploring Kernel Networking: BPF Hook Points, Part 1 – Elementary, My Dear Watson](https://blog.stackpath.com/bpf-hook-points-part-1/)

[Exploring Kernel Networking: BPF Hook Points, Part 2 – Say “hello” to my little friend!](https://blog.stackpath.com/bpf-hook-points-part-2/)

[Deep dive & Getting started with PSA implementation for eBPF](https://opennetworking.org/wp-content/uploads/2022/05/Deep-Dive-Getting-Started-with-PSA-Implementation-for-eBFP-Final-Slide-Deck.pdf)

[Cilium 从 0 到 0.1](https://domc.me/2021/10/17/cilium_0_to_0_1/)

[Understanding the eBPF networking features in RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_networking/assembly_understanding-the-ebpf-features-in-rhel_configuring-and-managing-networking#doc-wrapper)

https://github.com/mikeroyal/eBPF-Guide

[Clion配置ebpf-xdp环境](https://zhuanlan.zhihu.com/p/491491882)

## eBPF XDP

[eBPF XDP: The Basics and a Quick Tutorial](https://www.tigera.io/learn/guides/ebpf/ebpf-xdp/)

https://www.ebpf.top/post/ebpf_learn_path/

https://elixir.bootlin.com/linux/v5.19/source/include/uapi/linux/bpf.h

## Ubuntu Jammy (22.04) LTS

https://maofeichen.com/setup-the-extended-berkeley-packet-filter-ebpf-environment/

```bash
PUBKEY=4EB27DB2A3B88B8B
gpg --keyserver keyserver.ubuntu.com --recv "${PUBKEY}"
gpg --export --armor "${PUBKEY}" | apt-key add -

sudo apt -y update
sudo apt -y full-upgrade
sudo apt -y autoclean
sudo apt -y autoremove

sudo apt install -y build-essential git make libelf-dev strace tar bpfcc-tools \
linux-headers-$(uname -r) binutils-dev gcc-multilib libcap-dev libpcap-dev flex \
pkg-config bison libssl-dev dwarves docutils-common zstd bear

sudo apt install -y linux-source

#https://apt.llvm.org/
wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add -

#Jammy (22.04) LTS
cat > /etc/apt/sources.list.d/llvm.list <<EOF
deb http://apt.llvm.org/jammy/ llvm-toolchain-jammy-15 main
deb-src http://apt.llvm.org/jammy/ llvm-toolchain-jammy-15 main
EOF

sudo apt remove -y clang-* llvm-* --purge
sudo apt -y update
sudo apt -y autoremove
sudo apt -y autoclean

sudo apt install -y clang-format clang-tidy clang-tools clang clangd \
libc++-dev libc++1 libc++abi-dev libc++abi1 libclang-dev libclang1 liblldb-dev \
libllvm-ocaml-dev libomp-dev libomp5 lld lldb llvm-dev llvm-runtime llvm python3-clang

git clone git://git.kernel.org/pub/scm/linux/kernel/git/netdev/net-next.git --depth=1 -b v5.19

cd net-next
git tag
cp /boot/config-`uname -r`* .config; make menuconfig

scripts/config --disable SYSTEM_TRUSTED_KEYS
scripts/config --disable SYSTEM_REVOCATION_KEYS
sed -i 's#CONFIG_BPF_UNPRIV_DEFAULT_OFF=y#CONFIG_BPF_UNPRIV_DEFAULT_OFF=n#g' .config

bear -- make -j8
sudo make modules_install
sudo make headers_install
sudo make install
#sudo make INSTALL_MOD_STRIP=1 modules_install install
sudo update-grub2

../kernel-grok/generate_cmake
mkdir build
cd build
cmake ..
make -j8

sudo systemctl reboot
uname -sr

cd net-next/tools/testing/selftests/bpf
make
sudo ./test_verifier

cd ~
git clone --recursive https://github.com/libbpf/libbpf-bootstrap.git
cd libbpf-bootstrap/examples/c
make
ls -hl
sudo strace -e bpf ./bootstrap
```

### Ref Script

```bash
make -C /root/net-next.samples/samples/bpf/../../tools/lib/bpf RM='rm -rf' 


EXTRA_CFLAGS="-Wall -O2 -Wmissing-prototypes -Wstrict-prototypes -I./usr/include -I./tools/testing/selftests/bpf/ -I/root/net-next.samples/samples/bpf/libbpf/include -I./tools/include -I./tools/perf -DHAVE_ATTR_TEST=0" \
        LDFLAGS= srctree=/root/net-next.samples/samples/bpf/../../ \
        O= OUTPUT=/root/net-next.samples/samples/bpf/libbpf/ DESTDIR=/root/net-next.samples/samples/bpf/libbpf


include_directories("/root/net-next/include")
include_directories("/root/net-next.samples/usr/include")
include_directories("/root/net-next.samples/tools/testing/selftests/bpf")
include_directories("/root/net-next/samples/bpf/libbpf/include")
include_directories("/root/net-next.samples/tools/include")
include_directories("/root/net-next.samples/tools/perf")

make -C /root/net-next/samples/bpf/../../tools/bpf/bpftool srctree=/root/net-next/samples/bpf/../../ \
        OUTPUT=/root/net-next/samples/bpf/bpftool/ \
        LIBBPF_OUTPUT=/root/net-next/samples/bpf/libbpf/ \
        LIBBPF_DESTDIR=/root/net-next/samples/bpf/libbpf/


make -C /root/net-next/samples/bpf/../../tools/lib/bpf RM='rm -rf' EXTRA_CFLAGS="-Wall -O2 -Isamples/bpf/../../tools/include -Isamples/bpf/../../tools/include/uapi -I/root/net-next/samples/bpf/libbpf/include -Isamples/bpf/../../tools/testing/selftests/bpf" \
        LDFLAGS= srctree=/root/net-next/samples/bpf/../../ \
        O= OUTPUT=/root/net-next/samples/bpf/libbpf/ DESTDIR=/root/net-next/samples/bpf/libbpf prefix= \
        /root/net-next/samples/bpf/libbpf/libbpf.a install_headers




gcc -Wp,-MD,samples/bpf/.sampleip_user.o.d -Wall -O2 -Wmissing-prototypes -Wstrict-prototypes -I./usr/include -I./tools/testing/selftests/bpf/ -I/root/net-next/samples/bpf/libbpf/include -I./tools/include -I./tools/perf -DHAVE_ATTR_TEST=0  -c -o samples/bpf/sampleip_user.o samples/bpf/sampleip_user.c



gcc -Wp,-MD,samples/bpf/.sampleip.d -Wall -O2 -Wmissing-prototypes -Wstrict-prototypes -I./usr/include -I./tools/testing/selftests/bpf/ -I/root/net-next/samples/bpf/libbpf/include -I./tools/include -I./tools/perf -DHAVE_ATTR_TEST=0   -o samples/bpf/sampleip samples/bpf/sampleip_user.o samples/bpf/../../tools/testing/selftests/bpf/trace_helpers.o /root/net-next/samples/bpf/libbpf/libbpf.a -lelf -lz 



clang -nostdinc -I./arch/x86/include -I./arch/x86/include/generated  -I./include -I./arch/x86/include/uapi -I./arch/x86/include/generated/uapi -I./include/uapi -I./include/generated/uapi -include ./include/linux/compiler-version.h -include ./include/linux/kconfig.h -fno-stack-protector -g \
        -Isamples/bpf -I./tools/testing/selftests/bpf/ \
        -I/root/net-next/samples/bpf/libbpf/include \
        -D__KERNEL__ -D__BPF_TRACING__ -Wno-unused-value -Wno-pointer-sign \
        -D__TARGET_ARCH_x86 -Wno-compare-distinct-pointer-types \
        -Wno-gnu-variable-sized-type-not-at-end \
        -Wno-address-of-packed-member -Wno-tautological-compare \
        -Wno-unknown-warning-option  \
        -fno-asynchronous-unwind-tables \
        -I./samples/bpf/ -include asm_goto_workaround.h \
        -O2 -emit-llvm -Xclang -disable-llvm-passes -c samples/bpf/sampleip_kern.c -o - | \
        opt -O2 -mtriple=bpf-pc-linux | llvm-dis | \
        llc -march=bpf  -filetype=obj -o samples/bpf/sampleip_kern.o



link_directories("/root/net-next.samples/samples/bpf/libbpf")

include_directories("/root/net-next.samples/usr/include")

include_directories("/root/net-next/arch/x86/include")
include_directories("/root/net-next/arch/x86/include/uapi")
include_directories("/root/net-next/include")

include_directories("/root/net-next.samples/samples/bpf/libbpf/include")
include_directories("/root/net-next.samples/tools/perf")
include_directories("/root/net-next.samples/tools/testing/selftests/bpf")

add_library(kernel OBJECT
    /root/net-next/samples/bpf/sampleip_user.c
    /root/net-next/samples/bpf/sampleip_kern.c
)
```

