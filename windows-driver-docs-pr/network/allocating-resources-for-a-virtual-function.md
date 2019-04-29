---
title: 为虚拟功能分配资源
description: 为虚拟功能分配资源
ms.assetid: 00191D2C-E093-4DB7-AC82-8E8E5A74656F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d53fae6f93dccd62de66edfe2be9a7e4f857266
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367721"
---
# <a name="allocating-resources-for-a-virtual-function"></a>为虚拟功能分配资源


支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器必须能够支持以下硬件组件：

-   一个 PCI Express (PCIe) 物理函数 (PF)。 PF 始终存在于网络适配器上并附加到 HYPER-V 父分区。

    有关此硬件组件的详细信息，请参阅[SR-IOV 物理函数 (PF)](sr-iov-physical-function--pf-.md)。

-   一个或多个 PCIe 虚拟函数 (VF)。 必须初始化每个取景器，并将其来宾操作系统的网络组件才能发送或接收数据包通过取景器附加到 HYPER-V 子分区。

    有关此硬件组件的详细信息，请参阅[SR-IOV 虚拟功能 (VFs)](sr-iov-virtual-functions--vfs-.md)。

PF 微型端口驱动程序，可以在管理操作系统的 HYPER-V 父分区中运行，PF 和 SR-IOV 网络适配器上的每个 VF 会分配资源。 像任何网络适配器，此驱动程序为 PF 分配资源。 但是，该驱动程序分配资源的每个 VF 如下所示：

-   PF 微型端口驱动程序的每个 VF 驱动程序的网络适配器上创建网络接口卡 (NIC) 时，会分配硬件资源。 该驱动程序将通过调用完成 VFs 的硬件资源分配[ **NdisMEnableVirtualization**](https://msdn.microsoft.com/library/windows/hardware/hh451481)。 此过程的详细信息，请参阅[创建 NIC 交换机](creating-a-nic-switch.md)。

-   PF 微型端口驱动程序为 VF 驱动程序处理的对象标识符 (OID) 方法请求时都分配软件资源[OID\_NIC\_交换机\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)。 即使 VF 已分配给硬件资源，它被视为不再运行直到 PF 微型端口驱动程序已成功完成 OID\_NIC\_交换机\_分配\_VF。

基础驱动程序可以通过发出 OID 方法请求的请求 VF 软件资源的分配[OID\_NIC\_交换机\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构 OID 请求包含一个指向[ **NDIS\_NIC\_交换机\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451593)结构。

从 OID 请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指向[ **NDIS\_NIC\_交换机\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451593)结构。 此结构有一个适配器唯一 VF 标识符和 PCI 请求程序标识符 (RID)。 按以下方式使用这些标识符：

-   基础驱动程序在与 VF，如下所示相关的操作中使用 VF 标识符：

    -   获取通过 OID 方法请求的当前 VF 参数[OID\_NIC\_交换机\_VF\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451824)。

    -   通过 OID VF 释放以前分配的资源设置的请求[OID\_NIC\_交换机\_免费\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822)。

    -   发出重置为通过 OID 集请求的 VF PCI [OID\_SRIOV\_重置\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451889)。

-   虚拟化堆栈用于 RID DMA 和 PF 和 VF 之间中断重新映射。 RID 还使硬件输入/输出内存管理单元 (IOMMU) 若要将来宾物理地址转换为主机的物理地址。

有关详细信息如何过量的驱动程序将发出[OID\_NIC\_交换机\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)方法请求，请参阅[发出 OID\_NIC\_交换机\_分配\_VF 请求](issuing-oid-nic-switch-allocate-vf-requests.md)。

有关如何处理 PF 微型端口驱动程序的详细信息[OID\_NIC\_交换机\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)方法请求，请参阅[处理 OID\_NIC\_交换机\_分配\_VF 请求](handling-oid-nic-switch-allocate-vf-requests.md)。

**请注意**  通过 OID 方法请求的已分配资源 VF 后[OID\_NIC\_开关\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)，资源不能动态更改 VF 的参数。

 

 

 





