---
title: 虚拟化网络的概念和术语
description: 虚拟化网络的概念和术语
ms.assetid: 467996B2-9319-47F9-BAEB-5AC1F20B6E01
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efec1cbf7fdbb0c5d3f0fa9dcd150d60640ea041
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338329"
---
# <a name="virtualized-networking-concepts-and-terms"></a>虚拟化网络的概念和术语


以下列表提供的关键概念和虚拟化网络部分中使用的术语的定义。 我们建议您熟悉这些条款，然后阅读此部分中的其他主题：

<a href="" id="child-partition"></a>子分区  
在 HYPER-V 子分区是基于软件的虚拟机 (VM) 具有无特权访问物理主机计算机的资源。

通过父分区创建每个子分区。 可以有一个或多个主机计算机的 HYPER-V 下运行的子分区。 每个子分区承载来宾操作系统。

一般情况下，子分区不具有直接访问物理硬件资源，并会显示为虚拟设备的资源的虚拟视图。 对虚拟设备的请求将重定向，通过虚拟机总线 (VMBus) 或虚拟机监控程序在其中处理这些请求的父分区。 此外，子分区不能创建其他分区。

**请注意**  从 Windows Server 2012 开始，子分区却可以直接访问物理网络适配器支持单根 I/O 虚拟化 (SR-IOV) 的资源。

 

<a href="" id="emulated-network-adapter"></a>仿真的网络适配器  
在 HYPER-V 子分区中运行来宾操作系统中公开的 HYPER-V 可扩展交换机以太网适配器。 仿真的网络适配器是一种虚拟机网络适配器。 仿真的网络适配器模仿 Intel 网络适配器，并使用硬件仿真转发从可扩展交换机端口和接收的数据包。

在来宾操作系统是 Windows XP、 Windows Vista 或更高版本的 Windows 中公开此适配器。 此适配器还公开在来宾操作系统是一个非 Windows 操作系统中。

<a href="" id="external-extensible-switch-"></a>外部可扩展交换机   

虚拟以太网切换位置之间的 HYPER-V 父分区、 一个或多个 HYPER-V 子分区和主机的物理网络接口路由的数据包。 此类型的交换机允许将数据包发送或接收的 HYPER-V 的所有分区和主机上的物理网络接口之间。

此外，应用程序和管理操作系统中运行的驱动程序可以发送或接收通过此类型的交换机的数据包。

<a href="" id="external-network-adapter"></a>外部网络适配器  
在 HYPER-V 父分区中运行管理操作系统中公开的 HYPER-V 可扩展交换机以太网适配器。 外部网络适配器在主机上绑定到一个或多个物理网络适配器。

外部网络适配器将路由之间的 HYPER-V 分区和主机上的物理网络接口的数据包。

**请注意**  可扩展交换机的每个实例支持多个外部网络适配器。

 

<a href="" id="extensible-switch-team"></a>可扩展交换机团队  
这是一种配置中的可扩展交换机外部网络适配器绑定到的 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟微型端口边缘。 MUX 中间驱动程序绑定到一个或多个物理网络的团队在主机上。

在此配置中，可扩展交换机扩展公开给团队中每个网络适配器。 这样，转发扩展中要管理的配置和使用的团队中的单个网络适配器的可扩展交换机驱动程序堆栈。 例如，该扩展插件可以为负载平衡团队通过故障转移 (LBFO) 解决方案，通过将传出数据包转发到各个适配器提供支持。 此类扩展被称为*组合的提供程序*。

有关详细信息，请参阅[NDIS MUX 中间驱动程序](ndis-mux-intermediate-drivers.md)。

<a href="" id="guest-operating-system"></a>来宾操作系统  
在 HYPER-V 子分区中运行的操作系统。 每个子分区可以托管只有一个操作系统。 但是，许多不同的操作系统可以托管在子分区。 这包括 Windows 和 Linux 的不同版本。

<a href="" id="hypervisor"></a>Hypervisor  
在 HYPER-V 虚拟机监控程序是软件的层之间的物理硬件和一个或多个操作系统运行在 HYPER-V 分区中运行。

虚拟机监控程序的主要用途是提供了名为独立的执行环境*分区*。 虚拟机监控程序提供了与一组硬件资源、 此类内存、 设备和 CPU 周期的每个分区。 虚拟机监控程序控制并进行仲裁从每个分区到底层硬件的访问。

<a href="" id="hyper-v-extensible-switch"></a>HYPER-V 可扩展交换机  
在管理操作系统中运行虚拟以太网交换机。 可扩展交换机的每个实例连接到 HYPER-V 可扩展交换机的网络适配器的端口之间路由数据包。

有关详细信息，请参阅[HYPER-V 可扩展交换机](hyper-v-extensible-switch.md)。

**请注意**  HYPER-V 可扩展交换机支持在 NDIS 6.30 和更高版本的 NDIS。

 

<a href="" id="hyper-v-extensible-switch-extension"></a>HYPER-V 可扩展交换机扩展  
HYPER-V 可扩展交换机扩展是将附加到可扩展交换机驱动程序堆栈的 NDIS 筛选器驱动程序。 附加完成后，该扩展可以捕获、 筛选或转发网络数据包和 NDIS Oid。 可以为连接到可扩展交换机端口的网络适配器转发数据包和 Oid。

在 NDIS 6.30 和更高版本的 NDIS 中支持的 HYPER-V 可扩展交换机扩展。

**请注意**  Windows 筛选平台 (WFP) 提供了筛选扩展 (Wfplwfs.sys) 框中可扩展交换机。 该扩展允许 WFP 筛选器或标注驱动程序来截获的 HYPER-V 可扩展交换机数据路径上的数据包。 这允许筛选器或标注驱动程序来执行数据包检查或修改使用 WFP 管理和系统函数。 有关 WFP 的概述，请参阅[Windows 筛选平台](porting-packet-processing-drivers-and-apps-to-wfp.md)。

 

<a href="" id="hyper-v-extensible-switch-network-adapter"></a>网络适配器的 HYPER-V 可扩展交换机  
托管的 HYPER-V 可扩展交换机的网络适配器。 这些网络适配器连接到可扩展交换机上的端口，并包括以下适配器类型：

-   外部和内部网络适配器在运行 HYPER-V 父分区中管理操作系统中公开的。

-   综合或模拟 VM 网络适配器的 HYPER-V 子分区中运行来宾操作系统中公开的。

<a href="" id="internal-extensible-switch"></a>内部可扩展交换机  
哪些数据包路由之间的 HYPER-V 父分区和一个或多个 HYPER-V 子分区切换虚拟以太网。 此类型的交换机在主机上的物理网络接口从排除数据包流量。

此外，应用程序和管理操作系统中运行的驱动程序可以发送或接收通过此类型的交换机的数据包。

<a href="" id="internal-network-adapter"></a>内部网络适配器  
在 HYPER-V 父分区中运行管理操作系统中公开的 HYPER-V 可扩展交换机以太网适配器。 内部网络适配器发送或接收的 HYPER-V 的所有分区之间的数据包。 但是，内部网络适配器未绑定到主机的物理网络接口。

<a href="" id="i-o-memory-management-unit--iommu-"></a>I/O 内存管理单元 (IOMMU)  
IOMMU 用于将物理内存地址重新映射到子分区所使用的地址。 IOMMU 的操作处理器使用的内存管理硬件无关。

<a href="" id="load-balancing-failover--lbfo--team"></a>负载均衡故障转移 (LBFO) 团队  
这是中的可扩展交换机外部网络适配器绑定到的虚拟微型端口缘 LBFO 提供程序的配置。 LBFO 提供程序本身可以绑定到一个或多个物理网络适配器的团队。

在此配置中，可扩展交换机扩展公开到仅基础虚拟微型端口边缘为网络适配器。 这允许提供程序支持通过绑定到多个物理网络适配器 LBFO 解决方案。 这些适配器不受在可扩展交换机驱动程序堆栈中运行的转发扩展。

<a href="" id="management-operating-system"></a>管理操作系统  
在 HYPER-V 父分区中运行的操作系统。 父分区运行主机计算机运行的操作系统。 对于 HYPER-V，在主计算机必须运行 x64 版本的 Windows Server 2008 或更高版本的 Windows Server。

<a href="" id="network-virtual-service-client--netvsc--driver"></a>网络虚拟服务客户端 (NetVSC) 驱动程序  
在 HYPER-V 子分区的来宾操作系统中运行 NDIS 驱动程序。 NetVSC 公开名为的虚拟化的网络适配器*VM 网络适配器*。

NetVSC 访问通过管理交换机的网络接口转发数据包的 HYPER-V 可扩展交换机。 NetVSC 执行此操作通过将其在 VMBus 上的消息传递到关联 NetVSP 驱动程序。 此驱动程序在 HYPER-V 父分区的管理操作系统中运行。

在大多数情况下，NetVSC 发送，并通过连接到 HYPER-V 可扩展交换机上的端口来接收数据包。 但是，无法配置 NetVSC 为连接到虚拟函数 (VF) 的支持 SR-IOV 接口的物理网络适配器。 在这种情况下，NetVSC 通过发送和接收数据包直接基础物理适配器。

<a href="" id="network-virtual-service-producer--netvsp--driver"></a>网络虚拟服务生成者 (NetVSP) 驱动程序  
在 HYPER-V 父分区的管理操作系统中运行 NDIS 驱动程序。 此驱动程序提供服务以支持由 HYPER-V 子分区的网络访问。

<a href="" id="nic-switch"></a>NIC 开关  
NIC 开关是支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器的硬件组件。 此开关桥网络适配器的物理网络接口和物理函数 (PF) 和在适配器上的一个或多个 VFs 之间的流量。

<a href="" id="partition"></a>分区  
通过虚拟机监控程序管理分区。 每个分区代表独立的处理器和内存资源的逻辑单元。 这允许多个独立的操作系统共享单个硬件平台。

虚拟机监控程序也管理在主计算机上的内存和设备访问策略。 这些策略是不同的父和子分区。

<a href="" id="parent-partition"></a>父分区  
在 HYPER-V 父分区是在主计算机上的第一个分区。 此分区具有特权访问物理主机计算机，如对内存和设备访问的资源。 此外，父分区负责启动虚拟机监控程序和创建子分区。

没有在下运行的 HYPER-V 主机计算机只有一个父分区。 父分区托管在管理操作系统。

**请注意**  父分区是也称为*根*分区。

 

<a href="" id="physical-function--pf-"></a>物理函数 (PF)  
PCI Express (PCIe) 的函数支持单根 I/O 虚拟化 (SR-IOV) 接口。 SR-IOV 扩展 PCIe 接口以启用多个 Vm 共享相同的 PCIe 物理硬件资源。 PF 包含 PCIe SR-IOV 扩展功能结构，以其 PCI 配置空间。

<a href="" id="pf-vf-backchannel"></a>PF/取景器 Backchannel  
微型端口驱动程序的 PCIe 虚拟函数 (VF) 和 PCIe 物理函数 (PF) 之间的专用的基于软件的通信接口。 每个 VF 微型端口驱动程序可以通过反向通道向 PF 微型端口驱动程序发出请求。 PF 微型端口驱动程序可以向单个 VF 微型端口驱动程序通过反向通道发出状态通知。

对 backchannel 界面 PF 和 VF 微型端口驱动程序之间交换数据涉及到使用*VF 配置块*。 每个 VF 配置块是在概念上类似于进程间通信 (IPC) 消息，其中每个块都有一种专有格式，长度，并阻止标识符。 独立硬件供应商 (IHV) 可以定义一个或多个 VF 配置块 PF 和 VF 微型端口驱动程序。

<a href="" id="private-extensible-switch-"></a>专用可扩展交换机   
一个或多个 HYPER-V 子分区之间路由的数据包转换虚拟以太网。 此类型的交换机的 HYPER-V 父分区并且主机上的物理网络接口从排除数据包流量。

**请注意**  应用程序和管理操作系统中运行的驱动程序无法发送或接收通过此类型的交换机的数据包。

 

<a href="" id="single-root-i-o-virtualization--sr-iov-"></a>单根 I/O 虚拟化 (SR-IOV)  
SR-IOV 是一种方法所依据的 PCIe 网络适配器可以将分区到一个物理函数 (PF) 和一个或多个虚函数 (VF)。 在适配器上的每个函数被分配一个唯一的 PCIe 请求者的 id。 这使得适配器可以应用内存和中断翻译，以便可以直接向相应 PF 或 VF 传递不同的网络流量流。 通过避免通过 HYPER-V 可扩展交换机组件的网络流量的路由，SR-IOV 减少 I/O 开销在虚拟化网络环境中。

有关详细信息，请参阅[单根 I/O 虚拟化 (SR-IOV)](single-root-i-o-virtualization--sr-iov-.md)。

**请注意**  在 NDIS 6.30 和更高版本的 NDIS 支持 SR-IOV。

 

<a href="" id="synthetic-data-path"></a>综合数据路径  
在来宾操作系统和管理操作系统中的 HYPER-V 可扩展交换机组件中公开的 VM 网络适配器之间的网络数据路径。

<a href="" id="synthetic-network-adapter"></a>合成网络适配器  
在 HYPER-V 子分区中运行来宾操作系统中公开的 HYPER-V 可扩展交换机以太网适配器。 合成网络适配器是一种虚拟机网络适配器。 在 VM 中运行的网络虚拟服务客户端 (NetVSC) 公开此合成网络适配器。 NetVSC 通过虚拟机总线 (VMBus) 到关联 NetVSP 驱动程序将转发到和从可扩展的交换机端口的数据包。

在来宾操作系统是 Windows Vista 或更高版本的 Windows 中公开此网络适配器。

<a href="" id="virtual-function--vf-"></a>虚函数 (VF)  
PCIe 函数，则支持 SR-IOV 的网络适配器上 PF 与相关联。 VF 与 PF 和其他与同一 PF.相关联 VFs 共享上的适配器，如物理以太网端口，一个或多个物理资源

<a href="" id="vf-data-path"></a>VF 数据路径  
在来宾操作系统和 SR-IOV 网络适配器上的 VF 中公开的 VM 网络适配器之间的网络数据路径。 在此数据路径中，VM 网络适配器是与来宾操作系统中的取景器网络适配器成组。 VF 微型端口驱动程序将与 VM 网络适配器的数据包转发到 VF。 然后数据包进出 VF 到物理网络适配器上的接口转发，NIC 切换 SR-IOV 网络适配器上。

<a href="" id="vf-network-adapter"></a>VF 网络适配器  
VF 来宾操作系统中公开虚拟网络适配器。 如果 VF 分配资源，它将成为附加到子分区 VPCI 总线驱动程序在该分区的来宾操作系统公开 VF 网络适配器。 VPCI 总线驱动程序还会加载此适配器的 VF 微型端口驱动程序。

<a href="" id="virtual-machine--vm-"></a>虚拟机 (VM)  
在软件中实现并托管在物理主机计算机内的虚拟来宾计算机。 虚拟机来模拟的一整套硬件系统，包括处理器和网络适配器，在自包含、 独立的软件环境中。 这样，否则为不兼容的操作系统的并发操作。

每个来宾操作系统在其各自独立的软件的虚拟机中运行。

**请注意**  HYPER-V 中，子分区也称为是 VM。

 

<a href="" id="virtual-machine-bus--vmbus-"></a>虚拟机总线 (VMBus)  
将控件和数据消息传递的 HYPER-V 父级和子级之间分区虚拟通信总线。 通过其在 VMBus 上虚拟服务客户端 (VSC) 和虚拟服务提供程序 (VSP) 组件之间传递的消息进行子分区的主计算机上的物理资源的访问。

<a href="" id="virtual-machine--vm--network-adapter"></a>虚拟机 (VM) 网络适配器  
在来宾操作系统的 HYPER-V 子分区中公开的 HYPER-V 可扩展交换机虚拟网络适配器。

VM 网络适配器支持以下虚拟化类型：

-   VM 网络适配器可能是网络适配器的综合虚拟化 (*合成网络适配器*)。 在这种情况下，在 VM 中运行的网络虚拟服务客户端 (NetVSC) 公开此虚拟网络适配器。 NetVSC 通过虚拟机总线 (VMBus) 将数据包从可扩展交换机端口和接收的转发。

-   VM 网络适配器可以是物理网络适配器的仿真虚拟化 (*仿真的网络适配器*)。 在这种情况下，VM 网络适配器模仿 Intel 网络适配器，并使用硬件仿真转发从可扩展交换机端口和接收的数据包。

可以配置 VM 网络适配器用于访问 HYPER-V 外部、 内部或专用网络接口。

<a href="" id="virtual-machine-queue--vmq-"></a>虚拟机队列 (VMQ)  
支持 VMQ 的网络适配器使用 DMA 直接到虚拟机内存传输所有传入的帧。 VMQ 分布在多个处理器之间的多个 Vm 的网络流量的处理，还可以提高网络吞吐量。

有关详细信息，请参阅[虚拟机队列 (VMQ)](virtual-machine-queue--vmq-.md)。

**请注意**  NDIS 6.20 和更高版本的 NDIS 中支持 VMQ。

 

<a href="" id="virtual-pci--vpci--driver"></a>虚拟 PCI (VPCI) 驱动程序  
在 HYPER-V 子分区的来宾操作系统中运行 PCI 总线驱动程序。 此驱动程序将 VF 公开为来宾操作系统中的虚拟网络适配器。

VPCI 驱动程序的 HYPER-V VSC，与在 HYPER-V 父分区中管理操作系统中运行 VPCI VSP 进行通信。 通过 VMBUS 进行 VPCI VSP 和 VSC 组件之间的通信。

有关 VPCI 接口的详细信息，请参阅[GUID\_PCI\_虚拟化\_接口](https://msdn.microsoft.com/library/windows/hardware/hh451143)。

<a href="" id="virtualization-stack"></a>虚拟化堆栈  
管理创建和执行在 HYPER-V 下的子分区的软件组件的集合。 虚拟化堆栈通过子分区移到主机计算机上的硬件资源来管理访问权限。 在 HYPER-V 父分区中运行虚拟化堆栈。

 

 





