# 令人惊叹的 eBPF [![令人惊叹](https://awesome.re/badge.svg)](https://github.com/sindresorhus/awesome)

>一个关于eBPF的项目精选清单。

BPF，即伯克利数据包过滤器（Berkeley Packet Filter），是运行从用户空间传递的程序的内核虚拟机。最初在BSD上实现，然后移植到Linux上，在内核中使用“经典BPF”或cBPF机器，例如tcpdump等工具用于过滤数据包，以避免将数据复制到用户空间。最近，Linux中的BPF基础设施已经完全重构，并诞生了“扩展BPF”（eBPF），它获得了新功能（程序的安全性和终止检查、JIT编译、持久化映射、标准库、硬件卸载支持等），并且现在被用于许多任务。在非常低的水平（XDP）处理数据包，跟踪和监视系统上的事件，或者强制执行访问控制cgroups等都是eBPF为其提供性能，可编程性和灵活性的一些例子。

最近，[Cilium](https://cilium.io) 推出了一个关于 eBPF 的很棒的网站 [ebpf.io](https://ebpf.io/)。它有着类似于这份列表的作用，提供了 [eBPF 简介](https://ebpf.io/what-is-ebpf) 以及与之相关的项目链接。

> 注意： eBPF 是一项令人兴奋的技术，其生态系统不断发展。我们很希望得到您的帮助，以使这个很棒的列表保持最新，以及以任何我们能做到的方式来提高其信噪比。请随意在 [这里](https://github.com/zoidbergwill/awesome-ebpf/issues) 留下任何反馈。

## 目录

- [参考文档](#reference-documentation)
- [文章和演示文稿](#articles-and-presentations)
- [教程](#tutorials)
- [示例](#examples)
- [eBPF 工作流程：工具和实用程序](#ebpf-workflow-tools-and-utilities)
- [与 eBPF 相关的项目](#projects-related-to-ebpf)
- [eBPF 在安全领域的应用](#ebpf-in-security)
- [源代码](#the-code)
- [开发和社区](#development-and-community)
- [其他 eBPF 资源列表](#other-lists-of-resources-on-ebpf)
- [致谢](#acknowledgement)

## 参考文档

### eBPF 基础知识

- [ebpf.io](https://ebpf.io/) - 一个查找 eBPF 的所有基础知识的门户网站，包括相关主要项目和社区资源的列表。
- [Cilium's BPF and XDP Reference Guide](http://docs.cilium.io/en/latest/bpf/) - 关于 eBPF 大多数特性和方面的深入文档。

### 内核文档

- [BPF文档](https://www.kernel.org/doc/html/latest/bpf/index.html) - 包含Linux内核相关BPF文档的索引。
- [linux/Documentation/networking/filter.rst](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/Documentation/networking/filter.rst) - eBPF规范（略有过时；信息仍然有效，但不全面）。
- [BPF设计问答](https://www.kernel.org/doc/html/latest/bpf/bpf_design_QA.html) - 关于BPF基础设施决策的常见问题。
- [如何与BPF子系统交互](https://www.kernel.org/doc/html/latest/bpf/bpf_devel_QA.html) - eBPF开发贡献的常见问题。

### 手册页面

- [`bpf(2)`](http://man7.org/linux/man-pages/man2/bpf.2.html) - 用于从用户空间管理 BPF 程序和映射的系统调用 `bpf()` 的手册页。
- [`tc-bpf(8)`](http://man7.org/linux/man-pages/man8/tc-bpf.8.html) - 关于如何与 tc 一起使用 BPF 的手册页，包括示例命令和代码示例。
- [`bpf-helpers(7)` 手册页](http://man7.org/linux/man-pages/man7/bpf-helpers.7.html) - 描述组成 BPF 标准库的内核帮助程序函数。

### 其他

- [IO Visor的非官方eBPF规范](https://github.com/iovisor/bpf-docs/blob/master/eBPF.md) - eBPF语法和操作码的摘要。
- [Jesper Dangaard Brouer的文档](https://prototype-kernel.readthedocs.io/en/latest/bpf/index.html) - 正在进行中，欢迎贡献。
- 来自David Miller发送到[xdp-newbies](http://vger.kernel.org/vger-lists.html#xdp-newbies)邮件列表的邮件：

- [bpf.h 和您…](https://www.spinics.net/lists/xdp-newbies/msg00179.html)
  - [从上下文角度讲...](https://www.spinics.net/lists/xdp-newbies/msg00181.html)
  - [BPF 验证器概述](https://www.spinics.net/lists/xdp-newbies/msg00185.html)

- [内核版本中的 BPF 特性列表](https://github.com/iovisor/bcc/blob/master/docs/kernel-versions.md)

## 文章和演示

### 通用的 eBPF 演示文稿和文章

如果你刚接触eBPF，你可能想尝试本节中被描述为“介绍”的链接。

- [XDP 和 eBPF 简介](https://blogs.igalia.com/dpino/2019/01/07/introduction-to-xdp-and-ebpf/) - 一篇通俗易懂的介绍，提供了关于 eBPF 的背景、历史和运作细节。
- eBPF 概览 - Adrian Ratiu 的博客系列，涵盖了 eBPF 基础设施的许多方面。

- [第一部分：介绍](https://www.collabora.com/news-and-blog/blog/2019/04/05/an-ebpf-overview-part-1-introduction/)
  - [第二部分：机器和字节码](https://www.collabora.com/news-and-blog/blog/2019/04/15/an-ebpf-overview-part-2-machine-and-bytecode/)

- [Ferris Ellis的关于eBPF的博客文章](https://ferrisellis.com/tags/ebpf/) - 他们有几篇关于eBPF的文章：
  - [第一部分：过去、现在和未来](https://ferrisellis.com/content/ebpf_past_present_future/)
  - [第二部分：系统调用和映射类型](https://ferrisellis.com/content/ebpf_syscall_and_maps/)
- [BPF参考指南](https://github.com/iovisor/bcc/blob/master/docs/reference_guide.md) - 关于BPF C和bcc Python助手，来自bcc存储库。
- [使用BPF和XDP使内核的网络数据通路可编程化](http://schd.ws/hosted_files/ossna2017/da/BPFandXDP.pdf) - 一组幻灯片，涵盖了有关eBPF和XDP的所有基础知识（主要用于网络处理）。
- [BSD数据包过滤器](https://speakerdeck.com/tuxology/the-bsd-packet-filter) - 主要介绍跟踪方面。
- [BPF：跟踪和更多](http://www.slideshare.net/brendangregg/bpf-tracing-and-more) - 主要介绍跟踪方面。
- [Linux BPF Superpowers](http://www.slideshare.net/brendangregg/linux-bpf-superpowers) - 主要介绍跟踪方面，第一部分附带火焰图。
- [IO Visor](https://www.socallinuxexpo.org/sites/default/files/presentations/Room%20211%20-%20IOVisor%20-%20SCaLE%2014x.pdf) - 也介绍了[IO Visor项目](https://www.iovisor.org/)。
- [BPF - 内核虚拟机](http://vger.kernel.org/netconf2015Starovoitov-bpf_collabsummit_2015feb20.pdf) - eBPF的作者发表的演讲。
- [扩展扩展BPF](https://lwn.net/Articles/603983/) - 2014年的一篇博客文章，介绍BPF的开发并演示了如何使用它进行有状态套接字过滤，通过将eBPF程序附加到套接字。
- Greg Marsden制作了一些关于eBPF的文档：
  - [程序类型之旅](https://blogs.oracle.com/linux/notes-on-bpf-1) - 描述了所有现有的BPF程序类型的挂钩及其相关的兴趣点。
  - [BPF助手函数](https://blogs.oracle.com/linux/notes-on-bpf-2) - 对内核函数的回顾，这些函数可以从eBPF程序中调用。
  - [与用户空间通信](https://blogs.oracle.com/linux/notes-on-bpf-3) - BPF如何与用户空间通信 - BPF映射、perf事件、bpf_trace_printk。
  - [构建BPF程序](https://blogs.oracle.com/linux/notes-on-bpf-4) - 设置您的环境以构建BPF程序。
  - [BPF字节码和BPF验证器](https://blogs.oracle.com/linux/notes-on-bpf-5) - BPF如何确保程序安全?
  - [使用BPF进行数据包转换](https://blogs.oracle.com/linux/notes-on-bpf-6) - 关于数据包转换的一个eBPF用法。
- [通过eBPF观测Linux内核](https://sematext.com/blog/linux-kernel-observability-ebpf/) - 一篇博客文章，介绍了eBPF的基础知识以及如何在Go中编写和加载最小的eBPF程序到内核中的代码示例。
- [eBPF - 程序员的视角](https://www.researchgate.net/publication/349173667_eBPF_-_From_a_Programmer's_Perspective) - 一篇简短的论文，描述了eBPF的基本原理以及如何开始编写eBPF程序。
- [Cloudflare关于eBPF的博客文章](https://blog.cloudflare.com/tag/ebpf/) - 不同的博客文章，涉及关于网络使用案例和eBPF低级方面的内容。
- [Linux扩展BPF（eBPF）跟踪工具](https://www.brendangregg.com/ebpf.html) - 深入收集了使用eBPF的性能分析工具示例的信息。页面最后还有其他资源的部分。
- [eBPF入门指南](https://github.com/lizrice/ebpf-beginners) - 一组现场编码讲座及其附带的代码示例，介绍使用各种库和程序类型进行eBPF编程。

### BPF 内部机制

- Daniel Borkmann已经做了几次关于eBPF内部的演讲和论文，特别是关于它与tc一起使用的。

- [eBPF 和 XDP 指南以及最新的更新 (2017)](https://fosdem.org/2017/schedule/event/ebpf_xdp/)
  - [tc的cls_bpf高级可编程性和最新更新](http://netdevconf.org/1.2/session.html?daniel-borkmann) - 有关eBPF，它在隧道和封装、直接数据包访问等方面的使用等详细信息。
  - [自netdev 1.1以来的cls_bpf/eBPF更新](http://netdevconf.org/1.2/slides/oct5/07_tcws_daniel_borkmann_2016_tcws.pdf) - 属于[tc研讨会](http://netdevconf.org/1.2/session.html?jamal-tc-workshop)的一部分。
  - [如何使 tc 分类器完全可编程化](http://www.netdevconf.org/1.1/proceedings/slides/borkmann-tc-classifier-cls-bpf.pdf) - 介绍 eBPF，包括几个特性 (映射管理，尾部调用，校验器等)。全文[此处也可获得](http://www.netdevconf.org/1.1/proceedings/papers/On-getting-tc-classifier-fully-programmable-with-cls-bpf.pdf)。
  - [Linux tc 和 eBPF](https://archive.fosdem.org/2016/schedule/event/ebpf/attachments/slides/1159/export/events/attachments/ebpf/slides/1159/ebpf.pdf)。

- [IO Visor 博客](https://www.iovisor.org/resources/blog)
- [Linux 网络解析](http://www.slideshare.net/ThomasGraf5/linux-networking-explained) - Linux 网络内部，其中包括关于 eBPF 的一部分。

### 内核跟踪

- [Linux下的全系统动态追踪：eBPF和bpftrace](https://www.joyfulbikeshedding.com/blog/2019-01-31-full-system-dynamic-tracing-on-linux-using-ebpf-and-bpftrace.html) - 详细介绍了使用eBPF进行追踪的过程，包括列出可用的追踪点和运行bpftrace程序等。
- [eBPF和内核跟踪的初次相遇](http://www.slideshare.net/vh21/meet-cutebetweenebpfandtracing) - Kprobes、uprobes、ftrace等。
- [Linux内核跟踪](http://www.slideshare.net/vh21/linux-kernel-tracing) - Systemtap、Kernelshark、trace-cmd、LTTng、perf-tool、ftrace、hist-trigger、perf、function tracer、tracepoint、kprobe/uprobe等。
- Brendan Gregg的博客，特别是[Linux BPF Superpowers](http://www.brendangregg.com/blog/2016-03-05/linux-bpf-superpowers.html)一文。

### XDP

- [The eXpress Data Path](https://blogs.igalia.com/dpino/2019/01/10/the-express-data-path/) - 一篇介绍XDP的非常易懂的入门文章，提供了示例代码以展示如何处理数据包。
- 所有XDP的细节都在这篇技术论文中：[The eXpress Data Path: Fast Programmable Packet Processing in the Operating System Kernel](https://github.com/tohojo/xdp-paper)，作者为Toke Høiland-Jørgensen、Jesper Dangaard Brouer、Daniel Borkmann、John Fastabend、Tom Herbert、David Ahern和David Miller，他们都是重要的eBPF和XDP贡献者。
- [XDP正在进行中的文档](https://prototype-kernel.readthedocs.io/en/latest/networking/XDP/index.html)
- [BPF和XDP参考指南](http://docs.cilium.io/en/latest/bpf/) - Cilium项目的指南。
- [XDP项目概述](https://www.iovisor.org/technology/xdp)
- [eXpress Data Path (XDP)](https://github.com/iovisor/bpf-docs/raw/master/Express_Data_Path.pdf) - 关于XDP的第一份演示文稿。
- [BoF - BPF能为您做些什么？](https://events.linuxfoundation.org/sites/events/files/slides/iovisor-lc-bof-2016.pdf)
- [eXpress Data Path](http://www.slideshare.net/IOVisor/express-data-path-linux-meetup-santa-clara-july-2016) - 包含mlx4驱动程序获得的一些基准测试结果。
- Jesper Dangaard Brouer有几个幻灯片集，描述了XDP的内部内容：

- [XDP − eXpress Data Path, Intro and future use-cases](http://people.netfilter.org/hawk/presentations/xdp2016/xdp_intro_and_use_cases_sep2016.pdf) - Linux内核与DPDK的比拼。目前（撰写本文时）的XDP未来计划以及与DPDK的比较。
  - [Network Performance Workshop](http://netdevconf.org/1.2/session.html?jesper-performance-workshop) - XDP内部机理的额外提示以及预期发展。
  - [XDP – eXpress Data Path, Used for DDoS protection](http://people.netfilter.org/hawk/presentations/OpenSourceDays2017/XDP_DDoS_protecting_osd2017.pdf) - 关于XDP详细信息和用例，包括基于IP黑名单方案的基准结果和基于eBPF / XDP的基本DDoS保护的代码片段。
  - [Memory vs. Networking, Provoking and fixing memory bottlenecks](http://people.netfilter.org/hawk/presentations/MM-summit2017/MM-summit2017-JesperBrouer.pdf) - XDP开发人员当前内存问题的高级细节。
  - [XDP for the Rest of Us](http://netdevconf.org/2.1/session.html?gospodarek) - 如何开始使用eBPF和XDP。Julia Evans也在[她的博客](http://jvns.ca/blog/2017/04/07/xdp-bpf-tutorial/)上对其进行了总结。
  - [XDP now with REDIRECT](http://people.netfilter.org/hawk/presentations/LLC2018/XDP_LLC2018_redirect.pdf) - XDP的更新，特别是重定向操作的更新。

- [XDP工作坊 -- 介绍、经验及未来发展（视频）](http://netdevconf.org/1.2/session.html?herbert-xdp-workshop)
- [Linux 上的高速数据包过滤](https://cdn.shopify.com/s/files/1/0177/9886/files/phv2017-gbertin.pdf) - 关于 Linux 上的数据包过滤、DDoS 保护、内核中的数据包处理、内核旁路、XDP 和 eBPF。
- [如何每秒丢弃 1000 万个数据包](https://blog.cloudflare.com/how-to-drop-10-million-packets/) - Cloudflare 的博客文章，介绍了他们使用 XDP 进行数据包过滤的经验。

### AF_XDP

- [AF_XDP](https://www.kernel.org/doc/html/latest/networking/af_xdp.html) - AF_XDP地址族的内核文档。
- [在Linux中使用AF_XDP实现快速数据包处理](https://archive.fosdem.org/2018/schedule/event/af_xdp/)。

### bpfilter

- [为什么内核社区要用BPF替换iptables？](https://cilium.io/blog/2018/04/17/why-is-the-kernel-community-replacing-iptables/) - Cilium的一篇博客文章，介绍eBPF和bpfilter的动机，并提供一些例子和链接到使用eBPF和bpfilter的其他项目。
- [bpfilter：配有eBPF的Linux防火墙](https://qmo.fr/docs/talk_20180316_frnog_bpfilter.pdf) - Quentin Monnet的演讲幻灯片，介绍eBPF背景，将bpfilter与iptables进行比较。

### BTF
### BTF

- [BPF类型格式（BTF）](https://www.kernel.org/doc/html/latest/bpf/btf.html) - 有关BTF的内核文档，解释了如何使用它。
- [使用BTF类型信息增强Linux内核](https://facebookmicrosites.github.io/bpf/blog/2018/11/14/btf-enhancement.html) - 介绍了使用BTF为BPF程序提供调试信息的工作。

### cBPF

### 传统BPF

- [BSD 数据包过滤器：用户级数据包捕获的新架构](http://www.tcpdump.org/papers/bpf-usenix93.pdf) - 有关 （经典的） BPF 的原始论文。
- [FreeBSD 中有关 BPF 的手册页面](https://www.freebsd.org/cgi/man.cgi?query=bpf&sektion=4)
- [Linux 的 packet mmap(2), BPF 和 Netsniff-NG](http://borkmann.ch/talks/2013_devconf.pdf)
- [tc 和 cls bpf：使用 BPF 进行轻量级数据包分类](http://borkmann.ch/talks/2014_devconf.pdf)
- [介绍 Cloudflare 的 BPF 工具](https://blog.cloudflare.com/introducing-the-bpf-tools/) - 使用 `xt_bpf` 模块和 BPF 字节码来操作 iptables。
- [Libpcap 过滤器语法](http://biot.com/capstats/bpf.html)

### 硬件卸载

- [eBPF/XDP 硬件卸载到 SmartNICs](http://netdevconf.org/1.2/session.html?jakub-kicinski) - Netronome 引入的针对带有 TC 或 XDP（Linux kernel 4.9+）的 eBPF 的硬件卸载方案。
- [全面的 XDP 卸载——处理边缘情况](https://www.netdevconf.org/2.2/session.html?viljoen-xdpoffload-talk) - 上述主题的更新。
- [hBPF - eBPF 在硬件中的实现](https://github.com/rprinz08/hBPF) - 针对 FPGAs 编写的 eBPF CPU。
- [OpenCSD eBPF SSD 卸载](https://github.com/Dantali0n/qemu-csd) - 计算存储模拟（QEMU）平台，使用 FUSE LFS 文件系统和 uBPF 进行计算内核卸载，适用于分区命名空间 NVMe SSD，全部在用户空间中。

## 教程

- [bcc 参考指南](https://github.com/iovisor/bcc/blob/master/docs/reference_guide.md) - 许多增量步骤来开始使用 bcc 和 eBPF，大多集中在跟踪和监视上。
- [bcc Python 开发者教程](https://github.com/iovisor/bcc/blob/master/docs/tutorial_bcc_python_developer.md) - 随 bcc 一起提供，但针对 Python 代码，共包含十七个“课程”。
- [使用 libbpf-bootstrap 构建 BPF 应用程序](https://nakryiko.com/posts/libbpf-bootstrap/) - 帮助生成启动自己应用程序的最小或高级模板（内核侧和用户空间管理映射和程序），具有诸如 CO-RE、全局变量和环形缓冲区之类的功能。
- [我是如何使用纯 C 和 eBPF 编写 opensnoop 的](https://bolinfest.github.io/opensnoop-native/) - 对如何编写 eBPF 程序进行彻底介绍，首先仅使用 bpf() 系统调用，然后使用 libbpf 库，以及可复现的代码示例。
- [Linux 跟踪工作坊材料](https://github.com/goldshtn/linux-tracing-workshop) - 使用多个 BPF 工具进行跟踪。
- [使用 Linux tracepoints、perf 和 eBPF 跟踪数据包行程](https://blog.yadutaf.fr/2017/07/28/tracing-a-packet-journey-using-linux-tracepoints-perf-ebpf/) - 使用 perf 和 bcc 程序解决 ping 请求和响应的问题。
- [Open NFP 平台](https://open-nfp.org/dataplanes-ebpf/technical-papers/) - 由 Netronome 运营：一些与网络相关的 eBPF 应用实例教程，包括 eBPF 拦截入门指南。
- [XDP for the Rest of Us](http://netdevconf.org/2.1/session.html?gospodarek) - 一个工作坊的第一版，用于开始学习 XDP。
- [XDP for the Rest of Us](https://www.netdevconf.org/2.2/session.html?gospodarek-xdp-workshop) - 第二版，带有新的内容。
- [使用 ip（iproute2）命令加载 XDP 程序](https://medium.com/@fntlnz/load-xdp-programs-using-the-ip-iproute2-command-502043898263)
- [XDP 实践教程](https://github.com/xdp-project/xdp-tutorial) - 渐进式（包含三个难度级别）的教程，学习如何使用 XDP 处理数据包。
- [所有的跟踪都属于 BPF](https://www.trailofbits.com/post/all-your-tracing-are-belong-to-bpf) - 一步步指导的过程，将跟踪能力集成到您的 C++ 应用程序中，使用 LLVM 库。

## 示例

- [linux/samples/bpf/](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/samples/bpf) - 内核树：一些 eBPF 程序示例。
- [linux/tools/testing/selftests/bpf](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/tools/testing/selftests/bpf) - 内核树：Linux BPF 自测，包含许多 eBPF 程序。
- [prototype-kernel/kernel/samples/bpf](https://github.com/netoptimizer/prototype-kernel/tree/master/kernel/samples/bpf) - Jesper Dangaard Brouer 的原型内核存储库包含一些可以在内核基础设施之外编译的附加示例。
- [iproute2/examples/bpf/](https://git.kernel.org/pub/scm/network/iproute2/iproute2-next.git/tree/examples/bpf) - 一些网络程序用于连接到 TC 接口。
- [Netronome sample network applications](https://github.com/Netronome/bpf-samples/) - 提供基本但完整的 eBPF 应用程序示例，也与硬件卸载兼容。
- [bcc/examples](https://github.com/iovisor/bcc/tree/master/examples) - 与 bcc 工具一起提供的示例，主要与跟踪有关。
- [bcc/tools](https://github.com/iovisor/bcc/tree/master/tools) - 这些工具本身可以被视为 BPF 程序的示例用例，主要用于追踪和监视。 bcc 工具已针对一些 Linux 发行版进行了打包。
- [MPLSinIP sample](https://github.com/fzakaria/eBPF-mpls-encap-decap) - 大量注释的示例，演示了如何在 IP 中封装和解封装 MPLS。 该代码适用于 BPF 开发新手。
- [ebpf-samples](https://github.com/vbpf/ebpf-samples) - 多个项目中收集的编译（作为 ELF 对象文件）的示例集合，主要用作用户空间验证器的测试用例。
- [ebpf-kill-example](https://github.com/niclashedam/ebpf-kill-example) - 完全记录和测试过的 eBPF 探针示例，可记录所有强制终止并在用户空间中将其打印出来。
- [redbpf examples](https://github.com/foniod/redbpf/tree/main/examples) - 使用 RedBPF 编写 Rust eBPF 程序的示例程序。

## eBPF 工作流程：工具和实用程序

### 抄送

- [bcc](https://github.com/iovisor/bcc/) - 框架和工具 - 一种处理BPF程序的方法，特别是用于跟踪和监视。还包括一些实用程序，可帮助检查系统中的映射或程序。
- [用于BCC的Lua前端](https://github.com/iovisor/bcc/tree/master/src/lua) - 另一种替代C，甚至是bcc中大多数Python代码的选择。

### iproute2

- [iproute2](https://git.kernel.org/pub/scm/network/iproute2/iproute2.git) - 这个软件包包含了在 Linux 上进行网络管理的工具，其中包括了用于管理 eBPF 过滤器和动作的 `tc`，以及用于管理 XDP 程序的 `ip`。大多数与 BPF 相关的代码都在 lib/bpf.c 中。
- [iproute2-next](https://git.kernel.org/pub/scm/network/iproute2/iproute2-next.git) - 这是 iproute2 的开发树，与 net-next 同步更新。

### LLVM
### LLVM

- [LLVM](https://llvm.org/) - 包含在 eBPF 工作流程中广泛使用的多个工具。最新版本的 Ubuntu/Debian 快照可以从 [这里](http://apt.llvm.org/) 获取。

- clang被用来将C语言编译成eBPF格式的ELF目标文件（需使用clang v3.7.1+）。 BPF后端是通过[此提交](https://reviews.llvm.org/D6494)添加的。
- llvm-objdump用于以人类可读的格式转储目标文件的内容，可能包括初始的C源代码（需使用llvm-objdump v4.0+）。
- llvm-mc用于从LLVM中间表示编译成eBPF目标文件，因此可以从C语言编译成eBPF汇编语言，进而修改汇编代码，最后编译成ELF文件。

### libbpf

- [libbpf](https://git.kernel.org/pub/scm/linux/kernel/git/davem/net-next.git/tree/tools/lib/bpf) - 一个用于处理BPF对象（程序和映射）和操作包含它们的ELF对象文件的C库。它随内核一起提供，并在[GitHub上进行了镜像](https://github.com/libbpf/libbpf)。
- [libbpf-bootstrap](https://github.com/libbpf/libbpf-bootstrap) - 用于使用libbpf和BPF CO-RE进行BPF应用开发的脚手架。

### Go 库

- [cilium/ebpf](https://github.com/cilium/ebpf) - 纯Go库，用于读取、修改、加载eBPF程序并将其附加到Linux内核中的各种钩子。
- [libbpfgo](https://github.com/aquasecurity/libbpfgo) - 由libbpf支持的用于Go的eBPF库。
- [gobpf](https://github.com/iovisor/gobpf) - 用于创建eBPF程序的BCC的Go绑定。

### 阿嫣

- [aya](https://github.com/aya-rs/aya) - 一种用纯 Rust 编写、加载和管理 eBPF 对象的库，专注于开发人员体验和可操作性。它支持在 Rust 中编写 eBPF 程序，并通过 crates.io 分发库代码以在 eBPF 程序之间共享。Aya 不依赖于 libbpf。
- [aya-template](https://github.com/aya-rs/aya-template) - 用于在 Aya 中编写 BPF 应用程序的模板，可以与 [`cargo generate`](https://github.com/cargo-generate/cargo-generate) 一起使用。

### eunomia-bpf

- [eunomia-bpf](https://github.com/eunomia-bpf/eunomia-bpf) - 一个编译框架和运行库，可用于构建、分发、动态加载和运行多语言和WebAssembly的CO-RE eBPF应用程序。它支持仅写eBPF内核代码（以构建简单的CO-RE libbpf eBPF应用程序）、同时以BCC和libbpf风格编写内核部分，以及在WASM模块中以多种语言编写用户空间，并使用简单的JSON数据或WASM OCI镜像分发它。运行时仅基于libbpf，并提供CO-RE给BCC-style的eBPF程序，而不依赖于LLVM库。

### 氧化物bpf

- [oxidebpf](https://github.com/redcanaryco/oxidebpf) - 一个纯Rust库，用于管理eBPF程序，专为安全用例设计。功能集比其他库更有限，但强调在广泛的内核范围和向后兼容的编译一次运行多个地方方面的稳定性。

### bpftool和内核树中的其他工具

- [bpftool](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/tree/tools/bpf/bpftool) - 还有一些其他内核树中的工具，位于版本早于4.15的[linux/tools/net/](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/tools/net?h=v4.14)，或者之后的[linux/tools/bpf/](https://git.kernel.org/pub/scm/linux/kernel/git/davem/net-next.git/tree/tools/bpf)。

- [`bpftool`](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/tree/tools/bpf/bpftool) - 一个通用的实用工具，可用于与eBPF程序和用户空间映射进行交互，例如显示、转储、加载、反汇编、附着和分离程序到控制组，或显示、创建、固定、更新、删除映射。
  - [`bpf_asm`](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/tree/tools/bpf/bpf_asm.c) - 一个最小的cBPF汇编器。
  - [`bpf_dbg`](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/tree/tools/bpf/bpf_dbg.c) - 一个用于cBPF程序的小型调试器。
  - [`bpf_jit_disasm`](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/tree/tools/bpf/bpf_jit_disasm.c) - 一种适用于两种BPF语言的反汇编器，对JIT调试非常有用。

### 用户空间 eBPF

- [uBPF](https://github.com/iovisor/ubpf/) - 用 C 编写。包含一个解释器、一个用于 x86_64 架构的 JIT 编译器、一个汇编器和反汇编器。
- [A generic implementation](https://github.com/YutaroHayakawa/generic-ebpf) - 支持 FreeBSD kernel、FreeBSD user space、Linux kernel、Linux user space 和 macOS user space。用于 [VALE 软件交换机](https://www.unix.com/man-page/freebsd/4/vale/) 的 [BPF 扩展模块](https://github.com/YutaroHayakawa/vale-bpf)。
- [rbpf](https://github.com/qmonnet/rbpf) - 用 Rust 编写。用于 Linux、macOS 和 Windows 的解释器，以及在 Linux 下用于 x86_64 的 JIT 编译器。
- [PREVAIL](https://github.com/vbpf/ebpf-verifier) - 用于 eBPF 的用户空间验证器，[使用抽象解释层实现](https://elazarg.github.io/pldi19main-final.pdf)，支持循环。
- [oster](https://github.com/grantseltzer/oster) - 用 Go 编写。通过将 eBPF 附加到 uprobes 来跟踪 Go 程序的执行的工具。
- [wachy](https://rubrikinc.github.io/wachy/) - 一款追踪分析器，旨在通过将跟踪结果显示在源代码旁边并允许交互式分析以简化 eBPF uprobes 调试的使用。

### 其他平台上的eBPF

- [eBPF for Windows](https://github.com/microsoft/ebpf-for-windows) - 这个项目还在进行中，它允许使用现有的eBPF工具链和Linux生态系统中熟悉的API在Windows上使用。

### 在虚拟环境中进行测试

- [Vagrant设置](https://github.com/iovisor/xdp-vagrant) - 方便测试XDP。现在通用的XDP已经存在，所以用处较少（独立于驱动程序，主要用于测试）。
- [Docker容器中的bcc](https://github.com/zlim/bcc-docker)。

## 与 eBPF 相关的项目

### 网络

- P4 与 eBPF 有一些交互：

- [P4 on the Edge](https://schd.ws/hosted_files/2016p4workshop/1d/Intel%20Fastabend-P4%20on%20the%20Edge.pdf) - 使用 eBPF 创建高性能可编程交换机的 P4。
  - [OvS Orbit episode (#11)，名为 P4 on the Edge](https://ovsorbit.org/#e11) - 相关于前一条项目。由 Open vSwitch 核心维护者之一的 Ben Pfaff 对 John Fastabend 进行的音频采访。
  - [P4、EBPF 和 Linux TC Offload](https://open-nfp.org/m/documents/Open_NFP_P4_EBPF_Linux_TC_Offload_FINAL_5JHLETS.pdf) - 部分与 Netronome NFP 网络流处理器架构上的 eBPF 硬件卸载相关的 P4。
  - [P4 使用 eBPF 的旧文档](https://github.com/iovisor/bcc/tree/master/src/cc/frontends/p4) - 来自 bcc 存储库；由下面链接的 P4_16 后端弃用。
  - [eBPF 的 P4_16 后端](https://github.com/p4lang/p4c/blob/master/backends/ebpf/README.md)。

- [Cilium](https://cilium.io/) 项目 ([GitHub 代码库](https://github.com/cilium/cilium)) 是一项依赖于 BPF 和 XDP 技术的项目，可为基于容器的快速内核网络和安全策略实施提供“即时生成的eBPF程序”的支持。有许多演示文稿可用（有些内容重复）：

- [Cilium：使用BPF和XDP为容器提供网络和安全性](http://www.slideshare.net/ThomasGraf5/clium-container-networking-with-bpf-xdp) - 还包括负载均衡用例
  - [Cilium：使用BPF和XDP为容器提供网络和安全性](http://www.slideshare.net/Docker/cilium-bpf-xdp-for-containers-66969823) - [视频](https://www.youtube.com/watch?v=TnJF7ht3ZYc&list=PLkA60AVN3hh8oPas3cq2VA9xB7WazcIgs)
  - [Cilium: 使用BPF和XDP实现快速IPv6容器网络](http://www.slideshare.net/ThomasGraf5/cilium-fast-ipv6-container-networking-with-bpf-and-xdp)
  - [Cilium：容器的BPF和XDP](https://fosdem.org/2017/schedule/event/cilium/)
  - [OvS Orbit 第四集](https://ovsorbit.benpfaff.org/) - Ben Pfaff采访了Thomas Graf。
  - [Cilium的通用介绍](https://opensource.googleblog.com/2016/11/cilium-networking-and-security.html)
  - [采访Thomas Graf的播客](http://blog.ipspace.net/2016/10/fast-linux-packet-forwarding-with.html) - Ivan Pepelnjak在2016年十月采访了Thomas，谈论了eBPF、P4、XDP和Cilium。

- Open vSwitch (OvS)以及相关项目Open Virtual Network (OVN，一款开源的网络虚拟化解决方案)正在考虑在各个级别上使用eBPF:

- [使用eBPF卸载OVS流处理](http://openvswitch.org/support/ovscon2016/7/1120-tu.pdf)
  - [将OVN的灵活性与IOVisor的效率相结合](http://openvswitch.org/support/ovscon2016/7/1245-bertrone.pdf)

- [Katran](https://code.fb.com/open-source/open-sourcing-katran-a-scalable-network-load-balancer/) - 一个基于XDP且由Facebook开源的第四层负载均衡器。
- [XDP实践：将XDP集成到我们的DDoS应对流程中](http://netdevconf.org/2.1/session.html?bertin) - Cloudflare使用XDP进行DDoS防护。
- [Droplet: 由BPF + XDP驱动的DDoS应对措施](http://netdevconf.org/2.1/session.html?zhou) - Facebook使用XDP进行DDoS防护。
- [DPDK有一个基于AF_XDP的轮询模式驱动程序(PMD)](https://dpdkuserspace2018.sched.com/event/G45Z/dpdk-pmd-for-afxdp)
- [XDP的CETH](http://www.slideshare.net/IOVisor/ceth-for-xdp-linux-meetup-santa-clara-july-2016) - 用于更快速的网络输入/输出的通用以太网驱动程序框架，由Mellanox发起。
- Suricata是一款开源入侵检测系统，[依赖于eBPF组件](https://www.stamus-networks.com/2016/09/28/suricata-bypass-feature/)来实现其“捕获绕过”功能。

- [Suricata文档中“eBPF和XDP”部分](http://suricata.readthedocs.io/en/latest/capture-hardware/ebpf-xdp.html?highlight=XDP#ebpf-and-xdp)
  - [SEPTun-Mark-II](https://github.com/pevma/SEPTun-Mark-II) - 极致性能调优指南 - Mark II。
  - [介绍此特性的博客文章](https://www.stamus-networks.com/2016/09/28/suricata-bypass-feature/)
  - [一只Suricate在eBPF领域的冒险经历](http://netdevconf.org/1.2/slides/oct6/10_suricata_ebpf.pdf)
  - [一只浣熊的视角看eBPF和XDP](https://www.slideshare.net/ennael/kernel-recipes-2017-ebpf-and-xdp-eric-leblond)。

- [Project Calico](https://projectcalico.docs.tigera.io/about/about-calico) - Calico是一个开源的网络和网络安全解决方案，针对容器、虚拟机和本地主机负载。Calico的eBPF数据平面提供低延迟、高吞吐量的数据平面和丰富的网络安全策略模型。
  - [使用Calico启用eBPF数据平面](https://projectcalico.docs.tigera.io/maintenance/ebpf/enabling-bpf)
- [merbridge](https://github.com/merbridge/merbridge/) - 使用eBPF加速您的Service Mesh。Merbridge使用eBPF替换iptables规则以拦截流量。它还结合了msg_redirect以减少延迟，并在sidecars和服务之间缩短了数据路径。

### 可观测性

- [InKeV: In-Kernel Distributed Network Virtualization for DCN](https://github.com/iovisor/bpf-docs/blob/master/university/sigcomm-ccr-InKev-2016.pdf)
- [DEEP-mon](https://www.slideshare.net/necstlab/deepmon-dynamic-and-energy-efficient-power-monitoring-for-containerbased-infrastructures) - 用于测量服务器能耗的工具，利用eBPF程序进行数据聚合处理。
- [pixie](https://github.com/pixie-io/pixie) - 使用eBPF进行Kubernetes的可观测性分析。支持协议跟踪，应用程序分析以及分布式bpftrace部署等功能。
- [SkyWalking Rover](https://github.com/apache/skywalking-rover) - [Apache SkyWalking](https://skywalking.apache.org/)是一个专门为分布式微服务、云原生和基于容器（Kubernetes）架构而设计的开源应用程序性能监控（APM）平台。SkyWalking Rover是一个基于eBPF的调试器和度量收集器，支持C、C++、Golang和Rust应用程序。
- [parca-agent](https://github.com/parca-dev/parca-agent) - 基于eBPF的持续分析CPU和内存使用情况的分析器，可分析到代码行和时间流逝情况。
- [rbperf](https://github.com/javierhonduco/rbperf) - 用于Ruby的采样分析器和跟踪器。
- [Hubble](https://github.com/cilium/hubble) - 使用eBPF为Kubernetes提供网络、服务和安全可观测性。
- [Caretta](https://github.com/groundcover-com/caretta) - 通过eBPF生成的即时Kubernetes服务依赖图，可直接输出到Grafana示例。

### 安全

- [Falco](https://falco.org/) - 一款云原生的运行时安全项目，用作 Kubernetes 威胁检测引擎。
- [Sysmon for Linux](https://github.com/Sysinternals/SysmonForLinux) - 一款安全监控工具。它依赖于[SysinternalsEBPF](https://github.com/Sysinternals/SysinternalsEBPF)。
- [Red Canary Linux Agent](https://redcanary.com/blog/ebpf-for-security) - Red Canary 已经开始将 eBPF 纳入其 Linux 安全传感器。
- [Tracee](https://github.com/aquasecurity/tracee) - 一款用于 Linux 的运行时安全和取证工具，它使用 eBPF 技术对系统和应用程序进行跟踪，在运行时分析收集的事件以检测可疑的行为模式。
- [redcanary-ebpf-sensor](https://github.com/redcanaryco/redcanary-ebpf-sensor) - 一组 BPF 程序，从 Linux 内核中收集与安全相关的事件数据。BPF 程序组合成一个单独的 ELF 文件，可以根据运行的操作系统和内核版本选择性加载单个探针。
- [bpflock - 锁定 Linux 机器](https://github.com/linux-lock/bpflock) - 一种基于 eBPF 的安全工具，用于锁定和审计 Linux 机器。
- [Tetragon](https://github.com/cilium/tetragon) - 面向 Kubernetes、基于 eBPF 的安全监测和运行时强制执行工具。

### 工具

- [ply](https://wkz.github.io/ply/) - 一个 Linux 的小型而灵活的开源动态跟踪器，具有类似于 bcc 工具的功能，但语言更简单，灵感来自 awk 和 DTrace。
- [bpftrace](https://bpftrace.org/) - 一个使用自己的高级跟踪语言进行跟踪的工具。它足够灵活，可以被想象成 DTrace 和 SystemTap 的 Linux 替代品。
  - [bpftrace Cheat Sheet](https://www.brendangregg.com/BPF/bpftrace-cheat-sheet.html) - bpftrace 编程的摘要和备忘单。 包含有关语法，探针类型，变量和函数的信息。
- [kubectl trace](https://github.com/iovisor/kubectl-trace) - 一个用于在 Kubernetes 集群中执行 bpftrace 程序的 kubectl 插件。
- [inspektor-gadget](https://github.com/inspektor-gadget/inspektor-gadget) - 基于 eBPF 的工具集合，用于调试和检查 Kubernetes 资源和应用程序。
- [bpfd](https://github.com/genuinetools/bpfd) - 运行带有 Linux 规则的 BPF 程序的框架。 容器感知。
- [BPFd](https://github.com/joelagnel/bpfd) - 明显的 BPF 守护程序，试图利用 bcc 工具的灵活性来跟踪和调试远程目标，特别是在运行 Android 的设备上。
- [adeb](https://github.com/joelagnel/adeb) - 用于在拥有 BPFd 的 Android 上使用跟踪工具的 Linux shell 环境。
- [greggd](https://github.com/olcf/greggd) - 系统守护进程，用于将 eBPF 程序编译和加载到内核中，并将程序输出转发到套接字以进行度量聚合。
- [FUSE](https://events.linuxfoundation.org/wp-content/uploads/2017/11/When-eBPF-Meets-FUSE-Improving-Performance-of-User-File-Systems-Ashish-Bijlani-Georgia-Tech.pdf) - 考虑使用 eBPF。
- [upf-bpf](https://github.com/navarrothiago/upf-bpf) - 基于 XDP 的内核解决方案，适用于 5G UPF。
- [redbpf](https://github.com/foniod/redbpf) - 用于高效编写 Rust 中的 eBPF 代码的工具和框架。

# eBPF在安全中

- [Embrace The Red: Offensive BPF!](https://embracethered.com/blog/tags/ebpf) - 一系列关于BPF介绍的文章，侧重于攻击性场景，以及如何检测其滥用。其中包括关于eBPF的rootkit能力的讨论，或者哪种追踪类型适用于不同的用例。
- [eBPF: Block Linux Fileless Payload "Malware" Execution with BPF LSM](https://djalal.opendz.org/post/ebpf-block-linux-fileless-payload-execution-with-bpf-lsm/) - 关于BPF如何帮助检测和阻止无文件恶意软件的博客文章。
- [Blackhat 2021: With Friends Like eBPF, Who Needs Enemies?](https://www.blackhat.com/us-21/briefings/schedule/#with-friends-like-ebpf-who-needs-enemies-23619) - 讲述一种eBPF rootkit以及eBPF能力的滥用。此rootkit也成为Defcon上的一个演讲主题，[eBPF, I thought we were friends !](https://defcon.org/html/defcon-29/dc-29-speakers.html#fournier)。
- [ebpfkit](https://github.com/Gui774ume/ebpfkit) - 利用多种eBPF特性实施攻击性安全技术的rootkit。
- [ebpfkit-monitor](https://github.com/Gui774ume/ebpfkit-monitor) - 一个实用程序，可在运行时静态分析eBPF字节码或监视可疑的eBPF活动。它专为检测ebpfkit而设计。
- [Bad BPF](https://github.com/pathtofile/bad-bpf) - 恶意eBPF程序的集合，利用eBPF在用户模式程序和内核之间读写用户数据的能力。
- [TripleCross](https://github.com/h3xduck/TripleCross) - 一个Linux eBPF rootkit，具有后门、C2、库注入、执行劫持、持久性和隐蔽性能力。

## 代码

- [linux/include/linux/bpf.h](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/include/linux/bpf.h) - 包含与eBPF相关定义的头文件，适用于内核开发和用户空间交互。
- [linux/include/linux/filter.h](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/include/linux/filter.h) - 包含用于运行BPF程序本身的信息。
- [linux/kernel/bpf/](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/bpf) - 此目录包含大部分与BPF相关的代码。特别是以下文件值得关注：。

- [`syscall.c`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/kernel/bpf/syscall.c) - 系统调用允许的各种操作，如程序加载或映射管理。
  - [`core.c`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/kernel/bpf/core.c) - BPF 解释器。
  - [`verifier.c`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/kernel/bpf/verifier.c) - BPF 验证器。

- [linux/net/core/filter.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/core/filter.c) - 与网络相关的函数和 eBPF 帮助程序（TC，XDP 等）；还包含将 cBPF 字节码迁移到 eBPF 的代码（所有 cBPF 程序在近期内核中都被转换为 eBPF）。
- [linux/kernel/trace/bpf_trace.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/trace/bpf_trace.c) - 与跟踪和监控相关的函数和 eBPF 帮助程序（kprobes，tracepoints 等）。
- JIT 编译器位于其各自体系结构的目录下，例如文件 [linux/arch/x86/net/bpf_jit_comp.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/net/bpf_jit_comp.c) 用于 x86. 对于用于硬件卸载的 JIT 编译器，其驱动程序会有相应的文件，例如 [linux/drivers/net/ethernet/netronome/nfp/bpf/jit.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/drivers/net/ethernet/netronome/nfp/bpf/jit.c) 是针对 Netronome NFP 的。
- [linux/net/sched/](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/sched) - 特别是在文件 `act_bpf.c`（操作）和 `cls_bpf.c`（过滤器）中：与使用 TC 的 BPF 操作和过滤器相关的代码。
- [linux/kernel/seccomp.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/seccomp.c)
- [linux/net/core/dev.c](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/core/dev.c) - 包含函数 `dev_change_xdp_fd()`，该函数通过一个 Netlink 命令调用，将 XDP 程序钩到设备上，然后将从用户空间加载到内核的程序。该函数会使用相关驱动程序的回调函数。

## 开发和社区

- [bpf-next 树](https://git.kernel.org/pub/scm/linux/kernel/git/bpf/bpf-next.git/) - BPF 补丁会被合并进这棵树。它会被定期合并到 [net-next](https://git.kernel.org/pub/scm/linux/kernel/git/davem/net-next.git)，然后每个版本的发布都会合并到 Linus 的树。
- [内核文档](https://git.kernel.org/pub/scm/linux/kernel/git/davem/net-next.git/tree/Documentation/bpf/bpf_devel_QA.rst) - 关于对 BPF 的贡献。
- [netdev 邮件列表](http://lists.openwall.net/netdev/) - 用于 Linux 内核网络栈开发的邮件列表。所有补丁都会发送到此处进行审核和合并。
- [XDP-newbies](http://vger.kernel.org/vger-lists.html#xdp-newbies) - 专门用于 XDP 编程（包括架构和求助）的邮件列表。
- [IO Visor 邮件列表](http://lists.iovisor.org/pipermail/iovisor-dev/) - BPF 是该项目的核心，经常在邮件列表上讨论。
- [@IOVisor Twitter 账号](https://twitter.com/IOVisor)
- [XDP 协作项目](https://github.com/xdp-project/xdp-project) - 一个 GitHub 仓库，提供关于 XDP 未来发展的笔记和想法。

## eBPF相关资源列表

(Note: This translation is in simplified Chinese. If you need traditional Chinese or another Chinese variant, please let me know!)

- [IO Visor的bcc文档](https://github.com/iovisor/bcc/tree/master/docs)
- [IO Visor的bpf-docs存储库](https://github.com/iovisor/bpf-docs/)
- [深入理解BPF：阅读材料列表](https://qmonnet.github.io/whirl-offload/2016/09/01/dive-into-bpf/)。

## 致谢

感谢Quentin Monnet和Daniel Borkmann对 [深入理解BPF：阅读材料列表](https://qmonnet.github.io/whirl-offload/2016/09/01/dive-into-bpf/) 的原创工作，为该列表奠定了基础。

## 贡献

欢迎贡献！首先请阅读[贡献指南](contributing.md)。

## 许可证

[![知识共享CC0](http://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](http://creativecommons.org/publicdomain/zero/1.0)

尽可能根据法律规定，zoidbergwill已放弃对此作品的所有版权和相关权利。