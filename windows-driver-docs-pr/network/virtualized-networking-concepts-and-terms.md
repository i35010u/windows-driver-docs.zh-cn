---
title: 虚拟化网络的概念和术语
description: 虚拟化网络的概念和术语
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fe721f36daf0016be6509a22d97d2a44c760951
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793363"
---
# <a name="virtualized-networking-concepts-and-terms"></a>虚拟化网络的概念和术语


以下列表提供了虚拟化网络部分中使用的主要概念和术语的定义。 在阅读本部分中的其他主题之前，建议你熟悉这些术语：

<a href="" id="child-partition"></a>子分区  
在 Hyper-v 中，子分区是基于软件的虚拟机 (VM) 具有对主机物理资源的无特权访问权限。

每个子分区都是通过父分区创建的。 主计算机上的 Hyper-v 中可以有一个或多个子分区。 每个子分区都承载来宾操作系统。

通常，子分区不能直接访问物理硬件资源，而是作为虚拟设备提供资源的虚拟视图。 向虚拟设备发出的请求将通过 VM 总线 (VMBus) 或虚拟机监控程序重定向到处理这些请求的父分区。 此外，子分区无法创建其他分区。

**注意**  从 Windows Server 2012 开始，子分区确实可以直接访问物理网络适配器的资源，该适配器支持 (SR-IOV) 的单个根 i/o 虚拟化。

 

<a href="" id="emulated-network-adapter"></a>仿真网络适配器  
在 Hyper-v 子分区中运行的来宾操作系统中公开的 Hyper-v 可扩展交换机以太网适配器。 仿真网络适配器是一种 VM 网络适配器。 仿真网络适配器模拟 Intel 网络适配器，并使用硬件仿真将数据包转发到可扩展交换机端口并将其从可扩展交换机端口转发。

此适配器在 Windows XP、Windows Vista 或更高版本的 Windows 的来宾操作系统中公开。 此适配器也在非 Windows 操作系统的来宾操作系统中公开。

<a href="" id="external-extensible-switch-"></a>外部可扩展交换机   

一种虚拟以太网交换机，用于在 Hyper-v 父分区、一个或多个 Hyper-v 子分区以及主机的物理网络接口之间路由数据包。 此类型的开关允许在所有 Hyper-v 分区与主机上的物理网络接口之间发送或接收数据包。

此外，在管理操作系统中运行的应用程序和驱动程序可以通过此类型的开关发送或接收数据包。

<a href="" id="external-network-adapter"></a>外部网络适配器  
在管理操作系统中公开的 Hyper-v 可扩展交换机以太网适配器，在 Hyper-v 父分区中运行。 外部网络适配器绑定到主机上的一个或多个物理网络适配器。

外部网络适配器在 Hyper-v 分区与主机上的物理网络接口之间路由数据包。

**注意**  可扩展交换机的每个实例都不支持一个以上的外部网络适配器。

 

<a href="" id="extensible-switch-team"></a>可扩展的交换机团队  
这是一种配置，其中可扩展交换机外部网络适配器绑定到 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟端口边缘。 MUX 中间驱动程序绑定到主机上一个或多个物理网络的团队。

在此配置中，可扩展交换机扩展将公开给团队中的每个网络适配器。 这允许可扩展交换机驱动程序堆栈中的转发扩展管理团队中单个网络适配器的配置和使用。 例如，扩展可以通过将传出数据包转发到各个适配器，为负载平衡故障转移 (LBFO) 解决方案提供支持。 此类扩展称为 *组合提供程序*。

有关详细信息，请参阅 [NDIS MUX 中间驱动程序](ndis-mux-intermediate-drivers.md)。

<a href="" id="guest-operating-system"></a>来宾操作系统  
在 Hyper-v 子分区中运行的操作系统。 每个子分区只能托管一个操作系统。 但是，许多不同的操作系统可以托管在子分区中。 这包括不同版本的 Windows 和 Linux。

<a href="" id="hypervisor"></a>Hypervisor  
在 Hyper-v 中，虚拟机监控程序是在物理硬件与在 Hyper-v 分区中运行的一个或多个操作系统之间运行的软件层。

虚拟机监控程序的主要用途是提供称为 " *分区*" 的独立执行环境。 虚拟机监控程序为每个分区提供一组硬件资源（例如内存、设备和 CPU 周期）。 虚拟机监控程序控制和仲裁从每个分区访问基础硬件。

<a href="" id="hyper-v-extensible-switch"></a>Hyper-V 可扩展交换机  
在管理操作系统中运行的虚拟以太网交换机。 可扩展交换机的每个实例在连接到 Hyper-v 可扩展交换机网络适配器的端口之间路由数据包。

有关详细信息，请参阅 [Hyper-v 可扩展交换机](hyper-v-extensible-switch.md)。

**注意**  Ndis 6.30 和更高版本的 NDIS 支持 Hyper-v 可扩展交换机。

 

<a href="" id="hyper-v-extensible-switch-extension"></a>Hyper-v 可扩展交换机扩展  
Hyper-v 可扩展交换机扩展是附加到可扩展交换机驱动程序堆栈的 NDIS 筛选器驱动程序。 附加后，扩展可以捕获、筛选或转发网络数据包和 NDIS Oid。 数据包和 Oid 可以转发到连接到可扩展交换机端口的网络适配器。

Ndis 6.30 和更高版本的 NDIS 支持 hyper-v 可扩展交换机扩展。

**注意**  Windows 筛选平台 (WFP) 提供内置的可扩展交换机筛选扩展 ( # A0 ) 。 此扩展允许 WFP 筛选器或标注驱动程序按照 Hyper-v 可扩展交换机数据路径截获数据包。 这允许筛选器或标注驱动程序使用 WFP 管理和系统函数执行数据包检查或修改。 有关 WFP 的概述，请参阅 [Windows 筛选平台](porting-packet-processing-drivers-and-apps-to-wfp.md)。

 

<a href="" id="hyper-v-extensible-switch-network-adapter"></a>Hyper-v 可扩展交换机网络适配器  
由 Hyper-v 可扩展交换机管理的网络适配器。 这些网络适配器连接到可扩展交换机上的端口，由以下适配器类型组成：

-   在管理操作系统中公开的、在 Hyper-v 父分区中运行的外部和内部网络适配器。

-   在 Hyper-v 子分区中运行的来宾操作系统中公开的合成或模拟 VM 网络适配器。

<a href="" id="internal-extensible-switch"></a>内部可扩展交换机  
一种虚拟以太网交换机，用于在 Hyper-v 父分区和一个或多个 Hyper-v 子分区之间路由数据包。 此类型的开关从主机上的物理网络接口中排除数据包流量。

此外，在管理操作系统中运行的应用程序和驱动程序可以通过此类型的开关发送或接收数据包。

<a href="" id="internal-network-adapter"></a>内部网络适配器  
在管理操作系统中公开的 Hyper-v 可扩展交换机以太网适配器，在 Hyper-v 父分区中运行。 内部网络适配器在所有 Hyper-v 分区之间发送或接收数据包。 但是，内部网络适配器未绑定到主机的物理网络接口。

<a href="" id="i-o-memory-management-unit--iommu-"></a>I/o 内存管理单元 (IOMMU)   
IOMMU 用于将物理内存地址重新映射到子分区所使用的地址。 IOMMU 独立于处理器使用的内存管理硬件进行操作。

<a href="" id="load-balancing-failover--lbfo--team"></a>LBFO) 团队的负载平衡故障转移 (  
这是一种配置，其中可扩展交换机外部网络适配器绑定到 LBFO 提供程序的虚拟微型端口边缘。 LBFO 提供程序本身可以绑定到一个或多个物理网络适配器的团队。

在此配置中，可扩展交换机扩展仅向网络适配器公开基础虚拟小型端口边缘。 这允许提供程序通过绑定到多个物理网络适配器来支持 LBFO 解决方案。 这些适配器不受可扩展交换机驱动程序堆栈中运行的转发扩展管理。

<a href="" id="management-operating-system"></a>管理操作系统  
在 Hyper-v 父分区中运行的操作系统。 父分区运行在主计算机上运行的操作系统。 对于 Hyper-v，主机必须运行 x64 版本的 windows server 2008 或更高版本的 Windows Server。

<a href="" id="network-virtual-service-client--netvsc--driver"></a>网络虚拟服务客户端 (Netvsc.sys) 驱动程序  
在 Hyper-v 子分区的来宾操作系统中运行的 NDIS 驱动程序。 Netvsc.sys 公开称为 *VM 网络适配器* 的虚拟化网络适配器。

Netvsc.sys 访问 Hyper-v 可扩展交换机，以便通过交换机管理的网络接口转发数据包。 Netvsc.sys 通过将消息通过 VMBus 传递到关联的 NetVSP 驱动程序来实现此功能。 此驱动程序在 Hyper-v 父分区的管理操作系统中运行。

在大多数情况下，Netvsc.sys 通过连接到 Hyper-v 可扩展交换机上的端口来发送和接收数据包。 但是，可以将 Netvsc.sys 配置为连接到支持 SR-IOV 接口的物理网络适配器 (VF) 的虚拟函数。 在这种情况下，Netvsc.sys 直接通过基础物理适配器发送和接收数据包。

<a href="" id="network-virtual-service-producer--netvsp--driver"></a>网络虚拟服务生成方 (NetVSP) 驱动程序  
在 Hyper-v 父分区的管理操作系统中运行的 NDIS 驱动程序。 此驱动程序提供服务以支持 Hyper-v 子分区对网络的访问。

<a href="" id="nic-switch"></a>NIC 交换机  
NIC 交换机是网络适配器的硬件组件，它支持 (SR-IOV) 的单个根 i/o 虚拟化。 此开关将适配器的物理网络接口与物理函数之间的网络流量桥接 (PF) 以及适配器上的一个或多个 VFs。

<a href="" id="partition"></a>依据  
分区由虚拟机监控程序管理。 每个分区代表一个独立处理器和内存资源的逻辑单元。 这允许多个独立的操作系统共享单个硬件平台。

虚拟机监控程序还管理主机计算机上的内存和设备访问策略。 对于父分区和子分区，这些策略是不同的。

<a href="" id="parent-partition"></a>父分区  
在 Hyper-v 中，父分区是主计算机上的第一个分区。 此分区有权访问主机计算机的物理资源，如对内存和设备的访问权限。 此外，父分区负责启动虚拟机监控程序并创建子分区。

在主计算机上的 Hyper-v 中只能运行一个父分区。 父分区承载管理操作系统。

**注意**  父分区也称为 *根* 分区。

 

<a href="" id="physical-function--pf-"></a>物理函数 (PF)   
PCI Express (PCIe) 函数，支持 (SR-IOV) 接口的单个根 i/o 虚拟化。 SR-IOV 扩展了 PCIe 接口，使多个 Vm 共享同一 PCIe 物理硬件资源。 PF 在其 PCI 配置空间中包含 PCIe SR-IOV 扩展功能结构。

<a href="" id="pf-vf-backchannel"></a>PF/VF Backchannel  
在 PCIe 虚函数的小型端口驱动程序之间，基于专用软件的通信接口 (VF) ，而 PCIe 物理功能 (PF) 。 每个 VF 微型端口驱动程序都可以通过 backchannel 将请求发送到 PF 微型端口驱动程序。 PF 小型端口驱动程序可以通过 backchannel 将状态通知发送到单个 VF 微型端口驱动程序。

通过 backchannel 接口在 PF 和 VF 微型端口驱动程序之间交换的数据涉及使用 *VF 配置块*。 每个 VF 配置块在概念上类似于进程间通信 (IPC) 消息，其中每个块都有一个专用的格式、长度和块标识符。 独立硬件供应商 (IHV) 可以为 PF 和 VF 微型端口驱动程序定义一个或多个 VF 配置块。

<a href="" id="private-extensible-switch-"></a>专用可扩展交换机   
一种虚拟以太网交换机，在一个或多个 Hyper-v 子分区之间路由数据包。 这种类型的开关从 Hyper-v 父分区和主机上的物理网络接口中排除数据包流量。

**注意**  在管理操作系统中运行的应用程序和驱动程序无法通过此类型的开关发送或接收数据包。

 

<a href="" id="single-root-i-o-virtualization--sr-iov-"></a>单根 I/O 虚拟化 (SR-IOV)  
SR-IOV 是一种方法，通过该方法，可以将 PCIe 网络适配器分区为一个物理函数 (PF) 和一个或多个虚拟函数 (VF) 。 适配器上的每个函数均分配有一个唯一的 PCIe 请求者 ID。 这使适配器能够应用内存和中断转换，以便可以将不同的网络流量流直接传递到适当的 PF 或 VF。 通过使用 Hyper-v 可扩展交换机组件来避免路由网络流量，SR-IOV 可减少虚拟化网络环境中的 i/o 开销。

有关详细信息，请参阅 [单一根 I/o 虚拟化 (sr-iov) ](single-root-i-o-virtualization--sr-iov-.md)。

**注意**  Ndis 6.30 和更高版本的 NDIS 都支持 SR-IOV。

 

<a href="" id="synthetic-data-path"></a>合成数据路径  
在来宾操作系统中公开的 VM 网络适配器与管理操作系统中的 Hyper-v 可扩展交换机组件之间的网络数据路径。

<a href="" id="synthetic-network-adapter"></a>合成网络适配器  
在 Hyper-v 子分区中运行的来宾操作系统中公开的 Hyper-v 可扩展交换机以太网适配器。 合成网络适配器是一种 VM 网络适配器。 VM 中运行的网络虚拟服务客户端 (Netvsc.sys) 将公开此合成网络适配器。 Netvsc.sys 通过 VM 总线将数据包转发到可扩展交换机端口， (VMBus) 转发到关联的 NetVSP 驱动程序。

此网络适配器在 Windows Vista 或更高版本的 Windows 的来宾操作系统中公开。

<a href="" id="virtual-function--vf-"></a>虚函数 (VF)   
与支持 SR-IOV 的网络适配器上的 PF 关联的 PCIe 函数。 VF 将适配器上的一个或多个物理资源（如物理以太网端口）与 PF 以及与相同 PF 关联的其他 VFs 共享。

<a href="" id="vf-data-path"></a>VF 数据路径  
在来宾操作系统中公开的 VM 网络适配器与 SR-IOV 网络适配器上的 VF 之间的网络数据路径。 在此数据路径中，VM 网络适配器与来宾操作系统中的 VF 网络适配器成组。 VF 微型端口驱动程序将来自 VM 网络适配器的数据包转发到 VF。 SR-IOV 网络适配器上的 NIC 交换机随后将来自 VF 的数据包转发到适配器上的物理网络接口。

<a href="" id="vf-network-adapter"></a>VF 网络适配器  
在虚拟网络的来宾操作系统中公开的虚拟网络适配器。 为 VF 分配资源并将其附加到子分区时，该分区的来宾操作系统中的 VPCI 总线驱动程序将公开 VF 网络适配器。 VPCI 总线驱动程序还会加载此适配器的 VF 微型端口驱动程序。

<a href="" id="virtual-machine--vm-"></a>虚拟机 (VM)   
在软件中实现并且在物理主计算机中托管的虚拟来宾计算机。 虚拟机在自包含的、独立的软件环境中模拟整个硬件系统，从处理器到网络适配器。 这可以实现其他不兼容操作系统的并发操作。

每个来宾操作系统都在其自己的独立软件虚拟机中运行。

**注意**  在 Hyper-v 中，子分区也称为 VM。

 

<a href="" id="virtual-machine-bus--vmbus-"></a>虚拟机总线 (VMBus)   
在 Hyper-v 父分区和子分区之间传递控制和数据消息的虚拟通信总线。 子分区可以通过在虚拟服务客户端 (VSC) 和虚拟服务提供商 (VSP) 组件之间传递的消息，来访问主计算机上的物理资源。

<a href="" id="virtual-machine--vm--network-adapter"></a>虚拟机 (VM) 网络适配器  
在 Hyper-v 子分区的来宾操作系统中公开的 Hyper-v 可扩展交换机虚拟网络适配器。

VM 网络适配器支持以下虚拟化类型：

-   VM 网络适配器可以是网络适配器 (合成 *网络* 适配器) 的综合虚拟化。 在这种情况下，VM 中运行的网络虚拟服务客户端 (Netvsc.sys) 将公开此虚拟网络适配器。 Netvsc.sys)  (VMBus，将数据包转发到可扩展交换机端口，并将其从可扩展交换机端口转发。

-   VM 网络适配器可以是物理网络适配器的模拟虚拟化 (*仿真网络适配器*) 。 在这种情况下，VM 网络适配器模拟 Intel 网络适配器，并使用硬件仿真将数据包转发到可扩展交换机端口并将其从可扩展交换机端口转发。

可以将 VM 网络适配器配置为访问 Hyper-v 外部、内部或专用网络接口。

<a href="" id="virtual-machine-queue--vmq-"></a>虚拟机队列 (VMQ)  
支持 VMQ 的网络适配器使用 DMA 将所有传入帧直接传输到 VM 内存。 VMQ 还通过将多个 Vm 的网络流量处理分散到多个处理器，从而提高了网络吞吐量。

有关详细信息，请参阅 [ (VMQ) 虚拟机队列 ](virtual-machine-queue--vmq-.md)。

**注意**  在 ndis 6.20 和更高版本的 NDIS 中支持 VMQ。

 

<a href="" id="virtual-pci--vpci--driver"></a>虚拟 PCI (VPCI) 驱动程序  
在 Hyper-v 子分区的来宾操作系统中运行的 PCI 总线驱动程序。 此驱动程序将 VF 公开为来宾操作系统中的虚拟网络适配器。

VPCI 驱动程序为 Hyper-v VSC，并与 Hyper-v 父分区的管理操作系统中运行的 VPCI VSP 通信。 VPCI VSP 和 VSC 组件之间的通信在 VMBUS 上进行。

有关 VPCI 接口的详细信息，请参阅 [GUID \_ PCI \_ 虚拟化 \_ 接口](https://msdn.microsoft.com/library/windows/hardware/hh451143)。

<a href="" id="virtualization-stack"></a>虚拟化堆栈  
管理 Hyper-v 下子分区的创建和执行的软件组件的集合。 虚拟化堆栈管理子分区对主计算机上的硬件资源的访问。 虚拟化堆栈在 Hyper-v 父分区中运行。

 

 





