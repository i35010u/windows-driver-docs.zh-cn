---
title: 处理 OID_NIC_SWITCH_ALLOCATE_VF 请求
description: 处理 OID_NIC_SWITCH_ALLOCATE_VF 请求
ms.assetid: B48A19D5-A768-4614-961D-1BD00762B6D0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89090263945fc160a9370516ec3ed1c9a9775c2e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526198"
---
# <a name="handling-oidnicswitchallocatevf-requests"></a>处理 OID\_NIC\_交换机\_分配\_VF 请求


当微型端口驱动程序为 PCI Express (PCIe) 物理函数 (PF) 网络适配器上处理的对象标识符 (OID) 方法请求[OID\_NIC\_交换机\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)，它执行以下操作：

-   PF 微型端口驱动程序分配的软件资源的 PCIe 虚拟函数 (VF) 上的网络适配器。 这些资源的配置均基于中指定的参数[ **NDIS\_NIC\_交换机\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451593)结构。

-   PF 微型端口驱动程序将 VF 分配给网络适配器上的 NIC 交换机。 由标识 NIC 开关**SwitchId**的成员[ **NDIS\_NIC\_切换\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451593)结构。

    在 NIC 的交换机上的详细信息，请参阅[NIC 开关](nic-switches.md)。

-   PF 微型端口驱动程序更新**VFId** VF 标识符的成员。 此标识符是从零开始的索引，必须是唯一的分配的所有 VFs PF 微型端口驱动程序通过 NIC 交换机上。

    基础驱动程序使用的值**VFId**成员中的连续 OID 请求[OID\_NIC\_开关\_免费\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822)或[OID\_NIC\_交换机\_VF\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451824)。

-   PF 微型端口驱动程序更新**RequestorId**成员与 VF PCIe 请求程序标识符 (RID)。

    微型端口驱动程序调用[ **NdisMGetVirtualFunctionLocation** ](https://msdn.microsoft.com/library/windows/hardware/hh451487)获取对应于 VF RID 信息。 该驱动程序然后，通过使用创建 RID [ **NDIS\_使\_RID** ](https://msdn.microsoft.com/library/windows/hardware/hh451557)宏根据为调用所返回的信息**NdisMGetVirtualFunctionLocation**。

    虚拟化堆栈用于 RID DMA 和 PF 和 VF 之间中断重新映射。 RID 还使硬件输入/输出内存管理单元 (IOMMU) 若要将来宾物理地址转换为主机的物理地址。

-   PF 微型端口驱动程序初始化，并公开 VF。 这样就可以 VF 可随时用于进行虚拟化堆栈。

如果成功，PF 微型端口驱动程序可以分配必要的软件的资源，并初始化 VF，驱动程序完成 OID 请求使用 NDIS\_状态\_成功。 PF 微型端口驱动程序必须保持的每个已分配 VF VF Id。 NDIS 和基础驱动程序适用于各种操作，例如重置或释放 VF 连续 OID 请求 PF 微型端口驱动程序中使用 VF 标识符。

**请注意**  处于未附加状态是 VF 时 VF 的资源的分配，因为虚拟端口 (VPort) 未附加到 VF。 基础驱动程序可以发出的 OID 请求[OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)创建并附加到 VF VPort。 有关详细信息，请参阅[创建虚拟端口](creating-a-virtual-port.md)。

 

 

 





