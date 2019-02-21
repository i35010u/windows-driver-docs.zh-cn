---
title: SR-IOV 虚拟功能 (VFs)
description: SR-IOV 虚拟功能 (VFs)
ms.assetid: 92EFC8C3-A610-46EB-A1BC-750715378077
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5fcc02cbe32598a6f7417a75e10fdea49d948ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554946"
---
# <a name="sr-iov-virtual-functions-vfs"></a>SR-IOV 虚拟功能 (VFs)


PCI Express (PCIe) 虚拟函数 (VF) 是一种轻型 PCIe 函数支持单个根 I/O 虚拟化 (SR-IOV) 的网络适配器上。 VF 关联与 PCIe 物理函数 (PF) 上的网络适配器，并表示网络适配器的虚拟化的实例。 每个 VF 具有其自己的 PCI 配置空间。 每个 VF 还与 PF 和其他 VFs 共享一个或多个网络适配器，如外部网络端口上的物理资源。

VF 不成熟的 PCIe 设备。 但是，它提供了用于 HYPER-V 子分区和基础 SR-IOV 网络适配器之间直接传输数据的基本机制。 数据传输相关联的软件资源直接供 VF 并且独立于使用由其他 VFs 或 PF. 但是，PF 微型端口驱动程序运行在管理操作系统的 HYPER-V 父分区中执行大多数这些资源的配置。

作为虚拟网络适配器公开 VF (*VF 网络适配器*) 中的 HYPER-V 子分区中运行来宾操作系统。 VF 与 NIC 交换机的 SR-IOV 网络适配器上的虚拟端口 (VPort) 相关联后，在 VM 中运行的虚拟 PCI (VPCI) 驱动程序将公开 VF 网络适配器。 一旦公开，来宾操作系统中的 PnP 管理器将加载 VF 微型端口驱动程序。

**请注意**  HYPER-V 子分区是也称为*虚拟机 (VM)*。

 

VF 微型端口驱动程序是安装在 VM 中管理 VF NDIS 微型端口驱动程序。 其他 VF 或同一个网络适配器上的 PF 不能影响 VF 微型端口驱动程序执行任何操作。

VF 微型端口驱动程序可以像任何 PCI 设备驱动程序函数。 它可以读取和写入到的 VF PCI 配置空间。 但是，虚拟 PCI 设备的访问权限是一项特权的操作，并由 PF 微型端口驱动程序，如下所示：

-   当 VF 微型端口驱动程序调用[ **NdisMGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff563591)从 VF 网络适配器的 PCI 配置空间读取数据，虚拟化堆栈会收到通知。 此堆栈在 HYPER-V 父分区的管理操作系统中运行。 当堆栈接到通知的读取请求后时，它会发出的对象标识符 (OID) 方法请求[OID\_SRIOV\_读取\_VF\_CONFIG\_空间](https://msdn.microsoft.com/library/windows/hardware/hh451879)到 PF微型端口驱动程序。 中指定要读取的数据[ **NDIS\_SRIOV\_读取\_VF\_配置\_空间\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451681)OID 请求中包含的结构。

    该驱动程序从 VF PCI 配置空间读取请求的数据，并通过完成 OID 请求返回的数据。 此数据然后返回到 VF 微型端口驱动程序时对调用[ **NdisMGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff563591)完成。

-   当 VF 微型端口驱动程序调用[ **NdisMSetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff563670)将数据写入到 VF 网络适配器的 PCI 配置空间，虚拟化堆栈会通知的写入请求。 它发出的 OID 方法请求[OID\_SRIOV\_编写\_VF\_CONFIG\_空间](https://msdn.microsoft.com/library/windows/hardware/hh451925)到 PF 微型端口驱动程序。 中指定要写入的数据[ **NDIS\_SRIOV\_编写\_VF\_配置\_空间\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451688)OID 请求中包含的结构。

    该驱动程序将数据写入到 VF PCI 配置空间和函数完成 OID 请求时返回请求的状态。 此状态在调用后返回到 VF 微型端口驱动程序[ **NdisMSetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff563670)完成。

VF 微型端口驱动程序还可能与 PF 微型端口驱动程序通信。 此通信路径是通过 backchannel 接口。 有关详细信息，请参阅[SR-IOV PF/取景器 Backchannel 通信](sr-iov-pf-vf-backchannel-communication.md)。

**请注意**  VF 微型端口驱动程序必须知道它正在虚拟化环境中，以便它可以与某些操作 PF 微型端口驱动程序进行通信。 该驱动程序如何执行此的详细信息，请参阅[初始化 VF 微型端口驱动程序](initializing-a-vf-miniport-driver.md)。

 

 

 





