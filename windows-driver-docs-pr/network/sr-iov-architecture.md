---
title: SR-IOV 体系结构
description: SR-IOV 体系结构
ms.assetid: 548856F5-823A-4064-A6C3-28CA9FBA3860
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecfefc6a1feaf4d441499f78402eb21e05fb730c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543039"
---
# <a name="sr-iov-architecture"></a>SR-IOV 体系结构


本部分提供的单个根 I/O 虚拟化 (SR-IOV) 接口的简要概述和及其组件。

下图显示了从 Windows Server 2012 中的 NDIS 6.30 的 SR-IOV 的组件。

![显示与管理父分区的 sr-iov 适配器，并包含来宾操作系统的两个子分区的堆栈关系图](images/sriovarchitecture.png)

SR-IOV 界面由以下组件组成：

<a href="" id="hyper-v-extensible-switch-module"></a>HYPER-V 可扩展交换机模块  
配置 NIC 的可扩展交换机模块上的 SR-IOV 网络适配器，以提供网络连接到 HYPER-V 子分区切换。

**请注意**  HYPER-V 子分区称为*虚拟机 (Vm)*。

 

如果子分区连接到 PCI Express (PCIe) 虚拟函数 (VF)，可扩展交换机模块不参与 VM 和网络适配器之间的数据流量。 相反，直接在 VM 和附加到 VF 之间传递数据流量。

有关可扩展交换机的详细信息，请参阅[HYPER-V 可扩展交换机](hyper-v-extensible-switch.md)。

<a href="" id="physical-function--pf-"></a>物理函数 (PF)  
PF 是支持 SR-IOV 接口的网络适配器的 PCI Express (PCIe) 函数。 PF PCIe 配置空间中包括的 SR-IOV 扩展功能。 此功能用于配置和管理网络适配器，如启用虚拟化和公开 VFs 的 SR-IOV 功能。

有关详细信息，请参阅[SR-IOV 物理函数 (PF)](sr-iov-physical-function--pf-.md)。

<a href="" id="pf-miniport-driver"></a>PF 微型端口驱动程序  
PF 微型端口驱动程序负责管理由一个或多个虚拟网络适配器上的资源。 正因为如此，PF 微型端口驱动程序之前为 VF 分配任何资源的管理操作系统中加载。 PF 微型端口驱动程序将停止后释放已分配给 VFs 的所有资源。

有关详细信息，请参阅[编写的 SR-IOV PF 微型端口驱动程序](writing-sr-iov-pf-miniport-drivers.md)。

<a href="" id="virtual-function--vf-"></a>虚函数 (VF)  
VF 是支持 SR-IOV 接口的网络适配器上的轻型 PCIe 函数。 VF 与网络适配器上 VF 相关联，表示网络适配器的虚拟化的实例。 每个 VF 具有其自己的 PCI 配置空间。 每个 VF 还与 PF 和其他 VFs 共享一个或多个网络适配器，如外部网络端口上的物理资源。

有关详细信息，请参阅[SR-IOV 虚拟功能 (VFs)](sr-iov-virtual-functions--vfs-.md)。

<a href="" id="vf-miniport-driver"></a>VF 微型端口驱动程序  
VF 微型端口驱动程序安装在 VM 中管理 VF。 其他 VF 或同一个网络适配器上的 PF 不能影响 VF 微型端口驱动程序执行任何操作。

有关详细信息，请参阅[编写的 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)。

<a href="" id="network-interface-card--nic--switch"></a>网络接口卡 (NIC) 交换机  
NIC 开关是支持 SR-IOV 接口的网络适配器的硬件组件。 NIC 开关将在适配器上的物理端口和内部虚拟端口 (VPorts) 之间的网络流量转发。 每个 VPort 附加到 PF 或 VF。

有关详细信息，请参阅[NIC 开关](nic-switches.md)。

<a href="" id="virtual-ports--vports-"></a>虚拟端口 (VPorts)  
VPort 是数据对象表示支持 SR-IOV 接口的网络适配器的 NIC 交换机上的内部端口。 类似于物理交换机上的端口，NIC 交换机上的 VPort 将数据包传送到和从 PF 或 VF 端口附加到。

有关详细信息，请参阅[NIC 开关](nic-switches.md)。

<a href="" id="physical-port"></a>物理端口  
物理端口是支持 SR-IOV 接口的网络适配器的硬件组件。 物理端口为外部网络中的适配器上提供的接口。

 

 





