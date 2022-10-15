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
pkg-config bison libssl-dev dwarves docutils-common zstd

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

make -j8
sudo make modules_install install
#sudo make INSTALL_MOD_STRIP=1 modules_install install
sudo update-grub2

sudo systemctl reboot
uname -r

cd net-next/tools/testing/selftests/bpf
make
sudo ./test_verifier
```

