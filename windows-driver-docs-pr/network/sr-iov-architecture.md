---
title: SR-IOV 体系结构
description: SR-IOV 体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6598b40597f2fc86215aee69b103e3495a93c939
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834341"
---
# <a name="sr-iov-architecture"></a>SR-IOV 体系结构


本部分简要概述了 (SR-IOV) 接口及其组件的单个根 i/o 虚拟化。

下图显示了从 Windows Server 2012 中的 NDIS 6.30 开始的 SR-IOV 组件。

![显示具有管理父分区和包含来宾操作系统的两个子分区的 sr-iov 适配器的堆栈关系图](images/sriovarchitecture.png)

SR-IOV 接口包含以下组件：

<a href="" id="hyper-v-extensible-switch-module"></a>Hyper-v 可扩展交换机模块  
可扩展交换机模块，用于在 SR-IOV 网络适配器上配置 NIC 交换机，以便与 Hyper-v 子分区建立网络连接。

**注意**  Hyper-v 子分区称为 *虚拟机 (vm)*。

 

如果子分区连接到 PCI Express (PCIe) 虚函数 (VF) ，则可扩展交换机模块不参与 VM 和网络适配器之间的数据流量。 相反，数据流量直接在 VM 与其附加到的虚拟机之间进行传递。

有关可扩展交换机的详细信息，请参阅 [Hyper-v 可扩展交换机](hyper-v-extensible-switch.md)。

<a href="" id="physical-function--pf-"></a>物理函数 (PF)   
PF 是支持 SR-IOV 接口的网络适配器的 PCI Express (PCIe) 功能。 PF 在 PCIe 配置空间中包括 SR-IOV 扩展功能。 此功能用于配置和管理网络适配器的 SR-IOV 功能，如启用虚拟化并公开 VFs。

有关详细信息，请参阅 [Sr-iov 物理 Function (PF) ](sr-iov-physical-function--pf-.md)。

<a href="" id="pf-miniport-driver"></a>PF 微型端口驱动程序  
PF 微型端口驱动程序负责管理网络适配器上一个或多个 VFs 使用的资源。 因此，在为 VF 分配任何资源之前，会在管理操作系统中加载 PF 微型端口驱动程序。 释放为 VFs 分配的所有资源后，将停止 PF 微型端口驱动程序。

有关详细信息，请参阅 [编写 SR-IOV PF 微型端口驱动程序](writing-sr-iov-pf-miniport-drivers.md)。

<a href="" id="virtual-function--vf-"></a>虚函数 (VF)   
VF 是网络适配器上支持 SR-IOV 接口的轻量 PCIe 函数。 VF 与网络适配器上的 VF 相关联，表示网络适配器的虚拟化实例。 每个 VF 都有其自己的 PCI 配置空间。 每个 VF 还将网络适配器上的一个或多个物理资源（例如外部网络端口）与 PF 和其他 VFs 共享。

有关详细信息，请参阅 [sr-iov)  (Sr-iov 虚拟函数 ](sr-iov-virtual-functions--vfs-.md)。

<a href="" id="vf-miniport-driver"></a>VF 微型端口驱动程序  
VM 中安装了 VF 微型端口驱动程序来管理虚拟机。 由 VF 微型端口驱动程序执行的任何操作都不得影响同一网络适配器上的任何其他 VF 或 PF。

有关详细信息，请参阅 [编写 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)。

<a href="" id="network-interface-card--nic--switch"></a>网络接口卡 (NIC) 交换机  
NIC 交换机是支持 SR-IOV 接口的网络适配器的硬件组件。 NIC 交换机将网络流量转发到适配器上的物理端口和内部虚拟端口 (VPorts) 。 每个 VPort 都附加到 PF 或 VF。

有关详细信息，请参阅 [NIC 交换机](nic-switches.md)。

<a href="" id="virtual-ports--vports-"></a>虚拟端口 (VPort)  
VPort 是一个数据对象，表示支持 SR-IOV 接口的网络适配器的 NIC 交换机上的内部端口。 类似于物理交换机上的端口，NIC 交换机上的 VPort 提供进出端口的 PF 或 VF 的数据包。

有关详细信息，请参阅 [NIC 交换机](nic-switches.md)。

<a href="" id="physical-port"></a>物理端口  
物理端口是支持 SR-IOV 接口的网络适配器的硬件组件。 物理端口向外部网络介质提供适配器上的接口。

 

 





